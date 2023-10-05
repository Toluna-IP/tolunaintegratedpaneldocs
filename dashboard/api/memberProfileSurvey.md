---
title: Profiling Survey
has_children: false
nav_order: 99
parent: Dashboard API
grand_parent: Dashboard Offering
nav_exclude: false
search_exclude: true
---


# Profiling Survey
{: .no_toc }

## Table of Contents
{:toc}

---

## Use Case

In genral, the minimum attributes Toluna needs to know about a member in order to match them to a survey are BirthDate and Gender. There may be cases, however, when a Partner does not have access to this information. If you are on this page, it's highly likely you currently do or will fall into this category.  

For members without BirthDate or Gender assigned, Toluna can route them through a Member Profile Survey. This survey will ask the member a few questions and assign those answers to the member's profile. At the completion of the survey, the member will be returned to the Partner's defined End Page. 

The method to produce the Member Profile Survey is identical to that of the [Get Surveys API](/dashboard/api/getsurveys.html). The Member Profiling Survey will be automatically returned whenever surveys are requested of a member registered without the minimum attributes needed

{: .highlight }
Note: Toluna does not request or store PII Regulated information.

## Request

### Route
```plaintext
GET  https://{IP_CORE_URL}/IntegratedPanelService/api/Surveys/?memberCode={MemberCode}&partnerGuid={PartnerGUID}&numberOfSurveys=2&mobileCompatible=false&deviceTypeIDs=1&deviceTypeIDs=2
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| MemberCode | ```int``` | Unique Respondent Code from the Partner |
| PartnerGUID | ```Guid``` | Unique Partner code provided by Toluna |
| NumberOfSurveys | ```string``` | Number of Surveys the Partner is requesting to receive to show the Member (maximum 5 available) |
| MobileCompatible | ```bool``` | Optional - When TRUE, only mobile compatible surveys will be shown. This property will be deprecated in the future with an announcement. Use DeviceTypeIDs instead.  |
| DeviceTypeIDs | ```int``` | Indicated the device types for which Surveys should be returned. Supported values: 1=Desktop/Laptop, 2=Tablet, 3=Phone. *When "DeviceTypeIDs" are supplied, the "MobileCompatible" parameter is ignored* |

---

## Response

### Possible Response Codes

| Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, results returned without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 500 | Internal Error. An exception occurred while processing the request. Toluna likely has the details captured in its logs |

### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| SurveyID | ```int``` | Toluna-specified Survey identifier |
| WaveId | ```null``` | Always null for the Member Profiling Survey |
| Name | ```string``` | Toluna-specified Survey name. "MemberProfileSurvey" |
| URL | ```string``` | Invitation link. Clicking on the URL will take this specific Respondent to the survey. |
| Duration | ```int``` | Estimated length of interview |
| IR | ```null``` | Always null for the Member Profiling Survey |
| MemberAmount | ```decimal``` | By default, the Member Profile Survey is not incentivized to the Member by Toluna. |
| PartnerAmount | ```decimal``` | By default, the Member Profile Survey is not incentivized to the Partner by Toluna. |


### Example Response
```plaintext
[
    {
        "SurveyID": 1000001,
        "WaveId": null,
        "Name": "MemberProfileSurvey",
        "URL": "https://www.quicksurveys.com/tqsruntime/service?getDataUrl=https%3a%2f%2fttm.toluna.com%2fapi%2fsurveys%2fstart%3fsurveyStartDataEncrypted%3dcib8SUikmO4yif3RyYa%2bKLxWGCjkefejGYcNTnn3m96olsXa4e8d6HXTMy2bXMGxJUGRKgk%2b%2faHg7MNAXEOwPBe13F7k2sSRX8lRY1z62Xr2i64L1FRb%2bGdAc%2b95ruC0uETnJohyp%2bS3ORObMvDHi8lu690FOkXWc8c6ceKuQY9W2MgDTFMRaAyEOqecrioZ8P8rsub2RbgGHH2wdT0gd6AFMt8qwxjvFxzLL0%2bB1ZngPAMBFzqyPoNwrHIPhBlcki4LxNQJ2l3fePwrYpdXFrRnvbXFJDhKdC%2bw63hSEiNvxhbe5zfl%2bfv8SO9WGhyerANipTCIexuhwznxeVSCwrDlJS2O1KEdE280QqAtu2v732Dn59n2PlLf5F%2fuMI5OTYkpnsOUBpbfVJPqm76KXxqb8orBEXos5oZ3BTTIdQnMsMLWeBB7QENS3yFKRNBpYW50m9nbxfSLVvvwq%2bKqb%2fJZcvrwyX%2fTTMmkmjV26ObV2H2mXFlWDXa7PTNae8niEtX4pJ7ZuzJlqnbE6%2f3uyw%3d%3d&cultureid=7&location=IntegratedPanelService",
        "Duration": "5",
        "IR": null,
        "MemberAmount": 0.0,
        "PartnerAmount": 0.0
    }
]
```