---
title: External Sample API
has_children: true
nav_order: 2
---

# External Sample API 

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
| Sample Request | ``` GET http://{ES-Root-URL}/ExternalSample/96B52BEE-32FE-4A23-8FEE-821F6AAA5CA5/Quotas API_AUTH_KEY: 10B1BF48-F141-41CD-850F-4DE5A8BA44EB``` |
| Sample 200 Response | Full request can be seen [here]() |

| Name | Type | Description |
| :--- | :--- | :--- |
| CountryID | int | Toluna's unique identifier for the country in which the available Quotas are located. |
| CacheExpires | dateTime | Date at which Toluna's internal cache of this Quota data expired. Repreating API calls after this time guarentees an updated result set |
| Surveys | list<object> | A JSON
