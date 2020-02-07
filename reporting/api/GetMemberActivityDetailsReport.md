---
title: GetMemberActivityDetailsReport
has_children: false
parent: Reporting
nav_order: 6
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

