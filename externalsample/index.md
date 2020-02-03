---
title: External Sample
has_children: true
nav_order: 2
---

# External Sample 

## Introduction

### What is External Sample?

Toluna’s “External Sample” (ES) capability is an integration option offered as part of the Integrated Panel program. Its adoption permits the Partner to receive near real-time details about Toluna’s open quotas. Once obtained, Partners can use their own sampling capabilities to target the most appropriate respondents. This differs from the traditional IP model where Toluna maintains complete control over the sampling, routing, and invitation processes.

Internally at Toluna, the existing IP Framework views ES as simply another option for getting survey invitations into the hands of its Partners. As such, Partners choosing to adopt this capability requires only a few additional integration points beyond the traditional model.

### What is the Flow?

Within the realms of the ES Offering, there are two kinds of Quotas Toluna uses with its Partners. The first is the Standard Quota, similar to our traditional offerings, but with ES-specific parameters. The second kind is the Recontact Quota, the definition of which will be explained further below, along with the Quota-specific flow.


#### "Recontact" Flow

At times, Tluna will seek to "reconnect" specific Members for a Quoa. Typically this is done to facilitate follow-up information for an original study. Since the target Members are already known, the partner has not requirement to sample its membership for the Quota. Instead, they query a Toluna API which will return the list of MemberCodes applicable for recontact. Once Obtained, the Partner should saple the list against the Recontact Quota to validate the targeting and generate an invite request for each match. From here, the process is identical to the interaction with a typical Quota.


#### How is ES Different than other offerings?

*To Do*


#### What is needed to integrate?

These are the additional points needed to achieve the full IP integration:

- *Get Quotas from Toluna*
  - Call the "GetQuotas" route for an inventory of current, open Quotas.
- *Once Member is Sampled for Quota, Get Invite From Toluna*
  - Provide some basic information and receive an invite from Toluna for your Member
- *Create API to Receive Quota Status Notifications from Toluna*
  - Toluna will broadcast changes to its Quotas. Subscrube by establishing an API to handle these events.
  - >Please note: you will receive status changes for all open Quotas, not just those with which you are engaged.


## Notification / Webhooks

This describes several support processes Toluna will operate in the background of an ES integration.

### Member Status Link

When a Partner's Member has completed interaction with a Toluna Survey, Toluna will deliver a notification signifying this even and its details. For the most part, these are identical to the "real-time" notifications described in the [Main Integration Guide](*To do*).

{: .label .label-red }
Suscription to these notifications is mandatory for ES Partners.

### Quota Status Link

When a Quota is no longer available or a previously on-hold Quota becomes available/live, Toluna will broadcast this information to its Partners.

{: .label .label-red }
Suscription to these notifications is mandatory for ES Partners.

> Please note: Subscribers will receive updates for all Quotas, not just those with which they are engaged. Partners should integrate in a manner in which non-relevant Quota updates are ignored.

## Sampling Rules

External Sample Partners must comply with Toluna's samplingrules. To be sampled for a Quota, each member must:
 - Be targted for only 1 Quota per Survey
 - Match ALL Layers in the Quota
 - Match ONE of the SubQuotas
 - Match at least one "AnswerID" (SubQuotaAttribute) per SubQuota with the single QuestionID
 - Match at least one "AnswerID" (SubQuotaAttribute) per QuestionID in the SubQuota with multiple QuestionIDs
 
These rules can be consolidated into simple boolean conditions:
 - Quotas are "OR" conditions
 - Layers are "AND" conditions
 - SubQuotas are "OR" conditions
 - AnswerIDs are "OR" conditions
 - Within a SubQuota
   - "OR" for the same QuestionID
   - "AND" for multiple QuestionIDs

**Example Quotas**

[Example Quota with Multiple Layers](){: .btn }

[Example Quota with Single Layer, SubQuota with Multple QuestionIDs](){: .btn }

[Example Quota with Single lyaer, SubQuota with Single QuestionIDs](){: .btn}

## API Documentation


### "Bad Request" Response Codes

| Result | ResultCode | Description |
| :--- | :--- | :--- |
| PANEL_DOES_NOT_EXIST | 3 | The requested "PanelGUID" could not be found |
| PANEL_NOT_ES_ENABLED | 4 | The requested panel is not enabled for External Sampling |
| SURVEY_DOES_NOT_EXIST | 5 | The Survey to which the Quota belongs no longer exists |
| SURVEY_NOT_FOR_RECONTACT | 6 | The Survey to which the Quota belongs is not enabled for Recontact | 
| QUOTA_NOT_ES_ENABLED | 8 | The requested Quota is not enabled for External Sampling. |
| QUOTA_NOT_LIVE | 9 | The requested Quota is not live |
| NO_QUOTA_ID | 10 | The requested QuotaID could not be found |
| NO_MEMBER_FOUND | 12 | The requested MemberCode could not be found |
| MEMBER_NOT_ROUTABLE | 13 | The requested MemberCode is not in a state eligible for routing to a Quota |
| MEMBER_BLOCKED | 14 | The requested MemberCode is currently blocked from taking Surveys. Contact your Toluna representative for details |
| SURVEY_NOT_ENABLED_FOR_IP_ES | 15 | The Survey to which the Quota belongs is not enabled for Integrated Panel External Sample use. |
| MEMBER_DOES_NOT_MATCH_QUOTA | 16 | The requested MemberCode does not match the requested QuotaID |
| NO_RECONTACT_GID | 17 | A request for a Recontact Invite could not be fulfilled due to missing information from the Survey's sponsor |
| PANEL_INVALID_ES_REQUEST | 20 | The requested panel is not configured to ES-based invitations to Toluna Quotas |
| NON_QUOTA_DEMOGRAPHIC_REJECTION | 21 | The request to get an Invite is rejected due to non-quota demographic reasons. Examples: Prior participation in Quota, Device Type Mismatch, etc |
| MEMBER_NOT_ACTIVE | 22 | The member is not active in the Toluna system. This can be due to several reasons. Examples: Suspended User, BlockedForAbuse. Contact your Toluna representative for details |
| SURVEY_STUDY_TYPE_EXCLUDED | 23 | Panel has been configured to exclude any Survey containing the Study Type. |
| SURVEY_CUSTOMER_EXCLUDED | 24 | Panel has been configured to exclude any Survey hosted by the Customer |
| SURVEY_EXCLUDED | 25 | Partner is excluded from participation in this Surve |
| ACCOUNT_GROUP_SURVEY_TAKEN | 26 | The requested Member has already taken the survey, possibly from another account |
| INTERVALLIC_QUOTA_NOTAVAILBLE | 27 | Information about a rollover Quota is not currently availabl |
| QUOTA_FULL | 28 | Requested Quota is Ful |
| IP_EXTERNAL_RESPONDENTTYPE_FULL | 29 | The allotted completes for External Sample are full |
| EXCLUDED_SURVEY_TAKEN | 30 | Member has been excluded from the Survey. See Toluna respresentative for details |
| DEVICETYPE_NOT_SUPPORTED_FOR_SURVEY | 31 | The requested device types are not available for the Surve |
| SURVEY_LOI_MISMATCH | 32 | The requested LOI is higher than the Survey’s upper limit |
| IP_PROVIDER_COST_NOMATCH | 33 | Partner price is higher than the current limit on the Survey |
| SURVEY_VERIFICATION_LEVEL_FAILED | 34 | The Member’s verification score is lower than what the Survey requires |
| PREVIOUSLY_TERMINATED_SCREENER | 35 | The member has terminated on a TQS prescreener in a previous wave of a tracker survey |
| TECHNICAL_ERROR | 36 | A system error occurred, Toluna likely has captured details in its logs |
| UNABLE_TO_GET_GID | 37 | For a Recontact Survey, Toluna is unable to find the recontact member identifier |
| SURVEY_TAKEN | 38 | The member has already taken the requested Survey |
| MAX_DAILY_EXCEEDED | 39 | The member has exceeded the daily limit of Surveys |
| MAX_WEEKLY_EXCEEDED | 40 | The member has exceeded the weekly limit of Surveys |


## Notifications

In order to complete the ES Integrated experience, Toluna will issue notifications when conclive events occur within its system. To ensure the best possible experience and performance, Toluna required that its ES IP Partners host and API capable of consuming and activing upon its Member and Quota Status Notifications.





### C) Invite

*To Do*

### D) Survey Closed

*To Do*

### E) Prestart

*To Do*

## "Tracker" Surveys

A "Tracker" is a series of related Surveys. Toluna calls each iteration of these Surveys a "Wave." Each iteration will share a common SurveyID and its own WaveID. Toluna recommends that the Partner considers the combination of SurveyID+WaveID as the "unique identifier" for a Member's interation with a Survey. For the complete details of trackers and their benefits, pleae refer to the main Integration Guide.
