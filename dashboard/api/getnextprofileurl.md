---
title: Get Next Profile Url
has_children: false
parent: 
grand_parent: Dashboard Offering
nav_order: 2
nav_exclude: true
search_exclude: true
---


# Get Next Profile Url
{: .no_toc }

* TEST
{:toc}

---


Toluna’s client Surveys are always looking for rich profile information for all members. Additional profile information for a member increases the likelihood of that member qualifying for a Survey. Toluna provides a RESTful way to get access to these Survey Profiles that can be filled out by your members.

### Route
```plaintext
GET https://{IP_CORE_URL}/IntegratedPanelService/api/Profile/GetNextProfileURL/?memberCode={memberCode}&partnerGuid={partnerGUID}&cancelURL={cancelURL}&returnURL={returnURL}
```

>Note: This request can not be made multiple times for the same Member. Toluna keeps track of the profiles filled by each member and will not offer to fill an already filled profile for a member. Additional changes to a member's profile will need to be made using the [Update Member API](/membermanagement/v2/update) from the Member Management API group.

### Request Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| MemberCode | ```string``` | Unique member code from the Partner | Yes |
| PartnerGUID | ```GUID``` | Unique Partner code provided by Toluna | Yes |
| cancelURL | ```string``` | URL the member should be redirected to if they click cancel on the Profiler | Yes |
| returnURL | ```string``` | URL the member should be redirected to if they click save on the Profiler | Yes |

### Possible Response Codes

| Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally; results returned without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 404 | Member's profile already includes pertinent information. NextProfileSurvey not available |
| 500 | Internal Error. An exception occurred while processing the request. Toluna likely has details captured in its logs |

