---
title: Invite
has_children: false
parent: External Sample FAQ
grand_parent: FAQ
nav_order: 3
---

# Invite FAQs
{: .no_toc}

* TOC
{:toc}

---

## After we call GenerateInvite are the LOI and IR returned the same LOI and IR in the GetQuotas API?

There is a possibility that it might change as the scope of the job may change from initial sale.

---

## After we call GenerateInvite, will you send the invitation just like in Integrated Panel (IP) platform? (current invitation call with XML format)

API returns it in JSON format.

---

## Will the API return duplicate surveys?

Surveys won’t be returned via ES Invite API if a member has already responded/started the survey via other channels. For example, if a partner is enabled for ES and Dashboard, a survey will appear in both the APIs unless there is a click. If a Member responded via Dashboard link, then the survey won’t appear via ES channel and vice versa. 

---

## If we are using both External Sample and Dashboard or Notification, will Toluna send the same Surveys for ES and our other integration?

A Survey can be available in multiple offerings when a Partner integrates with more than one at a time. Ideally, Partners should only use ES or Dashboard/Notification and not use multiple offerings in conjunction with one another long-term. However, in the begging stages of a Partner transitioning to ES, we understand the desire to have ES running in parallel with another offering.

---