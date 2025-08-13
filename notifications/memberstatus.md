---
title: Member Status
has_children: false
parent: Notifications
nav_order: 1
---

# Member Status Notifications
{: .no_toc }

These notifications are issued upon conclusion of a Partner Member’s experience with a Toluna Survey. Partners must consume them in order to understand the outcome of their Member’s invitation to the Survey. In general, they take two forms: Termination and Completion. Both are existing features of the Toluna IP System, and documentation regarding their details can be found in the standard integration guide. In addition to the information shown in the example below, ES partners also get ‘QuotaID’ in their notifications.

These notifications can be encrypted at the Partner's request. For more information on Toluna's encryption offering, click [here.](/memberrouting/encryption)

* TOC
{:toc}

---

# Completions

Toluna provides a real time automated completion service that notifies the partner upon a qualified
revenue generating survey completion by one of their members.

>Note: Completion notifications may be sent multiple times if the user refreshes the end page of the survey. Toluna will only mark the Survey complete once even in this case. If the Partner is paying incentives to the Respondent, Toluna recommends that the Partner programs to check for duplicate completion notification based on the SurveyID and UniqueCode passed.

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
| Revenue | ```int``` | Amount of Revenue in 1/100 of the currency units (eg 100=100 cents or $1 USD) |
| DateTime | ```string``` | Date and time of Respondent completion. Format "YYYY-MM-DD HH:MM:SS" in UTC Time |
| WaveId | ```int``` | Current iteration of the Survey. Studies related to one another can be sent in "waves" that the Member will experience as a unique Survey |
| QuotaID | ```int``` | (Applicable for Partners utilizing the [External Sample Offering](/externalsample/) only) Toluna's unique identifier for a quota |
| IncidenceRate | ```int``` | Incidence Rate of the Survey |
| AdditionalData | ```string``` | Full QueryString from the inviteURL. Custom parameters appended by the Partner to the inviteURL will also be included |
| IsAutoRouted | ```bool``` | Indcates whether the Member was auto-routed or not |
| OriginalSurveyID | ```int``` | SurveyID to which the Member was originally invited |


### Example XML Response
```xml
<confirmation xmlns:xsd="https://www.w3.org/2001/XMLSchema"xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance">
 <UniqueCode>myCode</UniqueCode>
 <SurveyId>99</SurveyID>
 <SurveyRef>mySurveyRef</SurveyRef>
 <Revenue>99</Revenue>
 <DateTime>2014-09-11 16:06:27</DateTime>
 <WaveId>100</WaveId>
 <QuotaID>987654</QuotaID>
 <IncidenceRate>50</IncidenceRate>
 <AdditionalData>clickid=1234</AdditionalData>
 <IsAutoRouted>true</IsAutoRouted>
 <OriginalSurveyID>100</OriginalSurveyID>
</confirmation>
```

### Example JSON Response
```plaintext
{
 "UniqueCode": "111",
 "SurveyId": 123,
 "SurveyRef": "123560-US",
 "Revenue": 100,
 "DateTime": "2014-09-11 16:06:27",
 "WaveId": 100,
 "QuotaID":987654,
 "IncidenceRate": 50,
 "AdditionalData": "clickid=1234",
 "IsAutoRouted": true,
 "OriginalSurveyID": 100
}
```

---

# Terminates

Toluna provides an automated termination service that notifies the Partner upon a non-qualified
Survey completion by one of their Members. Terminates and Quota Full notifications
are sent this way. This implementation on the partner end is not mandatory.

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
| QuotaID | ```int``` | (Applicable for Partners utilizing the [External Sample Offering](/externalsample/) only) Toluna's unique identifier for a quota |


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
"OriginalSurveyID": 100,
}
```
