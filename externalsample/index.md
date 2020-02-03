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

**Generating Invite**

*Description*: Once a Member has been matched to a Toluna Quota, this reoute can be used to generate an invitation.

*Route(s)*: ```GET /ExternalSample/{PanelGuid:GUID}/{MemberCode:string}/Invite/{QuotaID:int}```

*Header(s)* ```API_AUTH_KEY```: A Partner-specifc GUID providen by Toluna that must accompany every request.

*Parameters*

| Name | Type | Description |
| :--- | :--- | :--- |
| PanelGUID | Guid | A Toluna-issued unique identifier for a Partner's culture-specific panel |
| MemberCode | string | Partner's unique identifier for the Member as define when registered with Toluna. The PanelGUID+MemberCode is always unique within the Toluna system |
| QuotaID | int | Toluna's unqiue identifier for a Quota |

*Properties*

 - None
 
*Responses*

| Code | Etiology, actions |
| :--- | :--- |
| 200 | Request processed normally |
| 400 | Bad Request: see response for details |
| 500 | Internal Error: An exception occured while processing the request. Toluna likely has captured details in its logs |
| 403 | Forbidden: Invalid API_AUTH_KEY. See response for details |

*Sample Request*
```json
GET http://[APIROOT]/ExternalSample/{PanelGUID:Guid}/{MemberCode:string}/Invite/{QuotaID:int}
API_AUTH_KEY: {API_AUTH_KEY}
cache-control: no-cache
```

*Sample 200 Response*
```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
 {
  "SurveyId": 2349720,
  "WaveID": 34839308,
  "QuotaID": 3445365,
  "MemberAmount": 0.5,
  "PartnerAmount": 1,
  "URL": "http://[ROOT]/TrafficUI/MSCUI/Page.aspx?pgtid=20&od=kqe0mda072UagaQSVQIlgUX1QE4E41107",
  "LOI": 5,
  "IR": 40
 }
```

*Response Properties*

| Name | Type | Description |
| :--- | :--- | :--- |
| SurveyID | int | Toluna's internal unique identifier for a Survey |
| WaveID | int | Toluna's internal unique indentifier for a single iteration of a Survey. The SurveyID+WaveID is always unique |
| QuotaID | int | Toluna's unqiue identifier for a Quota |
| Member Amount | double | Amount Partner has agreed to pay it’s Member for a complete. This is rarely used and Toluna prefers to avoid direct engagement with the Partner-Member relationship |
| Partner Amount | double | Amount Toluna has agreed to pay Partner for a complete |
| URL | string | Link to Invite Member to Quota |
| LOI | int | Length of Interview at the time fo invite generation |
| IR | int | Incidence Rate at the time fo invite generation |

*Sample 400 Response*
```json
HTTP/1.1 400
Content-Type: application/json; charset=utf-8
 {
  "Result": "NO_QUOTA_ID",
  "ResultCode": 10
 }
```

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

##### GET RecontactMembersForQuota

For the requested Quota, returns a list of MemberCodes eligible for a recontact.

*Route(s)* 
```json
GET /ExternalSample/{panelGuid:GUID}/Recontact/{quotaID:int}/MemberCodes?maxResults={maxResults:int}&lastMemberCodeReceived={lastMemberCodeReceived:string}
```
*Header(s)*

```API_AUTH_KEY: A Partner-specific GUID prvoided by Toluna that must accompany every request```

*Parameters*

| Name | Type | Description |
| :--- | :-- | :--- |
| panelGUID | Guid | A Toluna-issued unique identifier for a Partner's culture-specific panel |
| quotaID | int | Tluna's unique identifier for a Quota |
| [OPTIONAL] The maximum number of MemberCodes that will be returned for the request. If not provided, defaults to a Toluna-configurable value (for, v0.1:10000) |
| lastMemberCodeReceived | string | [OPTIONAL] When dealing with batched results for a single Quota, supply this value to signal the last result received. The batch results will start with the MemberCode AFTER this value. Note that MemberCodes for recontact are ordered alphanumerically |

*Properties*

 - None
 
*Responses*

| Code | Etiology, actions |
| :--- | :--- |
| 200 | Request processed normally |
| 400 | Bad Request: see response for details |
| 500 | Internal Error. An exception occurred while processing this request. Toluna has likely captured details in its logs |
| 403 | Forbidden: invalid API_AUTH_KEY. See response for details |

*Sample Request*
```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
 {
  "MaxResults": 25,
  "HasAdditionalMembers": false,
  "MemberCodes": [
    "MemberCode1",
    "MemberCode2",
    "MemberCode3"
  ]
 }
```

*Response Properties*

| Name | Type | Description |
| :--- | :--- | :--- |
| MaxResults | int | The number of MemberCodes included in the response |
| HasAdditionalMembers | bool | When true, the Quota has more MemberCodes for recontact. Obtain them by repeating the request with the "lastMemberCodeReceived" parameter. |
| Member codes | ```list<string>``` | The MemberCodes Toluna would like to recontact for the Quota |

*Sample 400 Response*
```json
HTTP/1.1 400
Content-Type: application/json; charset=utf-8
 {
  "Result": "NO_QUOTA_ID",
  "ResultCode": 10
 }
```

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

| Name | GetQuotas |
| :--- | :--- |
|Description | For a Toluna-issued "PanelGUID," returns a list of Surveys and their associated Quotas in need of supply. |
| Route(s) | ``` GET /ExternalSample/{PanelGUID:GUID}/Quotas?includeRoutables:bool``` |
| Header(s) | ``` API_AUTH_KEY ``` A partner-specific GUID provided by Toluna that must accompany every request |
| Parameters | <div class="table-wrapper"><table> <thead> <tr> <th style="text-align: left">Name</th> <th style="text-align: left">Type</th> <th style="text-align: left">Description</th> </tr> </thead> <tbody> <tr> <td style="text-align: left">PanelGUID</td> <td style="text-align: left">Guid</td> <td style="text-align: left">A Toluna-issue unique identifier for a Partner’s culture-specific panel.</td> </tr> <tr> <td style="text-align: left">includeRoutables</td> <td style="text-align: left">bool</td> <td style="text-align: left">(Optional) Indicates whether to include Routable questions in the result or not. This will take precedence over the panel-level setting which is OFF by default. Opt in to set Panel-level setting to be ON.</td> </tr> </tbody> </table></div> |
| Properties | N/A |
| Sample Request | ``` GET http://{ES-Root-URL}/ExternalSample/96B52BEE-32FE-4A23-8FEE-821F6AAA5CA5/Quotas API_AUTH_KEY: 10B1BF48-F141-41CD-850F-4DE5A8BA44EB``` |
| Sample 200 Response | Full request can be seen [here](https://josh-toluna.github.io/tolunaintegratedpaneldocs/externalsample/getquotasresponse.json "Sample 200 Response") |
| Possible Request Response Codes | <table> <thead> <tr> <th style="text-align: left">Code</th> <th style="text-align: left">Etiology, actions</th> </tr> </thead> <tbody> <tr> <td style="text-align: left">200</td> <td style="text-align: left">Request processed normally</td> </tr> <tr> <td style="text-align: left">400</td> <td style="text-align: left">Bad Request. See response for details</td> </tr> <tr> <td style="text-align: left">500</td> <td style="text-align: left">Internal Error. An exception occurred while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs</td> </tr> <tr> <td style="text-align: left">403</td> <td style="text-align: left">Forbidden: Invalid <code class="language-plaintext highlighter-rouge">API_AUTH_KEY</code> See response for details</td> </tr> </tbody> </table> |

### Sample 400 Response
```json
HTTP/1.1 400
Content-Type: application/json; charset=utf-8

 {
   "Result": "PANEL_DOES_NOT_EXIST",
   "ResultCode": 3
 }
```

### Response Properties

| Name | Type | Description |
| :--- | :--- | :--- |
| CountryID |	int |	Toluna’s unique identifier for the country in which the available Quotas are located. |
| CacheExpires |	dateTime |	Date at which Toluna’s internal cache of this Quota data expired. Repreating API calls after this time guarentees an updated result set |
| Surveys |	```list<object>``` |	A JSON object containing 1:M Surveys for which Toluna has open Quotas |
| Survey.SurveyID |	int |	Toluna’s internal unique identifies for a Survey |
| Survey.SurveyName |	string |	Toluna’s internal name for a Survey |
| Survey.SurveyTopic |	string |	Study type of a Survey |
| Survey.WaveID |	int |	Toluna’s internal unique identifier for a single iteration of a Survey. The SurveyID+WaveID is always unique |
| Survey.LOI |	int |	Length of interview |
| Survey.IR |	int |	Incidence Rate |
| Survey.StudyTypeID |	int |	The Survey’s “category.” See mapping document for values |
| Survey.ScheduledCompletionDate |	dateTime |	Date at which Survey is set to close |
| Survey.DeviceTypeIDs |	```list<int>``` |	Devices upon which the Survey can be used. See mapping document for details |
| Survey.IsSurveyRecontact |	bool |	When TRUE, the Survey is looking to engage specific Members for a follow-up study. Please see the “Recontact” section for mor einformation regarding its use |
| Survey.CompletesRequired |	int |	The total number of completes required across all Quotas until the ScheduleCompletionDate. This should be considered the limit of completes available. At times, this may be less than the sum of all Quotas |
| Survey.EstimatedCopletesRemaining |	int |	The estimated number of completes remaining until the ScheduleCompletionDate, across all Quotas, until the Survey is full. At times, this may be less than the sum of all Quotas |
| Survey.Price |	```<object>``` |	A JSON object containing details about price Toluna will pay per complete |
| Price.Amount |	double |	The monetary amount of the payment per complete |
| Price.CurrencyID |	int |	Currency in which the payment per complete is denoted. See mapping document for details |
| Survey.Quotas |	```list<object>``` |	A JSON object containing 1:M Quotas for the Survey. Members can be targeted only to one quota within the Survey |
| Quota.QuotaID |	int |	Toluna’s unique identifier for a Quota |
| Quota.CompletesRequired |	int |	The total number of completes required to fill the Quota |
| Quota.EstimatedCompletesRemaining |	int |	The estimated number of completes remaining until the Quota is filled |
| Quota.Layers |	```list<object>``` |	A JSON object containing groups of Quotas. When sampling, all Layers must be matched |
| Layer.LayerID |	int |	Toluna’s unique identifier for a Layer |
| Layer.SubQuotas |	```list<object>``` |	A JSON object contains 1:M SubQuotas. When sampling, one SubQuota must be matched |
| SubQuota.SubQuotaID |	int |	Toluna’s unique identifier for a SubQuota |
| SubQuota.CurrentCompletes |	int |	Current complete received for a SubQuota |
| SubQuota.MaxTargetCompletes |	int |	Maximum target completes required for a SubQuota |
| SubQuota.QuestionsAndAnswers |	```list<object>``` |	A JSON object contains collection of Question and Answers per SubQuota |
| QuestionAnswers.QuestionID |	int |	Toluna internal profile attribute identifier |
| QuesitonAndAnswers.AnswerIDs |	```list<int>``` |	List of Toluna internal profile attribute identifiers. When sampling, at least one AnswerID must match. See mapping document for details |
| QuestionAndAnswers.AnswerValues |	```string<int>``` |	List of Answer values of an open ended answers.Example: Custom Age values “18-100”, Postal codes, DMA and MSA. Note: “Age” will be range based. “DMA and MSA” will be comma separated Answer IDs. “Postal codes” will be comma separated postal code values. It can contain partial values. ‘Starts with’ must be applied to match it. API is limited to expose only first 1000 postal codes. |
| QuestionAndAnswers.IsRoutable |	boolean |	Indicates whether the question is Routable or not |


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

### A) Member Status Notification

When a Partner Member has completed interaction with a Toluna Survey, Toluna will deliver a notification signifying this event and its details. For the most part, these are identical to the "real-time" notifications described in the main Integration Guide. Subscription to these notification are required for ES Partners.

The following is information on the two types of Member Status Notification
 - Terminated: *To do*
 - Completed: *To do*

### B) Quota Status Notifications

A new feature for the ES Integration, Toluna will deliver these notifications when one of its Quotas is not longer available for sompling or any of its perviously on-hold Quotas become available for sampling. 
>A Partner must consume this event so that its sampling efforts can be discontinued when no longer viable.

#### Notification from Toluna to Partner API

Toluna will deliver this via HTTP POST when one of its Quotas is no longer available for sampling or any of its previously on-hold Quota becomes available for sampling. It is the Partner’s responsibility to create an endpoint capable of consuming this information. Please note that subscribers will receive updates for all Quotas, not just those with which they are engaged. Partners should construct their endpoint in a manner in which non-relevant Quota updates are ignored.

#### Route(s)

- Specified by Partner; Toluna will confingure accordingly
 
#### HTTP Verb

- POST
 
#### Sample Request
```json
POST [Partner-Specified URL]
```

#### Sample POST
```json
 {
  "QuotaID": 3445365,
  "SurveyID": 45367678,
  "WaveID": 45367678,
  "IsLive": false,
  "UpdateDateTimeUTC": “2018-10-22 19:58:42.99 +00:00“
 }
```

#### Response Properties

| Name | Type | Description |
| :--- | :--- | :--- |
| QuotaID | int | Toluna's unique identifier for a Quota |
| SurveyID | int | Toluna's internal unique identifier for a Survey |
| WaveID | int | Toluna's internal unique identifier for a single iteration of a Survey. The SurveyID+WaveID is always unique |
| IsLive | Bool | Is the Quota currently capable of accepting Sample? |
| UpdateDateTimeUTC | dateTime | The date/time, in UTC, of the quota status change |

### C) Invite

*To Do*

### D) Survey Closed

*To Do*

### E) Prestart

*To Do*

## "Tracker" Surveys

A "Tracker" is a series of related Surveys. Toluna calls each iteration of these Surveys a "Wave." Each iteration will share a common SurveyID and its own WaveID. Toluna recommends that the Partner considers the combination of SurveyID+WaveID as the "unique identifier" for a Member's interation with a Survey. For the complete details of trackers and their benefits, pleae refer to the main Integration Guide.
