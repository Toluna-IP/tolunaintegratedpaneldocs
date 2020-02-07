---
title: Reporting API
has_children: false
parent: Reporting
nav_order: 1
---


# Reporting API Detail
{: .no_toc}

* TOC
{:toc}

---

## GetSurveyStatus

Returns status information for the request survey. Two options available: by ID Parameters or by Name Parameters.

### By ID Parameters

#### Route
```
**GET** http://{IP_CORE_URL}/IntegratedPanelService/api/Reports/Surveys/{SurveyID}/StatusByID/?SamplePartnerGuid={ParnerGUID}
```

#### Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| SurveyID | ```int``` | Toluna Internal SurveyID | Yes |
| PartnerGUID | ```GUID``` | API key provided by Toluna | Yes |

### By Name Parameters

#### Route
```
**GET** http://{PI_CORE_URL}/IntegratedPanelService/api/Reports/Survey/{SurveyName}/StatusByName/?SamplePartnerGUID={PartnerGUID}
```

#### Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| SurveyName | ```string``` | Toluna external Survey Name | Yes |

### Possible Response Codes

| Code | Etiology, actions |
| 200 | OK. Request processed normally; results returned without issue |
| 404 | Not Found. Could not find a Survey for the input |
| 500 | Internal Error. An exception occurred while processing the request. Toluna likey has details captured in its logs |

### Example Response
```json
{
 "Status": "CLOSED",
 "SurveyName": "1072552-BR",
 "SurveyID": 31033,
 “WaveID”: 247
}
```

---

## GetSurveyMemberStatusReport

For a given Survey, returns a list of all associated Members who, at a minimum, started the Survey.
>Please note: the date range is restricted to 30 days and this report does not produce data for clicks which were terminated before the Survey could be started.

### Route
```
**GET** http://{IP_CORE_URL}/IntergratedPanelService/api/Reports/Surveys/{SurveyName}/MemberStatus/?SamplePartnerGUID={PartnerGUID}&StartDate={StartDate}&EndDate={EndDate}
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

---

## GetMemberSurveyStatusReport

For a given Member, returns a list of all associated Survey responses.
>Please note: date range is restricted to 30 days

### Route
```json
**GET** http://{IP_CORE_URL}/IntegratedPanelService/api/Reports/Members/{Membercode}/SurveyStatus/?SamplePartnerGuid={PartnerGUID}&StartDate={StartDate}&EndDate={EndDate}
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

---

## GetMemberActivityDetailsReport

For a given Member and Survey, returns a list of Member responses tot he survey.

### Route
```
**GET** http://{IP_CORE_URL}/IntegratedPanelService/api/Reports/Surveys/{MemberCode}/{SurveyName}/ActivityDetails?SamplePartnerGuid={PartnerGUID}
```

### Request Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| PartnerGUID | ```Guid``` | API key provided by Toluna | Yes |
| MemberCode | ```string``` | Partner's unique identifier for Member | Yes |
| SurveyName | ```string``` | Unique name of Survey for which Member status report is required | Yes |
| WaveID | ```int``` | When supplied restricts report result to the SurveyName+WaveID combination and WaveID is returned in the result. to use, append "&WaveId={WaveID}" | No |

### Response Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| PartnerGUID | ```GUID``` | Partner API Key |
| MemberCode | ```string``` | Partner's unique identifier for Member |
| SurveyID | ```int``` | Toluna's unique identifier for Survey |
| SurveyName | ```string``` | Toluna's unique name for Survey |
| WaveID | ```int``` | Iteration of Survey; returned only when Panel is configured for WaveID use |
| CreatedUTC | ```dateTime``` | UTC date/time report created |
| MemberResponse[] | ```array``` | List of Member responses to the given Survey |
| MemberResponse[n].Status | ```string``` | The Member's last status with the Survey. Result range: Success, QuotaFull, SurveyOnHold, QuotaOnHold, SurveyClosed, SurveyNotFound, SurveyNotLive, SurveyTaken, MemberBlocked, DuplicateMember, RejectedOther, Abandoned |
| MemberResponse[n].EventDate | ```dateTime``` | Date/time of last status change |
| MemberResponse[n].ReferenceID | ```GUID``` | Toluna's identifier for Member's response to a Survey; useful for support tickets |

### Example Response
```json
{
  "Name": "MemberActivityDetailsReport",
  "Description": "Shows individual Member experience to the requested Survey",
   "PartnerGUID": "b89268bf-5f68-470e-ac50-9ff6998cb93b",
  "MemberCode": "1701440138",
  "SurveyID": 33217,
  "SurveyName": "1074437-US",
  "CreatedUTC": "2017-11-01T18:26:04.693398Z",
  "MemberResponse": [
    {
    "Status": "Success",
    "EventDate": "2017-10-02T21:50:58.113+00:00",
    "ReferenceID": "f50806ef-1bb7-49cc-a401-2c355534d091"
    },
    {
    "Status": "SurveyTaken",
    "EventDate": "2017-10-03T10:06:38.277+00:00",
    "ReferenceID": "d40cd8e0-b271-40a4-8671-8154bd41e973"
    },
    {
    "Status": "SurveyTaken",
    "EventDate": "2017-10-03T10:30:06.67+00:00",
    "ReferenceID": "53e31cca-26ec-46c8-bf44-53444f02cc4d"
    }
  ]
}
```


---

## GetPanelCompletesReport

Returns all completes generated by a panel in the given date range.
>Please note: the date range is restricted to 30 days.

### Route
```
**GET** http://{IP_CORE_URL}/IntegratedPanelService/api/Reports/Surveys/PanelCompletes?SamplePartnerGuid={PartnerGUID}&StartDate={StartDate}&EndDate+{EndDate}
```

### Request Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| SamplePartnerGUID | ```GUID``` | API key provided by Toluna | Yes |
| StartDate | ```dateTime``` | UTC date/time at which report should begin. Format: YYYY-MM-DD HH:MM:SS |
| EndDate | ```dateTime``` | UTC date/time at which report should end. Format: YYYY-MM-DD HH:MM:SS |

### Response Details

| Name | Type | Description |
| :--- | :--- | :--- |
| PartnerGUID | ```GUID``` | Partner API key |
| CreatedUTC | ```dateTime``` | UTC date/time report created |
| StartSearchUTC | ```dateTime``` | UTC date/time start report |
| EndSearchUTC | ```dateTime``` | UTC date/time end report |
| CompletesSummary[] | ```array``` | List of completes |
| CompletesSummary[n].SurveyID | ```int``` | Toluna Survey identifier |
| CompletesSummary[n].SurveyName | ```string``` | Toluna Survey name |
| CompletesSummary[n].WaveID | ```int``` | Current iteration of the Survey. Studies related to one another can be sent "Waves" that the Member experiences as unique Surveys |
| CompletesSummary[n].MemberCode | ```string``` | Unique Respondent Code from the Partner |
| CompletesSummary[n].EventDate | ```dateTime``` | date/time fo last change |
| CompletesSummary[n].AdditionalData | ```string``` | Query string parameters requested by the Partner |

### Possible Response Codes

| Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally; results returned without issue |
| 400 | {StartDate} must precede {EndDate} |
| 400 | Search date range cannot exceed 30 days |
| 400 | Could not find Partner for {PartnerGUID} |
| 500 | Internal Error. An exception occurred while processing the request. Toluna likely has details captured in its logs |

### Example Response
```
{
  "Name": "PanelCompletesReport",
  "Description": "Shows the list of completes for a panel in the provided date range",
  "PartnerGUID": "b89268bf-5f68-470e-ac50-9ff6998cb93b",
  "CreatedUTC": "2018-01-23T17:28:19.157403Z",
  "StartSearchUTC": "2017-10-01T00:00:00",
  "EndSearchUTC": "2017-10-03T00:00:00",
  "CompletesSummary": [
    {
    "SurveyID": 36326,
    "SurveyName": "1074978-US-3",
    "WaveID": 0,
    "MemberCode": "1701440138",
    "EventDate": "2017-10-02T15:29:46.573",
    "AdditionalData": “clickid=123”
    },
    {
    "SurveyID": 36326,
    "SurveyName": "1074978-US-3",
    "WaveID": 0,
    "MemberCode": "1701440138",
    "EventDate": "2017-10-02T15:29:46.573",
    "AdditionalData": “clickid=124”
    }
  ]
}
```