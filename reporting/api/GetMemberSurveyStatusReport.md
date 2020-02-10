---
title: GetMemberSurveyStatusReport
has_children: false
parent: Reporting API
grand_parent: Reporting
nav_order: 4
---

## GetMemberSurveyStatusReport

For a given Member, returns a list of all associated Survey responses.
>Please note: date range is restricted to 30 days

### Route
```json
GET http://{IP_CORE_URL}/IntegratedPanelService/api/Reports/Members/{Membercode}/SurveyStatus/?SamplePartnerGuid={PartnerGUID}&StartDate={StartDate}&EndDate={EndDate}
```

### Request Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| MemberCode | ```string``` | Partner's unique identifier for Member | Yes |
| PartnerGUID | ```GUID``` | API key provided by Toluna | Yes |
| StartDate | ```dateTime``` | UTC Date/Time at which report should begin. Format: YYYY-MM-DD HH:MM:SS | Yes |
| EndDate | ```dateTime``` | UTC Date/Time at which report should end. Format: YYYY-MM-DD HH:MM:SS | Yes |

### Response Body Details 

| Name | Type | Description |
| :--- | :--- | :--- |
| PartnerGUID | ```GUID``` | Partner API key |
| CreatedUTC | ```dateTime``` | UTC Date/Time Report created |
| StartSearchUTC | ```dateTime``` | UTC Date/Time start Report |
| EndSearchUTC | ```dateTime``` | UTC Date/Time end Report |
| Details[] | ```array``` | List of Members reporting a status for the Survey |
| Details[n].SurveyID | ```int``` | Toluna unique identifier for Survey |
| Details[n].WaveID | ```int``` | Iteration of Survey. Returned only when Panel is configured for WaveID use |
| Details[n].SurveyName | ```string``` | Toluna's unique name for Survey | 
| Details[n].Status | ```string``` | The Member's last status with the Survey. Result range: Started, Abandoned, Terminated, FraudTerminated, PrescreenerQualified, Qualified, QuotaFull |
| Details[n].EventDate | ```dateTime``` | Date/Time of last status change |
| Details[n].ReferenceID | GUID | Toluna's identifier for Member's response to a Survey; useful for support tickets |

### Possible Response Code

| Code | Etiology, actions |
| :--- | :--- | 
| 200 | OK. Request processed normally, resulsts returned without issue |
| 404 | Not Found. Could not find a survey for the SurveyName |
| 400 | {StartDate} must precede {EndDate} |
| 400 | Search date range cannot exceed 30 days |
| 400 | Could not find Partner for the PartnerGUID |
| 500 | Internal Error. An exception occurred while processing the request. Toluna will likely have details capture in its logs |

### Example Response
```json
{
    "Name": "MemberSurveyStatusReport",
    "Description": "Shows Member Responses to all Surveys within a data range",
    "PartnerGUID": "XXaebd22-1d08-4209-ac17-449XX8c805a0",
    "MemberCode": "198433088",
    "CreatedUTC": "2016-01-29T16:17:13.9234034Z",
    "StartSearchUTC": "2016-01-01T00:00:00",
    "EndSearchUTC": "2016-01-30T00:00:00",
    "Details": [
   {
    "SurveyID": 110072,
    "Status": "Qualified",
    "EventDate": "2014-10-21T20:16:37.333+00:00",
    "ReferenceID": 730153,
    “WaveId”: 4584
     },
    {
    "SurveyID": 110072,
    "Status": "Started",
    "EventDate": "2014-10-21T21:08:32.753+00:00",
     "ReferenceID": 730154,
    “WaveId”: 4588
    }
  ]
}
```
