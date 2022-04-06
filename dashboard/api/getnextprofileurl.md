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
GET https://{IP_CORE_URL}/IntegratedPanelService/api/Profile/GetNextProfileURL/?memberCode={memberCode}&partnerGuid={partnerGUID}&cancelURL={cancelURL}&returnURL={returnURL}
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

