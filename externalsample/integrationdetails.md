---
title: Integration Details 
has_children: false
nav_order: 1
parent: External Sample Offering
---


# ES Integration Details
{: .no_toc }

* TOC
{:toc}

## Introduction / Conceptual Diagram

The following is a conceptual representation of an ES Integration with Toluna. It describes components in a general manner and is not meant as instructions/requirements for the development of Partner infrastructure. Detailed instruction is found further in this page.

![ES Integration Diagram](https://tolunaonline-my.sharepoint.com/personal/garret_mcdannald_toluna_com/Documents/Microsoft%20Teams%20Chat%20Files/Screenshot%202020-02-04%20at%2016.40.55.png "ES Integration Diagram")

---

## What is the Flow?

Within the realms of the ES Offering, there are two kinds of Quotas Toluna uses with its Partners. The first is the Standard Quota, similar to our traditional offerings, but with ES-specific parameters. The second kind is the Recontact Quota, the definition of which will be explained further below. Detailed information on the Standard Flow can be found [here.](https://josh-toluna.github.io/tolunaintegratedpaneldocs/externalsample/standardflow.html "Standard ES Flow")

---

## "Recontact" Flow

At times, Tluna will seek to "reconnect" specific Members for a Quoa. Typically this is done to facilitate follow-up information for an original study. Since the target Members are already known, the partner has not requirement to sample its membership for the Quota. Instead, they query a Toluna API which will return the list of MemberCodes applicable for recontact. Once Obtained, the Partner should saple the list against the Recontact Quota to validate the targeting and generate an invite request for each match. From here, the process is identical to the interaction with a typical Quota.

Detailed information on the Recontact Flow can be found [here.](https://josh-toluna.github.io/tolunaintegratedpaneldocs/externalsample/recontactflow.html "Recontact ES Flow")

---

## How is ES Different than other offerings?

Toluna’s “External Sample” (ES) capability is an integration option offered as part of the Integrated Panel program. Its adoption permits the Partner to receive near real-time details about Toluna’s open quotas. Once obtained, Partners can use their own sampling capabilities to target the most appropriate respondents. This differs from the traditional IP model where Toluna maintains complete control over the sampling, routing, and invitation processes.

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

In order to complete the ES Integrated experience, Toluna will issue notifications when conclive events occur within its system. To ensure the best possible experience and performance, Toluna requires that its ES IP Partners host an API capable of consuming and activing upon its Member and Quota Status Notifications.

Detailed inforation on notifications can be found [here.](https://josh-toluna.github.io/tolunaintegratedpaneldocs/notifications/ "Notifications/Webhooks")
