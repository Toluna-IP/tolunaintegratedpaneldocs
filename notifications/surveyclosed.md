---
title: Survey Notification
has_children: false
parent: Notifications
nav_order: 4
---


# Survey Closed Notifications 
{: .no_toc }

Toluna provides a notification service to alert the partner when a survey closes. This helps the partner to manage the panelist experience by preventing the panelist from attempting to enter a survey that is no longer available.

* TOC
{:toc}

---

## Route
```plaintext
POST https://myPartnerApi/TolunaNotify
```
### HTTP Verb

- POST

### Route(s)

- Specified by Partner; Toluna will configure accordingly

## Notification Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| SurveyID | ```int``` | Tuluna Survey identifier |
| SurveyRef | ```string``` | Toluna Survey name |
| Status | ```string``` | Toluna Survey status - Always "Closed" |
| DateTime | ```string``` | Date and time the Survey was closed. Format "YYYY-MM-DD HH:MM:SS" in UTC Time |
| WaveId | ```int``` | Current iteration of the survey. Studies related to one another can be sent in “waves” that the Member experiences as unique surveys. SurveyID+WaveID will always be unique |


### Example XML Notification
```xml
<?xml version="1.0"?>
<survey xmlns:xsd="https://www.w3.org/2001/XMLSchema"
xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance">
   <SurveyId>99</SurveyId>
   <SurveyRef>123560-US</SurveyRef>
   <Status>Closed</Status>
   <DateTime>2014-09-11 16:06:27</DateTime>
   <WaveId>100</WaveId>
</survey>
```

### Example JSON Notification
```plaintext
{
 "SurveyID": 99,
 "SurveyRef": "123560-US",
 "Status": "Closed",
 "DateTime": "2014-09-11 16:06:27",
 "WaveId": 100
}
```
