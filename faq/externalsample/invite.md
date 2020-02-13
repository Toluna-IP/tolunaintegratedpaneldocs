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

### After we call GenerateInvite, will you send the invitation just like in Integrated Panel (IP) platform? (current invitation call with XML format)

API returns it in JSON format.

---

### Will the API return duplicate surveys?

Surveys won’t be returned via ES Invite API if a member has already responded/started the survey via other channels. For example, if a partner is enabled for ES and Dashboard, a survey will appear in both the APIs unless there is a click. If a Member responded via Dashboard link, then the survey won’t appear via ES channel and vice versa. 

---
