---
title: Enhanced Terminate Notifications
has_children: false
parent: Notifications
nav_order: 2
---


# Enhanced Terminate Notifications
{: .no_toc}

In certain instances, Members will click on a Survey invite but the experience will be Terminated before the Member is routed through the Toluna Platform. These instances can occur for multiple reasons (e.g. the Member attempted to initiate the experience after the Survey or Invite Link has expired). 

Since the Member does not start the Survey experience before they are Terminated, these notifications are also referred to as "Pre-Start" Notifications, and are executed in similar fashion as the Terminate notifications, details on which can be found [here](/notifications/memberstatus.html#terminates).

* TOC
{:toc}


### HTTP Verb

- POST

### Route(s)

- Specified by Partner; Toluna will configure accordingly

### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| UniqueCode | ```string``` | Unique Respondent Code from the Partner |
| SurveyId | ```int``` | Tolujna Survey identifier |
| SurveyRef | ```string``` | Toluna Survey name |
| Reason | ```string``` | Reason for the Termination. Possible values: "QuotaFull," "SurveyTaken," "Terminated," "SurveyNotAvailable," "NoSurveysAvailable," "NoCookie," "MaxSurveysReached," or "NotQualified" |
| DateTime | ```string``` | Date and time of Respondent Termination. Format "YYYY-MM-DD HH:MM:SS" in UTC Time |
| WaveId | ```int``` | Current iteration of the Survey. Studies related to one another can be sent in "waves" that the Member will experience as a unique Survey |
| IncidenceRate | ```int``` | Incidence Rate of the Survey |
| AdditionalData | ```string``` | Full QueryString from the inviteURL. Custom parameters appended by the Partner to the inviteURL will also be included |
| IsAutoRouted | ```bool``` | Indcates whether the Member was auto-routed or not |
| OriginalSurveyID | ```int``` | SurveyID to which the Member was originally invited |
| RejectionID | ```int``` | Toluna's unqiue identifier for a rejection. See [Respondent Rejection Types](/mapping/referencedataapi/rejectiontypes.html) for mapping details |
| RejectionName | ```string``` | Name of a rejection. See [Respondent Rejection Types](/mapping/referencedataapi/rejectiontypes.html) for mapping details |
| QuotaID | ```int``` | (Applicable for Partners utilizing the [External Sample Offering](/externalsample/) only) Toluna's unique identifier for a quota |

> Please note: To prevent breaking changes, panels existing before June 20, 2021, have been excluded from receiving RespondentRejectionTypeID and RejectionName. If you have a panel that predates these additions and would like to enable them, please contact your Toluna Representative.

### Example XML Termination
```xml
<?xml version="1.0"?>
<termination xmlns:xsd="https://www.w3.org/2001/XMLSchema"
xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance">
 <UniqueCode>111</UniqueCode>
 <SurveyId>123</SurveyId>
 <SurveyRef>123560-US</SurveyRef>
 <DateTime>2014-09-11 16:06:27</DateTime>
 <Reason>Terminated</Reason>
 <WaveId>100</WaveId>
 <QuotaID>987654</QuotaID>
 <AdditionalData>clickid=1234</AdditionalData>
<IsAutoRouted>true</IsAutoRouted>
<OriginalSurveyID>100</OriginalSurveyID>
<RespondentRejectionTypeID>57</RespondentRejectionTypeID>
<RejectionName>AccountGroupSurveyTaken</RejectionName>
</termination>
```

### Example JSON Termination
```plaintext
{
 "UniqueCode": "111",
 "SurveyId": 123,
 "SurveyRef": "123560-US",
 "Reason": "Terminated",
 "DateTime": "2014-09-11 16:06:27",
 "WaveId": 100,
 "QuotaID": 987654,
 "AdditionalData": "clickid=1234",
"IsAutoRouted": true,
"OriginalSurveyId": 100,
"RespondentRejectionTypeID": 103,
"RejectionName": "NonQuotaDemographicRejection"
}
```

