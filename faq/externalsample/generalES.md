---
title: General ES
has_children: false
parent: External Sample
grand_parent: FAQ
nav_order: 1
---

# General ES FAQs
{: .no_toc}

* TOC
{:toc}

---

## What is “External Sample (ES)? How it is different from other IP integration options?

Toluna’s “External Sample” (ES) capability is an integration option offered as part of the Integrated Panel program.  Its  adoption permits the Partner to receive near real-time details about Toluna’s open quotas.  Once obtained, Partners can    use their own sampling capabilities to target the most appropriate respondents. This differs from the traditional IP      model where Toluna maintains complete control over the sampling, routing, and invitation processes.

---

## We’ve recently changed to External Sample offering from Notification or Dashboard. Do we need to re-PUT all panelists to a new panel? If so, can they be copied over on your end?



---

## Can other integration option(s) can be operated in parallel with IP ES? Will the current Integration work?

Yes. This is just another integration option. If you are a Dashboard partner and willing to integrate as an ES partner, it is possible, and both the integrations will work seamlessly.

---

## If I’m a Dashboard partner, do I need to have new End Page and Notification Urls?

No, the ES integration actually uses the same End Page and Notification Urls as the Dashboard offering. While this does reduce the need for a new set of endpoints, it also means that only one set of Endpoint Urls is allowed in our platform.

---

## How are Members added to Toluna's panel in ES?

IP Member Managemnet API must be used by ES Partners to add/update/get member information. This is the same as other integration options. Please check the regular IP Integration Guide for more details. Note: For an existing partner, the ES feature can be turned on to the existing panel and it becomes available for your panel members.

---

## Can ES partner use existing Members in the IP Program?

Yes. ES integration offering/feature can be turned on to the existing program and all the panel members become eligible.

---

##  Is the new API related to the old API?

The External Sample API will contain the same projects presented in the current API. However, the method in which those opportunities are delivered is different.

---

## What are the new features introduced with “External sample”? 

Besides exposing the inventory/open quotas via the API, below are the new features available for the ES partners.
 - Pre-Start Notification: All pre-start failures will be sent as “terminate” notifications. Examples: SurveyTaken, QuotaFull, NoSurveysFound, BlockedIPAddress etc.
 - Quota Status Notification: Notifictions are sent to the Partner's URL if a Quota's status changes from active to inactive or vice versa.

 ---

## How does the ES process vary from the regular IP integration after obtaining the invite link?

After obtaining the invite link via Invite API (please refer Integration Guide for complete details), everything is the same as the regular integration including the real time notifications, redirections, etc.

---

## Is there some property of a survey that indicates that panelists need to be restricted if they participated in some other survey or set of surveys?

For Recontact Surveys and WaveIDs, Toluna allows Members to be excluded from participating based on their answers on previous Surveys or Waves. Detailed information on how to use this feature can be seen [here.](/externalsample/api/surveyexclusion.html)

---

## For our Age profiler, sometimes Toluna uses only AnswerIDs, and other times they use AnswerValues. What is and where is there this distinction?

If has Toluna provides a defined custom age range, the age range will be sent in AnswerValues, otherwise AnswerIDs will be provided. The partner will need to accommodate both on their end.