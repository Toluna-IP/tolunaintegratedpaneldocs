---
title: Integration Details 
has_children: false
nav_order: 1
parent: External Sample Offering
---


# ES Integration Details
{: .no-toc }

* TOC
{:toc}

---

## What is the Flow?

Within the realms of the ES Offering, there are two kinds of Quotas Toluna uses with its Partners. The first is the Standard Quota, similar to our traditional offerings, but with ES-specific parameters. The second kind is the Recontact Quota, the definition of which will be explained further below. Quota-specific flows can be found [here.](https://josh-toluna.github.io/tolunaintegratedpaneldocs/externalsample/api/ "ES API")

---

## "Recontact" Flow

At times, Tluna will seek to "reconnect" specific Members for a Quoa. Typically this is done to facilitate follow-up information for an original study. Since the target Members are already known, the partner has not requirement to sample its membership for the Quota. Instead, they query a Toluna API which will return the list of MemberCodes applicable for recontact. Once Obtained, the Partner should saple the list against the Recontact Quota to validate the targeting and generate an invite request for each match. From here, the process is identical to the interaction with a typical Quota.

---

## How is ES Different than other offerings?

*To Do*

---

## What is needed for ES integration?

These are the additional points needed to achieve the full IP integration:

### Get Quotas from Toluna

Call the "GetQuotas" route for an inventory of current, open Quotas.

### Sampling / Member Selection 

Handled by Partner's platform

### Once Member is Sampled for Quota, Get Invite From Toluna

Provide some basic information and receive an invite from Toluna for your Member

### Create API to Receive Quota Status Notifications from Toluna 

Toluna will broadcast changes to its Quotas. Subscrube by establishing an API to handle these events.

>Please note: you will receive status changes for all open Quotas, not just those with which you are engaged.

---

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
   
### Sampling Examples

Click each button to open a new page with the JSON file for the specific example.

#### [Quota with Multiple Layers](){: .btn }

#### [Quota with Single Layer, SubQuota with Multiple QuestionIDs](){ .btn }

#### [Quota with Single Layer, SubQuota with Single QuestionID](){ .btn }

---

## Notifications

In order to complete the ES Integrated experience, Toluna will issue notifications when conclive events occur within its system. To ensure the best possible experience and performance, Toluna required that its ES IP Partners host and API capable of consuming and activing upon its Member and Quota Status Notifications.

### Member Status Notifications

These are issued upon conclusion of a Partner Member’s experience with a Toluna Survey. Partners must consume them in order to understand the outcome of their Member’s invitation to the Survey. In general, they take two forms: Termination and Completion. Both are existing features of the Toluna IP System, and documentation regarding their details can be found in the standard integration guide. ES partners also get ‘QuotaID’ in their notifications.

{: .label .label-green }
Suscription to these notifications is strongly recommended for ES Partners.

### Quota Status Notifications

A new feature for the ES integration, Toluna will deliver these notifications when one of its Quotas is no longer available for sampling or any of its previously on-hold Quota becomes available for sampling. A Partner must consume this event so that its sampling efforts can be discontinued when no longer viable.

Toluna will deliver this via HTTP POST when one of its Quotas is no longer available for sampling or any of its previously on-hold Quotas become available for sampling. It is the Partner’s responsibility to create an endpoint capable of consuming this information. 

>Please note that subscribers will receive updates for all Quotas, not just those with which they are engaged. Partners should construct their endpoint in a manner in which non-relevant Quota updates are ignored.

{: .label .label-green }
Suscription to these notifications is strongly recommended for ES Partners.

#### Route

Specified by Partner; Toluna will configure accordingly.

#### HTTP Verb

```POST```

#### Example Request

```POST [Partner-specified URL]```

#### Example POST Content
```json
 {
  "QuotaID": 3445365,
  "SurveyID": 45367678,
  "WaveID": 45367678,
  "IsLive": false,
  "UpdateDateTimeUTC": “2018-10-22 19:58:42.99 +00:00“
 }
 ```
#### Response Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| QuotaID | ```int``` | Toluna's unique identifier for a Quota |
| SurveyID | ```int``` | Toluna's ~~internal~~ unique identifier for a Survey |
| WaveID | ```int``` | Toluna's ~~internal~~ unqiue identifier for a single iteration of a Survey. The SurveyID+WaveID is always unqiue |
| IsLive | ```bool``` | Is the Quota currently capable of accepting Sample? |
| UpdateDateTimeUTC | ```dateTime``` | The date/time, in UTC, of the quota status change |
