---
title: GetSurveyStatus
has_children: false
parent: Reporting
nav_order: 2
---

## GetSurveyStatus

Returns status information for the request survey. Two options available: by ID Parameters or by Name Parameters.

### By ID Parameters

#### Route
```plaintext
GET http://{IP_CORE_URL}/IntegratedPanelService/api/Reports/Surveys/{SurveyID}/StatusByID/?SamplePartnerGuid={ParnerGUID}
```

#### Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| SurveyID | ```int``` | Toluna's SurveyID | Yes |
| PartnerGUID | ```GUID``` | API key provided by Toluna | Yes |

### By Name Parameters

#### Route
```plaintext
GET http://{IP_CORE_URL}/IntegratedPanelService/api/Reports/Surveys/{SurveyName}/StatusByName/?SamplePartnerGUID={PartnerGUID}
```

#### Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| SurveyName | ```string``` | Toluna external Survey Name | Yes |
| PartnerGUID | ```GUID``` | API key provided by Toluna | Yes |

### Possible Response Codes

| Code | Etiology, actions |
| 200 | OK. Request processed normally; results returned without issue |
| 404 | Not Found. Could not find a Survey for the input |
| 500 | Internal Error. An exception occurred while processing the request. Toluna likely has details captured in its logs |

### Example Response
```plaintext
{
 "Status": "CLOSED",
 "SurveyName": "1072552-BR",
 "SurveyID": 31033,
 “WaveID”: 247
}
```