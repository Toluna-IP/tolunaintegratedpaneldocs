---
title: Quotas
has_children: false
parent: External Sample
grand_parent: FAQ
nav_order: 2
---

# Quotas FAQ
{: .no_toc}

* TOC
{:toc}

---

## Does the "CountryID" depend on the GUID?

Yes. Toluna IP Panels are culture-specific. CountryID is returned explicitly in the Quotas API for Partner’s ease when processing quotas across cultures

---

## What is CompletesRequired? Is it the max number of Members who are allowed to complete the survey?

It is the total number of qualified survey completes required to fill the Quota. Members will be allowed until the designated qualified completes are achieved.

---

## What is the API_AUTH_KEY configured in the new interface?

The API_AUTH_KEY is a partner-specific GUID provided by Toluna that must accompany every request to the ES APIs.

---

## When will we receive the panelGUID and ES_AUTH_KEY?

The panelGUID and ES_AUTH_KEY will be issued once our RnD integrates the panel on the Toluna side. The integration will begin once you are contacted by your account manager to complete/sign the Toluna API External Sampling Addendum as well as confirm pricing, end page, and notification URL implementation information required to be used for the ES panel.

> Note: If you are an existing IP Partner, then the ES option will be enable to your existing panel and the GUID will remain the same.

----

## What are Sampling rules? How do I Sample against a Quota?

External Sample Partners must comply with Toluna’s sampling rules. To be sampled for a  Quota, each Member must:

 - Be targeted for only one (1) Quota per Survey
 - Match ALL Layers in the Quota
 - Match ONE of the SubQuotas
 - Match at least one (1) "AnswerID" (SubQuotaAttribute) per SubQuota with the single QuestionID
 - Match at least one (1) "AnswerID" (SubQuotaAttribute) per QuestionID in the SubQUota with multiple QuestionIDs

For more details, please refer to the [Integration Details.](/externalsample/integrationdetails "Integration Details")

---

## Can I send users/members/panelists to Quotas with unanswered/unknown SubQuotas?

The Tolunma Platform requires complete match to all questions on a Quota unless the question is marked as isRoutable = true. With routable questions, Toluna will ask the Member a preliminary question before sending them to the Survey if the platform does not have an answer to a Quota.

---

## What happens when Toluna attempts to send us a notification and we do not receive it due to connection issues?

If an error occurs in sending the Quota notification, Toluna will try the message again after processing the rest of the current message Queue.

---

## What does the Parameter "IsRoutable" mean?

For a Member to be selected for a Survey, they must be an exact match to the desired quota. Questions that are "routable" allow Members to be invited to a Survey even if they do not have a Question/Answer set that is required by the Quota. Instead, Toluna will route the Member to a "prescreener" survey. This is prescreener survey will ask the missing question of the Member. If the Member selects an answer that matches the quota, they will be directed to the final Survey. If they don't match, they will be directed to the [Not Qualified URL](/memberrouting/endpages.html#not-qualified).