---
title: End Pages
has_children: false
parent: Member Routing
nav_order: 1
---


# End Pages
{: .no_toc}

At the end of a Member's experience, Redirect URLs, commonly referred to as Webhooks, will be used to redirect the Member back to an end page specified by the Partner. The events requiring these URLs are enumerated and explained below.

---

* TOC
{:toc}

---

## Events

Toluna strongly recommends Partners supplying unique Redirect URLs for each of the events below to optimize the Member's experience.

### Max Survey Reached

Used when a Member has already completed the daily maximum number of Surveys allowed (25 Starts or 5 Completes per day).

### Qualified

Also known as "Qualified Complete." The Member has successfully completed the Survey and qualifies for a reward.

### No Surveys

There are no Surveys left available for the Member at this time or the member was not eligible to take the survey due to non-attribute related criteria.

### Terminated

The Member accessed the Survey but was screened out before completing.

### Quota Full

No further Panelists are needed to fulfill the Quota.

### Survey Taken

The Member attempted to access a Survey they have taken previously.

### No Cookies

The Member is not able to take the Survey because they have cookies disabled in their browser.

### Survey Not Available

The Member attempted to access a Survey that is no longer active.

### Not Qualified

The Member does not qualify for the invited Survey, often after the member has answered questions in the Prescreener survey.

### Fraud Terminate

The Member accessed the Survey but was screened out due to fraudulent behaviour.

---

## Routing Parameters

Toluna can return to the Partner any query string parameters they pass in when routing a member to a Survey. For example, if the Partner passes in “…toluna.com?di=1adsfadf&customParam=param123” in the invite URL, we can return “partnerendpage.com?customParam=param123.”

Additionally, Toluna can return the following value on the query string even if the Partner does not pass them in:

| Name | Type | Description |
| :--- | :--- | :--- |
| SurveyID | ```int``` | Toluna's identifier of a Survey |
| SurveyName | ```string``` | Toluna's name of Survey |
| WaveID | ```int``` | Toluna's identifier of the Wave |
| MemberCode | ```string``` | Member's unique identifier |

To facilitate any of these parameters, the Partner must provide these parameters in the URL structure, as presented in the below example:

https://thisisanexample.com/survey/complete?Source=toluna&completionStatus=5&**SurveyID=[SurveyID]&WaveID=[WaveID]&MemberCode=[MemberCode]&customParam=[customParam]**

## Enhanced Terminate Parameter

Upon opting in to [Enhanced Terminate Notifications](/general/changelog.html#620), the following parameter will also be included on non-Qualified end pages.

| Name | Type | Description |
| :--- | :--- | :--- |
| rejectionID | ```int``` | Toluna's unqiue identifier for a rejection. See [Rejection Types](/mapping/referencedataapi/rejectiontypes.html) for more details |