---
title: FAQ
has_children: false
nav_order: 99
---

# FAQs
{: .no_toc }

* TOC
{:toc}

---

# External Sample Integration

---

## General

### What is “External Sample (ES)? How it is different from other IP integration options?

Toluna’s “External Sample” (ES) capability is an integration option offered as part of the Integrated Panel program.  Its  adoption permits the Partner to receive near real-time details about Toluna’s open quotas.  Once obtained, Partners can    use their own sampling capabilities to target the most appropriate respondents. This differs from the traditional IP      model where Toluna maintains complete control over the sampling, routing, and invitation processes.

### Can other integration option(s) can be operated in parallel with IP ES? Will the current Integration work?

Yes. This is just another integration option. If you are a Dashboard partner and willing to integrate as an ES partner, it is possible, and both the integrations will work seamlessly.

### If I’m a Dashboard partner, do I need to have new End Page and Notification Urls?

No, the ES integration actually uses the same End Page and Notification Urls as the Dashboard offering. While this does reduce the need for a new set of endpoints, it also means that only one set of Endpoint Urls is allowed in our platform.

### How are Members added to Toluna's panel in ES?

IP Member Managemnet API must be used by ES Partners to add/update/get member information. This is the same as other integration options. Please check the regular IP Integration Guide for more details. Note: For an existing partner, the ES feature can be turned on to the existing panel and it becomes available for your panel members.

### Can ES partner use existing Members in the IP Program?

Yes. ES integration offering/feature can be turned on to the existing program and all the panel members become eligible.

###  Is the new API related to the old API?

The External Sample API will contain the same projects presented in the current API. However, the method in which those opportunities are delivered is different.

### What are the new features introduced with “External sample”? 

Besides exposing the inventory/open quotas via the API, below are the new features available for the ES partners.
 - Pre-Start Notification: All pre-start failures will be sent as “terminate” notifications. Examples: SurveyTaken, QuotaFull, NoSurveysFound, BlockedIPAddress etc.
 - Quota Status Notification: Notifictions are sent to the Partner's URL if a Quota's status changes from active to inactive or vice versa.

### How does the ES process vary from the regular IP integration after obtaining the invite link?

After obtaining the invite link via Invite API (please refer Integration Guide for complete details), everything is the same as the regular integration including the real time notifications, redirections, etc.

---

## Quotas API

### Does the "CountryID" depend on the GUID?

Yes. Toluna IP Panels are culture-specific. CountryID is returned explicitly in the Quotas API for Partner’s ease when processing quotas across cultures

### What is CompletesRequired? Is it the max number of Members who are allowed to complete the survey?

It is the total number of qualified survey completes required to fill the Quota. Members will be allowed until the designated qualified completes are achieved.

### What is the API_AUTH_KEY configured in the new interface?

The API_AUTH_KEY is a partner-specific GUID provided by Toluna that must accompany every request to the ES APIs.

### When will we receive the panelGUID and ES_AUTH_KEY?

The panelGUID and ES_AUTH_KEY will be issued once our RnD integrates the panel on the Toluna side. The integration will begin once you are contacted by your account manager to complete/sign the Toluna API External Sampling Addendum as well as confirm pricing, end page, and notification URL implementation information required to be used for the ES panel.

> Note: If you are an existing IP Partner, then the ES option will be enable to your existing panel and the GUID will remain the same.

### What are Sampling rules? How do I Sample against a Quota?

External Sample Partners must comply with Toluna’s sampling rules. To be sampled for a  Quota, each Member must:

 - Be targeted for only one (1) Quota per Survey
 - Match ALL Layers in the Quota
 - Match ONE of the SubQuotas
 - Match at least one (1) "AnswerID" (SubQuotaAttribute) per SubQuota with the single QuestionID
 - Match at least one (1) "AnswerID" (SubQuotaAttribute) per QuestionID in the SubQUota with multiple QuestionIDs

For more details, please refer to the [Integration Details.](https://josh-toluna.github.io/tolunaintegratedpaneldocs/externalsample/integrationdetails.html "Integration Details")

---

## Invite API

### After we call GenerateInvite are the LOI and IR returned the same LOI and IR in the GetQuotas API?

There is a possibility that it might change as the scope of the job may change from initial sale.

### After we call GenerateInvite, will you send the invitation just like in Integrated Panel (IP) platform? (current invitation call with XML format)

API returns it in JSON format.

### Will the API return duplicate surveys?

Surveys won’t be returned via ES Invite API if a member has already responded/started the survey via other channels. For example, if a partner is enabled for ES and Dashboard, a survey will appear in both the APIs unless there is a click. If a Member responded via Dashboard link, then the survey won’t appear via ES channel and vice versa. 
