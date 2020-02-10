---
title: Member Status
has_children: false
parent: Notifications
nav_order: 1
---

# Member Status Notifications
{: .no_toc }

* TOC
{:toc}

---

## Introduction

These notifications are issued upon conclusion of a Partner Member’s experience with a Toluna Survey. Partners must consume them in order to understand the outcome of their Member’s invitation to the Survey. In general, they take two forms: Termination and Completion. Both are existing features of the Toluna IP System, and documentation regarding their details can be found in the standard integration guide. ES partners also get ‘QuotaID’ in their notifications.

---

# Completions

Toluna provides a real time automated completion service that notifies the partner upon a qualified
revenue generating survey completion by one of their members.

>Note: Completion notifications may be sent multiple times if the user refreshes the end page of the survey. Toluna will only mark the Survey complete once even in this case. If the Partner is paying incentives to the Respondent, Toluna recommends that the Partner programs to check for duplicate completion notification based on the SurveyID and UniqueCode passed.

### Route
```
POST http://myPartnerApi/TolunaComplete
```

### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| UniqueCode | ```string``` | Unique Respondent Code from the Partner |
| SurveyID | ```int``` | Tolujna Survey identifier |
| SurveyRef | ```string``` | Toluna Survey name |
| Revenue | ```int``` | Amount of Revenue in 1/100 of the currency units (eg 100=100 cents or $1 USD) |
| DateTime | ```string``` | Date and time of Respondent completion. Format "YYYY-MM-DD HH:MM:SS" in UTC Time |
| WaveiD | ```int``` | Current iteration of the Survey. Studies related to one another can be sent in "waves" that the Member will experience as a unique Survey |
| Incidence Rate | ```int``` | Incidence Rate of the Survey |
| AdditionalData | ```string``` | Query string argument in the completion URL with its data replaced |
| IsAutoReouted | ```bool``` | Indcates whether the Member was auto-routed or not |
| OriginalSurveyID | ```int``` | SurveyID to which the Member was originally invited |

>Note: v2.1 requires Partners to opt-in to WaveID feature; it will not appear by default

### Example XML Response
```xml
<confirmation xmlns:xsd="http://www.w3.org/2001/XMLSchema"xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <UniqueCode>myCode</UniqueCode>
 <SurveyId>99</SurveyId>
 <SurveyRef>mySurveyRef</SurveyRef>
 <Revenue>99</Revenue>
 <DateTime>2014-09-11 16:06:27</DateTime>
 <WaveId>100</WaveId>
 <IncidenceRate>50</IncidenceRate>
 <AdditionalData>clickid=1234</AdditionalData>
 <IsAutoRouted>true</IsAutoRouted>
 <OriginalSurveyID>100</OriginalSurveyID>
</confirmation>
```

### Example JSON Response
```json
{
 "UniqueCode": "111",
 "SurveyId": 123,
 "SurveyRef": "123560-US",
 "Revenue": 100,
 "DateTime": "2014-09-11 16:06:27",
 "WaveId": 100,
 "IncidenceRate": 50,
 "AdditionalData": "clickid=1234",
 "IsAutoRouted": true,
 "OriginalSurveyID": 100
}
```

---

# Terminates

Toluna provides an automated termination service that notifies the Partner upon a non-qualified
Survey completion by one of their Members. Terminates, Quota Full, No Survey Available notifications
are sent this way. This implementation on the partner end is not mandatory.

### Route
```
POST http://myPartnerAPI/TolunaTerminate
```

### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| UniqueCode | ```string``` | Unique Respondent Code from the Partner |
| SurveyID | ```int``` | Tolujna Survey identifier |
| SurveyRef | ```string``` | Toluna Survey name |
| Reason | ```string``` | Reason for the Termination. Possible values: "QuotaFull," "SurveyTaken," "Terminated," "SurveyNotAvailable," "NoSurveysAvailable," "NoCookie," "MaxSurveysReached," or "NotQualified" |
| DateTime | ```string``` | Date and time of Respondent Termination. Format "YYYY-MM-DD HH:MM:SS" in UTC Time |
| WaveiD | ```int``` | Current iteration of the Survey. Studies related to one another can be sent in "waves" that the Member will experience as a unique Survey |
| Incidence Rate | ```int``` | Incidence Rate of the Survey |
| AdditionalData | ```string``` | Query string argument in the completion URL with its data replaced |
| IsAutoReouted | ```bool``` | Indcates whether the Member was auto-routed or not |
| OriginalSurveyID | ```int``` | SurveyID to which the Member was originally invited |

>Note: v2.1 requires Partners to opt-in to WaveID feature; it will not appear by default

### Example XML Termination
```xml
<?xml version="1.0"?>
<termination xmlns:xsd="http://www.w3.org/2001/XMLSchema"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <UniqueCode>111</UniqueCode>
 <SurveyId>123</SurveyId>
 <SurveyRef>123560-US</SurveyRef>
 <DateTime>2014-09-11 16:06:27</DateTime>
 <Reason>Terminated</Reason>
 <WaveId>100</WaveId>
 <AdditionalData>clickid=1234</AdditionalData>
<IsAutoRouted>true</IsAutoRouted>
<OriginalSurveyID>100</OriginalSurveyID>
</termination>
```

### Example JSON Termination
```json
{
 "UniqueCode": "111",
 "SurveyId": 123,
 "SurveyRef": "123560-US",
 "Reason": "Terminated",
 "DateTime": "2014-09-11 16:06:27",
 "WaveId": 100,
 "AdditionalData": "clickid=1234",
"IsAutoRouted": true,
"OriginalSurveyID": 100
}
```
