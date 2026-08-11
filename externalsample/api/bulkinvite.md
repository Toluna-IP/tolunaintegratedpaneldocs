---
title: Bulk Invite
has_children: false
parent: ES API
grand_parent: External Sample Offering
nav_order: 3
nav_exclude: true
search_exclude: true
---


# Bulk Invite
{: .no_toc }

This Route can be used to attempt to generate multiple Invites for one Member from a given list of Quotas. 

> **Please note:** response times of the API will be proportionally affected by the number of QuotaIDs included with the Request.


* TOC
{:toc}


---

## Request

### Route
```plaintext
POST https://{IP_ES_URL}/IPExternalSamplingService/ExternalSample/{PanelGuid}/{MemberCode}/Invites
```

### Route Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| PanelGUID | ```Guid``` | A Toluna-issued unique identifier for a Partner's culture-specific panel | Yes |
| MemberCode | ```string``` | Partner's unique identifier for the Member as define when registered with Toluna. The PanelGUID+MemberCode is always unique within the Toluna system | Yes |

### Route Header(s) 

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| API_AUTH_KEY | ```GUID``` | A Partner-specific GUID provided by Toluna | Yes |


### Body Details

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| QuotaIDs | ```arrary<int>``` | List of Quota IDs pulled from the [GetQuotas API](/externalsample/api/getquotas.html). **Note:** No more than 100 quotas should be requested with any one Invites call. | Yes |


### Example Request

```plaintext
POST https://{IP_ES_URL}/IPExternalSamplingService/ExternalSample/XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX/MyMemberCode/Invites
API_AUTH_KEY: XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX

{
    "QuotaIDs": [
        1234567,
        8910111
    ]
}
```

---

## Response


### Possible Codes

| Code | Etiology, actions |
| :--- | :--- |
| 200 | Request processed normally |
| 400 | Bad Request: see response for details |
| 500 | Internal Error: An exception occurred while processing the request. Toluna likely has captured details in its logs |
| 403 | Forbidden: Invalid API_AUTH_KEY. See response for details |


### Body Details


| Name | Type | Description |
| :--- | :--- | :--- |
| Invites | ```array<object>``` | List of Invite responses for each QuotaID provided |

#### Invites Objects

| Name | Type | Description |
| :--- | :--- | :--- |
| QuotaID | ```int``` | Toluna’s unique identifier for a Quota |
| Invite | ```array<object>``` | Details of the Invite provided the Member is eligible for the Quota. *nullable* |
| ResultCode | ```int``` | Unique identifier for the Invite result. For a list of possible codes, please click [here](/externalsample/api/common.html). **Note:** a value of 1 indicates a successful Invite generation |
| Result | ```string``` | Toluna's result of the Invite generation attempt. For a list of possible results, please click [here](/externalsample/api/common.html). **Note:** a successful Invite generate will produce ```"Result": "SUCCESS"``` |

#### Invite Objects

| Name | Type | Description |
| :--- | :--- | :--- |
| SurveyID | int | Toluna's unique identifier for a Survey |
| WaveID | int | Toluna's unique identifier for a single iteration of a Survey. The SurveyID+WaveID is always unique |
| QuotaID | int | Toluna's uniqiue identifier for a Quota |
| MemberAmount | double | Amount Partner has agreed to pay it’s Member for a complete. This is rarely used and Toluna prefers to avoid direct engagement with the Partner-Member relationship |
| PartnerAmount | double | Amount Toluna has agreed to pay Partner for a complete. Note: for patners using the Programmatic Pricing model, this amount may vary until the member enters the survey |
| URL | string | Link to Invite Member to Quota |
| LOI | int | Length of Interview at the time of invite generation. Valued in minutes |
| IR | int | Incidence Rate at the time fo invite generation |


### Example Response

```json
{
    "Invites": [
        {
            "QuotaID": 1234567,
            "Invite": null,
            "ResultCode": 9,
            "Result": "QUOTA_NOT_LIVE"
        },
        {
            "QuotaID": 1213141,
            "Invite": {
                "SurveyID": 5299929,
                "WaveID": 3848788,
                "QuotaID": 23691639,
                "URL": "https://ups.surveyrouter.com/TrafficUI/MSCUI/Page.aspx?pgtid=20&di=pbGASQj072mPPYpFkvAkM250fmM3m6PScWt3gPiJDiaDWtIE1l8u2lKMm41chgFDLuRSTRLa6ZoCdeeQoRb6nSSgE4E41107",
                "LOI": 13,
                "IR": 23,
                "MemberAmount": 0.0,
                "PartnerAmount": 0.55
            },
            "ResultCode": 1,
            "Result": "SUCCESS"
        },
        {
            "QuotaID": 8910111,
            "Invite": {
                "SurveyID": 5525106,
                "WaveID": 4079828,
                "QuotaID": 24233253,
                "URL": "https://ups.surveyrouter.com/TrafficUI/MSCUI/Page.aspx?pgtid=20&di=mvgMpE1Y072oNv5O1Ki26I5OOcx14pkWfeQR72gvE1jNF0ODPMpXsQAOhdtMb2Uu4sben3nVKBMlPtnSAdFwszTQE4E41107",
                "LOI": 15,
                "IR": 90,
                "MemberAmount": 0.0,
                "PartnerAmount": 0.71
            },
            "ResultCode": 1,
            "Result": "SUCCESS"
        }
    ]
}
```