---
title: Pre-Start
has_children: false
parent: Notifications
nav_order: 999
---


# Pre-Start Notifications 
{: .no_toc}

In certain instances, Members will click on a Survey invite but the experience will be Terminated before the Member is routed through the Toluna Platform. These instances can occur for multiple reasons (e.g. the Member attempted to initiate the experience after the Survey or Invite Link has expired). 

Since the Member does not start the Survey experience before they are Terminated, these notifications are call "Pre-Start" Notifications, and are executed in similar fashion as the Terminates notifications, details on which can be found [here](/notifications/memberstatus.html#terminates).

* TOC
{:toc}


## Route

 - None


## Body Details

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


## Example XML Pre-Start 

Pre-start notifications are only available in JSON format.


## Example JSON Pre-Start
```plaintext
{
 "UniqueCode": "111",
 "SurveyId": 123,
 "SurveyRef": "123560-US",
 "Reason": "QuotaFull",
 "DateTime": "2014-09-11 16:06:27",
 "WaveId": 100,
 "AdditionalData": "clickid=1234",
"IsAutoRouted": true,
"OriginalSurveyID": 100
}
```
