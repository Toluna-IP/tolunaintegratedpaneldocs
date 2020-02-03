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

#### Standard Flow

##### Real-Time Flow Diagram

![ES Flow](https://upload.wikimedia.org/wikipedia/en/8/84/Flo_from_Progressive_Insurance.jpg)


##### Get Quotas

Using your culture-specific "PanelGUID" provided by Toluna, call this route to obtain a current inventory of the application open Toluna Quotas.


##### Sample, Invite

Once Quota data is obtained, use your own sampling capability to match a Toluna Quota with one of your Members. Toluna will provide a document that links its profile attributes to a series of "AnswerIDs" found on each Quota. Partners can use this to map these details to their own standards. When a match is found, call Toluna and get an invite for the Member/Quota combination. Among other things, Toluna will provide a pre-formatted and "ready-to-go" invitation link.


##### Execute Invitation

Place the Invitation link in your Member's possession according to your internal workflow. Once executed, it behaves like any other (non-ES) IP invite.


##### Take Survey

Once the invitation is exercised, the Partner Member takes a Survey in the Toluna ecosystem. This process is identical to any other in the IP Program; no special provisions or action are required for ES-based experience


##### Survey Conclusion

Upon conclusion of the Survey, the Partner Member is redirected ack to a Partner-specific landing page. The options for redirection are identical to non-ES integration and can be found in Toluna's main integration guide.

#### "Recontact" Flow

At times, Tluna will seek to "reconnect" specific Members for a Quoa. Typically this is done to facilitate follow-up information for an original study. Since the target Members are already known, the partner has not requirement to sample its membership for the Quota. Instead, they query a Toluna API which will return the list of MemberCodes applicable for recontact. Once Obtained, the Partner should saple the list against the Recontact Quota to validate the targeting and generate an invite request for each match. From here, the process is identical to the interaction with a typical Quota.

##### Real-Time Flow Diagram

![Recontact Flow](https://via.placeholder.com/150)

##### Recontact Quotas

Using your culture-specific "PanelGUID" provided by Toluna, call this route to obtain a current inventory of the applicable open Toluna quotas

##### Is Survey Recontact

Once Quota data is obtained, each Survey applicable for Recontact will have the “IsSurveyRecontact” property set to “true”. This is an indication to disregard your own sampling capability and, instead, obtain the Quota’s list of “invite-able” MemberCodes from Toluna. Toluna will expose Recontact Surveys to Partners only if they have Members targetedfor Recontact; otherwise these Surveys will not appear in the results.

As the list of Recontact-eligible Members can be large, Toluna uses a separate API route (“GetRecontactMembersForQuota”) route to provide this information. This takes the Recontact Toluna QuotaID as a parameter and returns, by default, up to 10000 results per-call. It supports batching via the “lastMemberCodeReceived” parameter: provide your last MemberCode obtained for the Quota, and Toluna will begin the result set at the next Member (ordered alphanumerically, ascending). This route also allows consumers to define their own batch size via the “maxResults” parameter. If not provided, the default “maxResults” of 10000 is used. Toluna recommends restricting results to less than this value and does not guarantee performance about this limit. As a single Recontact Survey can have multiple Quotas, repeat this step for each Quota

##### Validate, Sample, Get Invites

When the list of MemberCodes has been obtained, perform any rquired local validation (e.g. Are the members still active on your end?). Once validated, execute your sampling process against the target recontact Quota for every Member. This will ensure that the targeting is correct and that each Recontact Member mataches the Quota Criteria. Finally, call the Toluna "GenerateInvite" route to obtain a standard Toluna IP invite for each matched Member. Once obtained, these invites are identical to any other in the IP Program.

##### Execute Invite

Use the Toluna invites according to the Partner's own requirements/workflow. Once executed, the Member's experience is consistent witht he traditional, "real-time" flow.

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
