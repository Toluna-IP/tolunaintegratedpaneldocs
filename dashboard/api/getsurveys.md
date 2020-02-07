---
title: Get Surveys
has_children: false
parent: Dashboard API
grand_parent: Dashboard Offering
nav_order: 1
---


# Get Surveys
{: .no_toc }

* TEST
{:toc}

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