---
title: Integration Details 
has_children: false
nav_order: 1
parent: External Sample Offering
---


# External Sample - Standard Flow

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


## Notifications

In order to complete the ES Integrated experience, Toluna will issue notifications when conclive events occur within its system. To ensure the best possible experience and performance, Toluna required that its ES IP Partners host and API capable of consuming and activing upon its Member and Quota Status Notifications.

