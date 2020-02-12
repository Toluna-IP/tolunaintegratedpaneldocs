---
title: General FAQ
has_children: false
parent: FAQ
nav_order: 1
---

# General FAQ
{: .no_toc}

* TOC
{:toc}

---

## What is your API root, i.e. the common part of the URL for your API calls?

The API root URL will be provided by Toluna once partnership has started. Please contact your Toluna representative if you have yet to receive your URL.

---

## What is your API to register a panelist?

To register a panelist/member with Toluna, a Partner must use the HTTP POST route. Full details on Member Mangement, including registering, updating, and requesting Member info can be found [here.](/membermanagement)

---

## What is your API to get your set of questions and answers?

The route for a Partner to obtain their set(s) of questions and answers differs slightly depending on the Integration Offering of their choice. Select your offering from the following list for detailed information:

 - [Notification Offering](/notification)
 - [Dashboard Offering](/dashboard)
 - [External Sampling](/externalsample)

---

## Is there an API to get the current stats of a survey, such as conversion rate?

Toluna has a significant inventory of Reporting APIs that Partners can use to obtain information on Surveys, Members, and Panels, such as the details of a Survey, including LOI and IR.

Detailed information on this and other useful Reports can be found [here.](/reporting/api)

---

## I don’t see any indication of what country or locale a panelist belongs to. How does Toluna handle that?

Toluna includes these values with PartnerGUID property, which is tied to a specific culture (country-language).

---

## What is the distinction between "Unique Partner Code," PartnerGUID, and PanelGUID?

There is not distinction between these values. The terms are equivalent and interchangeable in discussion, but PanelGUID should be used with Toluna's API.

---

## Why am I seeing some duplicates of answers with separate, unique IDs regarding question 1001569 (MSA)?

The MSA answer value uniqueness is driven by the MSA code instead of the text that it is associated with.

Example: There are two "Decatur" values, 2040 and 2030. The first refers to Decatur, IL, USA, while the second refers to Decatur, AL, USA.

Similar cases can be seen showing multiple MSA values that resolve the cities of the same name but are located in different states. Toluna's recommendation is to match on the MSA Answer Integer instead of the associated text.

---
