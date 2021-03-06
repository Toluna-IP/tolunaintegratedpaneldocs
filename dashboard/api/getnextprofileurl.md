---
title: Get Next Profile Url
has_children: false
parent: Dashboard API
grand_parent: Dashboard Offering
nav_order: 2
---


# Get Next Profile Url
{: .no_toc }

* TEST
{:toc}

---


Toluna’s client Surveys are always looking for rich profile information for all Respondents. Additional profile information for a Respondent increases the likelihood of a respondent qualifying for a Survey. Toluna provides a RESTful way to get access to these Survey Profiles that can be filled out by your Respondents.

### Route
```plaintext
GET http://{IP_CORE_URL}/IntegratedPanelService/api/Profile/GetNextProfileURL/?memberCode={memberCode}&partnerGuid={partnerGUID}&cancelURL={cancelURL}&returnURL={returnURL}
```

>Note: This request can be made multiple times. Toluna keeps track of the profiles filled by each respondent and will not offer to fill an already filled profile for a respondent.

### Request Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| MemberCode | ```string``` | Unique Respondent code from the Partner | Yes |
| PartnerGUID | ```GUID``` | Unique Partner code provided by Toluna | Yes |
| cancelURL | ```string``` | URL the Respondent should be redirected to if they click cancel on the Profiler | Yes |
| returnURL | ```string``` | URL the Respondent should be redirected to if tey click save on the Profiler | Yes |

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