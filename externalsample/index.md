---
title: External Sample
has_children: true
nav_order: 2
---

# External Sample 

## Introduction

### Background

Toluna’s “External Sample” (ES) capability is an integration option offered as part of the Integrated Panel program. Its adoption permits the Partner to receive near real-time details about Toluna’s open quotas. Once obtained, Partners can use their own sampling capabilities to target the most appropriate respondents. This differs from the traditional IP model where Toluna maintains complete control over the sampling, routing, and invitation processes.

### Incremental Option

Internally at Toluna, the existing IP Framework views ES as simply another option for getting survey invitations into the hands of its Partners. As such, Partners choosing to adopt this capability requires only a few additional integration points beyond the traditional model.

### Additional Integration Requirements

When evaluating IP Partnership, the Partner should choose ES as the method of invitation (as opposed to Dashboard or Notification). After doing so, these are the additional points needed to achieve the full IP integration:

- *Get Quotas from Toluna*
  - Call the "GetQuotas" route for an inventory of current, open Quotas.
- *Once Member is Sampled for Quota, Get Invite From Toluna*
  - Provide some basic information and receive an invite from Toluna for your Member
- *Create API to Receive Quota Status Notifications from Toluna*
  - Toluna will broadcast changes to its Quotas. Subscrube by establishing an API to handle these events.
  - >PLease note: you will receive status changes for all open Quotas, not just those with which you are engaged.

## Real-Time Flow

![Input ES Flow Here](https://upload.wikimedia.org/wikipedia/en/8/84/Flo_from_Progressive_Insurance.jpg)

**Get Quotas**

Using your culture-specific "PanelGUID" provided by Toluna, call this route to obtain a current inventory of the application open Toluna Quotas.


**Sample, Invite**

Once Quota data is obtained, use your own sampling capability to match a Toluna Quota with one of your Members. Toluna will provide a document that links its profile attributes to a series of "AnswerIDs" found on each Quota. Partners can use this to map these details to their own standards. When a match is found, call Toluna and get an invite for the Member/Quota combination. Among other things, Toluna will provide a pre-formatted and "ready-to-go" invitation link.


**Execute Invitation**

Place the Invitation link in your Member's possession according to your internal workflow. Once executed, it behaves like any other (non-ES) IP invite.


**Take Survey**

Once the invitation is exercised, the Partner Member takes a Survey in the Toluna ecosystem. This process is identical to any other in the IP Program; no special provisions or action are required for ES-based experience


**Survey Conclusion**

Upon conclusion of the Survey, the Partner Member is redirected ack to a Partner-specific landing page. The options for redirection are identical to non-ES integration and can be found in Toluna's main integration guide.

## What happens in the Back-end?

This describes several support processes Toluna will operate in the background of an ES integration.

A) Member Status Notification

When a Partner Member has completed interaction with a Toluna Survey, Toluna will deliver a notification signifying this event and its details. For the most part, these are identical to the "real-time" notifications described in the main Integration Guide. Subscription to these notification are required for ES Partners.

B) Quota Status Notifications

When a Quota is no longer available or a previosly on-hold Quota becomes available/live, Toluna will broadcase this information to its Partners. Subscription to this notiifcatoin is required for all ES Partners.
> Please note: Subscribers will receive updates for all Quotas, not just those with which they are engaged. Partners should integrate in a manner in which non-relevant Quota updates are ignored.

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
| Response Properties | <table> <thead> <tr> <th style="text-align: left">Name</th> <th style="text-align: left">Type</th> <th style="text-align: left">Description</th> </tr> </thead> <tbody> <tr> <td style="text-align: left">CountryID</td> <td style="text-align: left">int</td> <td style="text-align: left">Toluna’s unique identifier for the country in which the available Quotas are located.</td> </tr> <tr> <td style="text-align: left">CacheExpires</td> <td style="text-align: left">dateTime</td> <td style="text-align: left">Date at which Toluna’s internal cache of this Quota data expired. Repreating API calls after this time guarentees an updated result set</td> </tr> <tr> <td style="text-align: left">Surveys</td> <td style="text-align: left"><code class="language-plaintext highlighter-rouge">list&lt;object&gt;</code></td> <td style="text-align: left">A JSON object containing 1:M Surveys for which Toluna has open Quotas</td> </tr> <tr> <td style="text-align: left">Survey.SurveyID</td> <td style="text-align: left">int</td> <td style="text-align: left">Toluna’s internal unique identifies for a Survey</td> </tr> <tr> <td style="text-align: left">Survey.SurveyName</td> <td style="text-align: left">string</td> <td style="text-align: left">Toluna’s internal name for a Survey</td> </tr> <tr> <td style="text-align: left">Survey.SurveyTopic</td> <td style="text-align: left">string</td> <td style="text-align: left">Study type of a Survey</td> </tr> <tr> <td style="text-align: left">Survey.WaveID</td> <td style="text-align: left">int</td> <td style="text-align: left">Toluna’s internal unique identifier for a single iteration of a Survey. The SurveyID+WaveID is always unique</td> </tr> <tr> <td style="text-align: left">Survey.LOI</td> <td style="text-align: left">int</td> <td style="text-align: left">Length of interview</td> </tr> <tr> <td style="text-align: left">Survey.IR</td> <td style="text-align: left">int</td> <td style="text-align: left">Incidence Rate</td> </tr> <tr> <td style="text-align: left">Survey.StudyTypeID</td> <td style="text-align: left">int</td> <td style="text-align: left">The Survey’s “category.” See mapping document for values</td> </tr> <tr> <td style="text-align: left">Survey.ScheduledCompletionDate</td> <td style="text-align: left">dateTime</td> <td style="text-align: left">Date at which Survey is set to close</td> </tr> <tr> <td style="text-align: left">Survey.DeviceTypeIDs</td> <td style="text-align: left"><code class="language-plaintext highlighter-rouge">list&lt;int&gt;</code></td> <td style="text-align: left">Devices upon which the Survey can be used. See mapping document for details</td> </tr> <tr> <td style="text-align: left">Survey.IsSurveyRecontact</td> <td style="text-align: left">bool</td> <td style="text-align: left">When TRUE, the Survey is looking to engage specific Members for a follow-up study. Please see the “Recontact” section for mor einformation regarding its use</td> </tr> <tr> <td style="text-align: left">Survey.CompletesRequired</td> <td style="text-align: left">int</td> <td style="text-align: left">The total number of completes required across all Quotas until the ScheduleCompletionDate. This should be considered the limit of completes available. At times, this may be less than the sum of all Quotas</td> </tr> <tr> <td style="text-align: left">Survey.EstimatedCopletesRemaining</td> <td style="text-align: left">int</td> <td style="text-align: left">The estimated number of completes remaining until the ScheduleCompletionDate, across all Quotas, until the Survey is full. At times, this may be less than the sum of all Quotas</td> </tr> <tr> <td style="text-align: left">Survey.Price</td> <td style="text-align: left"><code class="language-plaintext highlighter-rouge">&lt;object&gt;</code></td> <td style="text-align: left">A JSON object containing details about price Toluna will pay per complete</td> </tr> <tr> <td style="text-align: left">Price.Amount</td> <td style="text-align: left">double</td> <td style="text-align: left">The monetary amount of the payment per complete</td> </tr> <tr> <td style="text-align: left">Price.CurrencyID</td> <td style="text-align: left">int</td> <td style="text-align: left">Currency in which the payment per complete is denoted. See mapping document for details</td> </tr> <tr> <td style="text-align: left">Survey.Quotas</td> <td style="text-align: left"><code class="language-plaintext highlighter-rouge">list&lt;object&gt;</code></td> <td style="text-align: left">A JSON object containing 1:M Quotas for the Survey. Members can be targeted only to one quota within the Survey</td> </tr> <tr> <td style="text-align: left">Quota.QuotaID</td> <td style="text-align: left">int</td> <td style="text-align: left">Toluna’s unique identifier for a Quota</td> </tr> <tr> <td style="text-align: left">Quota.CompletesRequired</td> <td style="text-align: left">int</td> <td style="text-align: left">The total number of completes required to fill the Quota</td> </tr> <tr> <td style="text-align: left">Quota.EstimatedCompletesRemaining</td> <td style="text-align: left">int</td> <td style="text-align: left">The estimated number of completes remaining until the Quota is filled</td> </tr> <tr> <td style="text-align: left">Quota.Layers</td> <td style="text-align: left"><code class="language-plaintext highlighter-rouge">list&lt;object&gt;</code></td> <td style="text-align: left">A JSON object containing groups of Quotas. When sampling, all Layers must be matched</td> </tr> <tr> <td style="text-align: left">Layer.LayerID</td> <td style="text-align: left">int</td> <td style="text-align: left">Toluna’s unique identifier for a Layer</td> </tr> <tr> <td style="text-align: left">Layer.SubQuotas</td> <td style="text-align: left"><code class="language-plaintext highlighter-rouge">list&lt;object&gt;</code></td> <td style="text-align: left">A JSON object contains 1:M SubQuotas. When sampling, one SubQuota must be matched</td> </tr> <tr> <td style="text-align: left">SubQuota.SubQuotaID</td> <td style="text-align: left">int</td> <td style="text-align: left">Toluna’s unique identifier for a SubQuota</td> </tr> <tr> <td style="text-align: left">SubQuota.CurrentCompletes</td> <td style="text-align: left">int</td> <td style="text-align: left">Current complete received for a SubQuota</td> </tr> <tr> <td style="text-align: left">SubQuota.MaxTargetCompletes</td> <td style="text-align: left">int</td> <td style="text-align: left">Maximum target completes required for a SubQuota</td> </tr> <tr> <td style="text-align: left">SubQuota.QuestionsAndAnswers</td> <td style="text-align: left"><code class="language-plaintext highlighter-rouge">list&lt;object&gt;</code></td> <td style="text-align: left">A JSON object contains collection of Question and Answers per SubQuota</td> </tr> <tr> <td style="text-align: left">QuestionAnswers.QuestionID</td> <td style="text-align: left">int</td> <td style="text-align: left">Toluna internal profile attribute identifier</td> </tr> <tr> <td style="text-align: left">QuesitonAndAnswers.AnswerIDs</td> <td style="text-align: left"><code class="language-plaintext highlighter-rouge">list&lt;int&gt;</code></td> <td style="text-align: left">List of Toluna internal profile attribute identifiers. When sampling, at least one AnswerID must match. See mapping document for details</td> </tr> <tr> <td style="text-align: left">QuestionAndAnswers.AnswerValues</td> <td style="text-align: left"><code class="language-plaintext highlighter-rouge">string&lt;int&gt;</code></td> <td style="text-align: left">List of Answer values of an open ended answers.Example: Custom Age values “18-100”, Postal codes, DMA and MSA. Note: “Age” will be range based. “DMA and MSA” will be comma separated Answer IDs. “Postal codes” will be comma separated postal code values. It can contain partial values. ‘Starts with’ must be applied to match it. API is limited to expose only first 1000 postal codes.</td> </tr> <tr> <td style="text-align: left">QuestionAndAnswers.IsRoutable</td> <td style="text-align: left">boolean</td> <td style="text-align: left">Indicates whether the question is Routable or not</td> </tr> </tbody> </table> |
| Test | Test |

