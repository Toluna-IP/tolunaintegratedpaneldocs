---
title: Quota Details
has_children: false
parent: ES API
grand_parent: External Sample Offering
nav_order: 7
---

# Quota Details Endpoint
{: .no_toc}

At times, it is beneficial for a Partner to obtain the status of a single Quota regardless of whether or not it would be included in the [GetQuotas](/externalsample/api/getquotas) request. This is the purpose of QuotaDetails, an exclusive feature for Partners using ES Integration.

The method, explained below, reveals if the requested Quota is available for ES, if the Partner qualifies for the Quota, and the Quota details (provided the Partner qualifies).

* TOC
{:toc}

## Request

### Route
```
GET {IP_ES_URL}/IPExternalSamplingService/ExternalSample/{panelGUID}/QuotaStatus/{quotaID}
```

### Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| PanelGUID | ```Guid``` | A Toluna-issued unique identifier for a Partner's culture-specific panel. | Yes |
| QuotaID | ```int``` | Toluna's unique identifier for a Quota | Yes |

### Headers

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| API_AUTH_KEY | ```GUID``` | A Partner-specific GUID provided by Toluna | Yes |

### Body Details
 - None

### Example Request
```
GET {IP_ES_URL}/IPExternalSamplingService/ExternalSample/XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX/QuotaStatus/42386
```

## Response

For response details, please refer to the [Get Quotas Page](/externalsample/api/getquotas#response).

### Example Responses

#### Survey Available for Partner
```json
{
"QuotaID": 42387,
"CountryID": 2000223,
"CompletesRequired": 5,
"EstimatedCompletesRemaining": 5,
"Layers": [
{
"LayerID": 56059,
"SubQuotas": [
{
"QuestionsAndAnswers": [
{
"QuestionID": 1001538,
"AnswerIDs": [],
"AnswerValues": [
"18-75"
],
"IsRoutable": false
}
],
"SubQuotaID": 167082,
"CurrentCompletes": 0,
"MaxTargetCompletes": 5
}
]
}
],
"CacheExpires": "2020-01-31T21:19:30.3616306Z"
}
```

### Survey Not Available for Partner
```json
{
"Result": "SURVEY_NOT_AVAILABLE_FOR_PARTNER",
"ResultCode": 42
}
```