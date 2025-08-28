---
title: Best Practices
has_children: false
parent: General
nav_order: 5
---

# Best Practices to Improve Click-to-Conversion Rates and Respondent Survey Experience
{: .no_toc}

Toluna recognizes the importance of continuous improvement and excellence, and we want to support Partners in maximizing their performance and achieving outstanding results. To this end, we have compiled a comprehensive list of best practices which are designed to help Partners optimize their integration. By adopting these best practices, Partners will be better equipped to navigate challenges and enhance their overall performance.

These guidelines specifically focus on Survey Rejections and Survey Terminations. By
applying the following suggestions, can optimize their traffic and enhance their Members' survey experience.

* TOC
{:toc}

## Pre-Start Rejections

These statuses correlate with [Respondent Rejection Types](/mapping/referencedataapi/rejectiontypes.html) and are provided by Toluna automatically if the Partner is configured to receive [Enhanced Terminate Notification](/notifications/etns.html).

### DeviceTypeIDNotSupportForSurvey

This Rejection correlates with RespondentRejectionTypeID 96.

These Rejections occur when there is a mismatch between the device used by the Member and the devices supported by the Survey. To avoid these Rejections, ensure only Members that use a device supported by the Survey are invited to it.

- External Sampling: Partners can use the device user agent or other means to determine which device the Member is using and make sure that the device type is found in the DeviceTypeIds section from the [Survey object](/externalsample/api/getquotas.html#survey-object). The DeviceTypeIDs section from the Survey object specifies which devices are supported by the Survey.
- Dashboard: Partners can use the device user agent or other means to determine which device the Member is using and then specify the device type parameter in the [GetSurveys API request](/dashboard/api/getsurveys.html).

### ExcludedSurveyTaken

This Rejection correlates with RespondentRejectionTypeID 23.

These Rejections occur when the Member is invited to a Survey from which they’re excluded based on a previous Survey participation. To avoid these Rejections, the Partner's system should check the [SurveyWaveExclusions](/externalsample/api/surveyexclusion.html) from the Survey object within the [GetQuotas API response](/externalsample/api/getquotas.html). Partners integrated with the Dashboard API should not see such Rejections since the sampling part is done on Toluna’s side

### VerificationFailed

This Rejection correlates with RespondentRejectionTypeIDs 97 and 98.

The Toluna system rejects respondents with an IPQS fraud score >=90. There are other parameters that Toluna's system takes into account, but these Rejections can also be reduced by not inviting Members with an IPQS fraud score >=90. It is recommended that Partners to implement industry-standard solutions such as IPQualityScore or Research Defender to determine a Member's fraud score.

### IncorrectRespondentCountry

This Rejection correlates with RespondentRejectionTypeID 70.

During pre-survey checks, Toluna's system will reject any Member that is in a different country than the one targeted by the Survey. The specified country for a Survey can be determined by the Culture associated with the PanelGuid used by the Partner. These Rejections can be reduced by checking the location of the Member's IP before generating a Survey invite for them.

### MaxDailySurveys

This Rejection correlates with RespondentRejectionTypeID 2.

Toluna has a threshold of 5 completes or 25 starts per day (UTC). Once a Member reaches that threshold, any further attempt from that Member will be rejected.

### QuotaOnHold

This Rejection correlates with RespondentRejectionTypeID 11.

This Rejection occurs when the Member is invited to a Quota that is on hold. To avoid such Rejections, Toluna recommend Partners to call the [GetQuotas endpoint](/externalsample/api/getquotas.html) every 1 minute. This will ensure that Partners are seeing a fresh Survey inventory. Calling the GetQuotas
endpoint every less frequently might expose the Partner to Surveys that already reached their Quota size and are no longer in need of traffic. 

Likewise, enabling and processing the [Quota](/notifications/quotastatus.html)/[Survey](/notifications/surveyclosed.html) notifications can help Partners decide which Surveys they should stop exposing. Furthermore, reducing the time elapsed between generating the Survey invite and the click should help reduce these Rejections. This approach is applicable to Partners integrated with the [Dashboard Offering](/dashboard/index.html) as well. Implementing the aforementioned suggestions will also help to reduce other Rejection types such as SurveyClosed, SurveyNotLive, SurveyOnHold.

### RestartNotAllowed

This Rejection correlates with RespondentRejectionTypeID 10.

To reduce these Rejections, it is important to remove the Survey link from a Member that has already accessed it.

### SubQuotaFull

This Rejection correlates with RespondentRejectionTypeIDs 19 and 163.

By taking into account the MaxTargetCompletes and CurrentCompletes from the [SubQuota object](/externalsample/api/getquotas.html#subquota) in the GetQuotas API response, Partners can decide how much traffic should be sent to a certain Quota. Calling the GetQuotas endpoint more frequently will also allow Partners to see updated details regarding the Survey.

### Survey Taken

This Rejection correlates with RespondentRejectionTypeID 4.

This occurs when a Member clicks on an invite link that has already been used and an end status was registered for the Member (the Member finished the Survey to some capacity). Partners should ensure their system removes the invite link / makes it unavailable after the Member initially clicks on it.

### Not Qualified

This Rejection correlates with RespondentRejectionTypeIDs 14, 123, and 124.

These Rejections occur whenever a Member is invited to a Survey for which they’re not qualified. These Members are rejected after going through the Prescreener. To reduce these Rejections, the Partner should add as many attributes as possible to a Member's profile before inviting them to a Survey. 

The [ReferenceData API](/mapping/referencedataapi/index.html) can be used to view information on attributes that may be used for Quota targeting. Toluna also publishes quarterly reports showing the most requested attributes. Those can be found [here](https://drive.google.com/drive/u/1/folders/1MsAUeldUTmWqYlTrfhf-1EFSGWTSlkJN). 

## In-Survey Terminations

### Fraud Terminate

These Terminations occur when a Member's activity within a Survey is determined as fraudulent. To help reduce these Terminations, Toluna suggests implementing more quality checks such as:
- Attention and speeding checks
- Behavioural checks for honesty or bias
- Representativity checks
- Straightlining checks
- Open-ended (OE) checks (grammar analysis, OE repetition,genuineness, AI/bot-like detection)
- IP checks (IPQS/ Research Defender)
- Device checks
- Email domain checks 
- Browser version checks
- OS checks
- Timezone checks

Toluna also suggests excluding Members access Surveys with VPNs.

### QuotaFull

These Terminations can be reduced by implementing the same logic as with the [QuotaOnHold Pre-Survey Rejections](/general/bestpractices.html#quotaonhold). Additionally, checking the CompletesRequired and EstimatedCompletesRemaining sections from the [Survey object](/externalsample/api/getquotas.html#survey-object) can help Partners decide how much traffic to send to a certain Quota.