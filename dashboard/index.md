---
title: Dashboard Offering
has_children: false
nav_order: 3
---

# Dashboard Offering 
{: .no_toc }

* TOC
{:toc}

## Introduction

Toluna provides a RESTful way to get surveys to display to your panel on your own website. This can be accomplished once the respondent data is loaded into Toluna’s system. Please note that Toluna caches the results of this call for 1 minute; repeated calls within this timeframe will NOT consult the Toluna router and will instead return the latest results from cache.

---

## Flow Diagram

![Dashboard Flow Diagram](https://github.com/josh-toluna/tolunaintegratedpaneldocs/blob/master/resources/flows/IP%20Flow%20Diagrams-Dashboard.png?raw=true)

---

## Request

### Route
```
GET  http://{IP_CORE_URL}/IntegratedPanelService/api/Surveys/?memberCode={MemberCode}&partnerGuid={PartnerGUID}&numberOfSurveys=2&mobileCompatible=false&deviceTypeIDs=1&deviceTypeIDs=2
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| MemberCode | ```int``` | Unique Respondent Code from the Partner |
| PartnerGUID | ```Guid``` | Unique Partner code provided by Toluna |
| NumberOfSurveys | ```string``` | Number of Surveys the Partner is requesting to receive to show the Member (maximum 5 available) |
| MobileCombatible | ```bool``` | When TRUE, only mobile combatible surveys will be shown. *Depreciate as of v2.3. Use DeviceTypeIDs instead* |
| DeviceTypeIDs | ```int``` | Indicated the device types for which Surveys should be returned. Supported values: 1=Desktop/Laptop, 2=Tablet, 3=Phone. *When "DeviceTypeIDs" are supplied, the "MobileCombatible" parameter is ignored* |

---

## Response

### Possible Codes

| Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, results returned without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 500 | Internal Error. An exception occurred while processing the request. Toluna likely has the details captured in its logs |

### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| SurveyID | ```int``` | Toluna-specified Survey identifier |
| Name | ```string``` | Toluna-specified Survey name |
| URL | ```string``` | Clicking on the URL will take this specific Respondent to the survey. URL’s are unique to the respondent and are **NOT** to be used by other respondents. |
| Desription | ```string``` | Description of the Survey |
| Duration | ```int``` | Estimated length of interview |
| IR | ```int``` | Incidence rate fo the Survey |
| MemberAmount | ```decimal``` | This is currently only returned as a value > 0 if the partner has a specific amount that is paid to each of their respondents for a survey |
| PartnerAmount | ```decimal``` | This is what the negotiated amount Toluna will pay the partner if the respondent successfully completes and the responses qualify for our client |
| WaveID | ```int``` | Current iteration of the survey. Studies related to one another can be sent in “waves” that the Member experiences as unique surveys. SurveyID+WaveID is always unique |
| IsTqsSurvey | ```bool``` | Indicates whether the Survey returned from Dashboard belongs to Toluna Quick Survey. For non-TQS surveys, this property will not appear |

>Note: v2.1 requires Partners to opt-in to WaveID and IsTqsSurvey features. They will not appear by default

### Example Response
```json
[
 {
 "SurveyID": 21737,
 "Name": "1063626-US-IP1",
 "URL":
"http://ups.surveyrouter.com/TrafficUI/MSCUI/Page.aspx?pgtid=20&di=zi19HDWwzDwhDXE2DjZ8NIlZX8LPjuUJh
kV37eSE1dC3kE4",
 "Description": "Entertainment",
 "Duration": 0,
 "MemberAmount": 0,
 "PartnerAmount": 2,
 "WaveId": 100,
 "IsTqsSurvey": true
 }
]
```

---

## Demographic Requirements

In order to place a Member into a Survey, Toluna must know - at a minimum - the panelist Date of Birth and Gender. When the Dashboard is called for a Member lacking this information, Toluna returns a special result: a single link to a Member Profile page. The panelist can use this link to submit the missing data. Once complete, future calls to the Dashboard will result in the normal result of Survey links.

### Example Response Demographic Data Missing

```json
{
 "SurveyID": 0,
 "Name": "MemberProfileSurvey",
 "URL":"http://surveyqa.na.toluna.com/TrafficUI/MSCUI/Profilepage.aspx?guid=55725428-e128-4dfb-90d7-51ffaee7a574&rt=9&pt=1000082&bid=200&cid=1&brandcss=1&redirect=http%3a%2f%2fsurveyqa.na.toluna.com%2fTrafficUI%2fMSCUI%2fpage.aspx%3fpgtid%3d23&cancel=http%3a%2f%2fsurveyqa.na.toluna.com%2fTrafficUI%2fMSCUI%2fpage.aspx%3fpgtid%3d22",
 "Description": "contains link to a Member Profile Page",
 "Duration": "5",
 "MemberAmount": 0,
 "PartnerAmount": 0
}
```



## Survey Profiles

Toluna’s client Surveys are always looking for rich profile information for all Respondents. Additional profile information for a Respondent increases the likelihood of a respondent qualifying for a Survey. Toluna provides a RESTful way to get access to these Survey Profiles that can be filled out by your Respondents.

### Route
```
**GET**  http://{IP_CORE_URL/IntegratedPanelService/api/Profile/GetNextProfileURL/
```

>Note: This request can be made multiple times. Toluna keeps track of the profiles filled by each respondent and will not offer to fill an already filled profile for a respondent.

### Request Parameters

| Name | Description |
| :--- | :--- |
| MemberCode | Unique Respondent code from the Partner |
| PartnerGUID | Unique Partner code provided by Toluna |
| cancelURl | URL the Respondent should be redirected to if they click cancel on the Profiler |
| returnURL | URL the Respondent should be redirected to if tey click save on teh Profiler |

### Possible Response Codes

| Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally; results returned without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 500 | Internal Error. An exception occurred while processing the request. Toluna likely has details captured in its logs |

### Example Response

To view a sample result, paste the following URL in your browser.

http://ups.surveyrouter.com/TrafficUI/MSCUI/Profilepage.aspx?guid=ce009f76-2076-4a16-89a1-714fe356af38&rt=9&pt=1000080&bid=200&cid=1&brandcss=1&redirect=http%3a%2f%2fwww.google.com&cancel=http%3a%2f%2fwww.google.com

This page can be hosted in an iframe on your website. When the respondent clicks save, the data will be saved on Toluna’s site and the user will be able to qualify for more surveys

---