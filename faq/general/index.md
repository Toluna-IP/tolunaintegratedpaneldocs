---
title: General
has_children: false
parent: FAQ
nav_order: 1
---

# General FAQs
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

## Is there a service or documentation that will help us derive regional mappings, such as DMA and MSA?

Toluna provides documents to all of its Partners to assist with mapping. Contact your Toluna representative if you require these documents.

---

## Will Toluna provide us a daily inventory count?

At Partner request, Toluna may set up a profiler to keep track of the Partner’s average daily inventory. Please note: Toluna may not recall average daily inventories retroactively - averages will only be recorded from the date of profiler setup.

---

## Why am I receiving different return values in production than I did in sandbox testing?

Surveys have a category/SurveyTopic (denoted internally as StudyType), which can have a different translated value for each culture. Sandbox and Production environments are consistent in many things but it is possible for Survey translations, both the values and presence of them, to vary between the two environments.

---

## Does Toluna provide any metrics around Survey conversion rates?

We do not currently have an API which provides metrics on conversion rate. The closest indicator of performance we have is the project IR, or Incidence Rate, which adjusts in real time once a particular threshold has been reached for a particular Survey.

---

## What is the difference between a Redirect URL and a Notification URL?

[Redirect URL](/memberrouting/) is where Toluna’s platform is sending Respondents in certain situations. A [Notification])(/notifications/quotastatus.html) is Toluna’s platform sending information to a Partner about an event.

---

## What do DeviceTypeIDs 1, 2, and 3 stand for?

1. Desktop/laptop
2. Tablet
3. Phone

---

## Does Toluna require its Partners to implement IP whitelists?

No, Toluna does not require its Partners use IP whitelists.

---

## If a Panelist  a Survey and, upon completion, is routed directly a separate Survey, how can a Partner update the transactions for bothn Surveys?

Example:

* Panelist starts Survey A
* Upon completion, Panelist is automatically routed to Survey B
* After completing Survey B, panelist is routed to the endpage for Survey B
* Panelist is never routed to/through the endpage for Survey A

The complete/termination notification for Survey B would contain additional data to indicate this is for a re-route and have the original survey info.

Ex:
```
...
"IsAutoRouted": true,
OriginalSurveyID: {SurveyID of Survey A}
...
```

See [Member-Survey Flow](/memberrouting/membersurveyflow#autorouting.html) for more details on the AutoRouting feature.

---

## What are DMA and MSA?

These are both computed demographic values that are based off of a Member's zip code (US members) that provide additional context. More details can be found [here.](https://www.digitaladvertising-101.com/blog/digital-101-dma-vs-msa)

---
