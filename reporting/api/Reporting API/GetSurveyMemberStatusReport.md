---
title: GetSurveyMemberStatusReport
has_children: false
parent: Reporting
nav_order: 3
---

## GetSurveyMemberStatusReport

For a given Survey, returns a list of all associated Members who, at a minimum, started the Survey.
>Please note: the date range is restricted to 30 days and this report does not produce data for clicks which were terminated before the Survey could be started.

### Route
```
GET http://{IP_CORE_URL}/IntergratedPanelService/api/Reports/Surveys/{SurveyName}/MemberStatus/?SamplePartnerGUID={PartnerGUID}&StartDate={StartDate}&EndDate={EndDate}
```

### Request Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| SurveyName | ```string``` | Unique name of a Survey for which Member status report is required | Yes |
| PartnerGUID | ```GUID``` | API Key provided by Toluna | Yes |
| StartDate | ```dateTime``` | UTC Date/Time at which report should begin. Format: YYYY-MM-DD HH:MM:SS | Yes |
| EndDate | ```dateTime``` | UTC Date/Time at which report should end. Format: YYYY-MM-DD HH:MM:SS | Yes |
| WaveID | ```int``` | Restricts report results to the SurveyName+WaveID combination and WaveID is returned in the result. To use, append "&WaveID={WaveID}" to the request | No |

### Response Body Details 

| Name | Type | Description |
| :--- | :--- | :--- |
| PartnerGUID | ```GUID``` | Partner API key |
| SurveyID | ```int``` | Toluna unique identifier for Survey |
| SurveyName | ```string``` | Toluna unique name for Survey |
| CreatedUTC | ```dateTime``` | UTC Date/Time Report created |
| StartSearchUTC | ```dateTime``` | UTC Date/Time start Report |
| EndSearchUTC | ```dateTime``` | UTC Date/Time end Report |
| WaveID | ```int``` | Iteration of Survey; returned only when requested and Panel is configured for WaveID use |
| Details[] | ```array``` | List of Members reporting a status for the Survey |
| Details[n].MemberCode | ```string``` | Partners unique identifier for Member |
| Details[n].Status | ```string``` | the Member's last status with the Survey. Result range: Started, Abandoned, Terminated, FraudTerminated, PrescreenerQualified, Qualified, QuotaFull |
| Details[n].EventDate | ```dateTime``` | Date/Time of last status change |
| Details[n].ReferenceID | ```GUID``` | Toluna's identifier for Member's response to a Survey; useful for support tickets |

### Possible Response Code

| Code | Etiology, actions |
| :--- | :--- | 
| 200 | OK. Request processed normally, resulsts returned without issue |
| 404 | Not Found. Could not find a survey for the SurveyName |
| 400 | {StartDate} must precede {EndDate} |
| 400 | Search date range cannot exceed 30 days |
| 400 | Could not find Partner for the PartnerGUID |
| 500 | Internal Error. An exception occurred while processing the request. Toluna will likely have details capture in its logs |
| 400 | "WaveID" is included and the Panel has not yet been configured to use WaveID |

### Example Response
```json
{
    "Name": "SurveyMemberStatusReport",
    "Description": "Shows Member responses to the requested Survey",
    "PartnerGUID": "XXaebd22-1d08-4209-ac17-449XX8c805a0",
    "SurveyID": 110072,
    "WaveId": 324567,
    "SurveyName": "1150122-US-CBG11",
    "CreatedUTC": "2016-01-29T16:17:13.9234034Z",
    "StartSearchUTC": "2016-01-01T00:00:00",
    "EndSearchUTC": "2016-01-30T00:00:00",
    "Details": [
    {
     "MemberCode": "160784820",
     "Status": "QuotaFull",
     "EventDate": "2014-10-21T15:17:04.09-04:00",
     "ReferenceID": ‘4898681E-C781-45D2-A0ED-B83D2D3C10E8’
    },
    {
     "MemberCode": "198433088",
     "Status": "Qualified",
     "EventDate": "2014-10-21T16:16:37.333-04:00",
     "ReferenceID": ‘D202AF3C-0A75-4A76-94DA-389F16F1F979’
     },
     {
     "MemberCode": "198433088",
     "Status": "Started",
     "EventDate": "2014-10-21T17:08:32.753-04:00",
     "ReferenceID": ‘08D65758-2E36-4185-850B-B307F2C51590’
    },
    {
     "MemberCode": "1378711522",
     "Status": "Terminated",
     "EventDate": "2014-10-21T17:15:04.977-04:00",
     "ReferenceID": ‘9C2D16A9-D036-4858-A84F-6E32B7FEDF1D’
    }
    ]
}
```