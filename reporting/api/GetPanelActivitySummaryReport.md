---
title: GetPanelActivitySummaryReport
has_children: false
parent: Reporting
nav_order: 5
---

## GetPanelActivitySummaryReport

Returns the summary of the successfully started Surveys in the given date range.
>Please note: the date range is restricted to 30 days

### Route
```json
**GET** http://{IP_CORE_URL}/IntegratedPanelService/api/Reports/Surveys/PanelActivitySummary?SamplePartnerGUID={PartnerGUID}&StartDate={StartDate}&EndDate={EndDate}
```

### Request Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| PartnerGUID | ```Guid``` | API key provided by Toluna | Yes |
| StartDate | ```dateTime``` | UTC date/time at which report should begin. Format: YYYY-MM-DD HH:MM:SS | Yes |
| EndDate | ```dateTime``` | UTC date/time at which report should end. Format: YYYY-MM--DD HH:MM:SS | Yes |

### Response Body Details

| Name | Type | Desscription |
| :--- | :--- | :--- |
| PartnerGUID | ```GUID``` | Partner API key |
| CreatedUTC | ```dateTime``` | UTC date/time report created |
| StartSearchUTC | ```dateTime``` | UTC date/time start report |
| EndSearchUTC | ```dateTime``` | UTC date/time end report |
| Summary[] | ```array``` | List of statuses of successfully started Surveys |
| Summary[n].Status | ```string``` | Satus of the surveys. Result range: Qualified, QuotaFull, Terminated, Started, Abandoned, FraudTerminated, QualifiedIncomplete |
| Summary[n].StatusCount | ```int``` | Number of Surveys having designated "Summary[n].Status" |

### Possible Response Codes

| 200 | OK. Request processed normally; results returned without issue |
| 400 | {StartDate} must precede {EndDate} |
| 400 | Search date range cannot exceed 30 days |
| 400 | Could not find Partner for {PartnerGUID} |
| 500 | Internal Error. An exception occurred while processing the request. Toluna likely has details captured in its logs |

### Example Response
```json
{
  "Name": "SurveyTrackingSummary",
  "Description": "Shows Summary of Outcomes of all Surveys within a data range",
  "PartnerGUID": "b89268bf-5f68-470e-ac50-9ff6998cb93b",
  "CreatedUTC": "2017-11-01T18:04:27.2743459Z",
  "StartSearchUTC": "2017-02-23T21:54:03.16",
  "EndSearchUTC": "2017-03-15T21:54:03.16",
  "Summary": [
    {
    "Status": "Started",
    "StatusCount": 2
    },
    {
    "Status": "Terminated",
    "StatusCount": 3
    },
    {
    "Status": "Qualified",
    "StatusCount": 7
    },
    {
    "Status": "QuotaFull",
    "StatusCount": 1
    }
  ]
}
```