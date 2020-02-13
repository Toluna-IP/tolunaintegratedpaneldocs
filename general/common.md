---
title: Common Items
has_children: false
parent: General
nav_order: 3
---

# Common Items
{: .no_toc}

The following are important features and notes on the Toluna Platform that are useful to all Partners, regardless of Integration Offering Selection.

* TOC
{:toc}

---

## Jargon

The following is a list of Jargon commonly within Toluna's platform.

| Name | Description |
| :--- | :--- |
| jargon | jargon descriptor |

## Pricing

*to do* by Josh

 - Business will decide
 - Approaches: fixed, dynamic, grid
 - Pricing done by culture

---

## Content Type

The preferred content type is json. Any new notification developed will only be available in JSON format. Existing content that is also available in XML format will be explicitly described.

---

## "Tracking" Surveys and the WaveID Property

A “Tracker” is a series of related surveys. Toluna calls each iteration of these Surveys a “Wave." Waves are specific to Surveys only and not to the Repondent themselves. From the Respondent’s perspective, each Wave is experienced like an individual Survey. To the Partner, each Wave of a Tracker carries its own “WaveID” but shares a common SurveyID. All new partners are opted-in to use WaveID by default. WaveID will appear on Invites, Reports, Redirects, and in all Notifications (completion, termination, and surveyClosed).

### Benefits of Using WaveID

Since each iteration of the Tracker shares the same SurveyID, a Survey can be interpreted as duplicate if the WaveID is not included. Including WaveID eliminates the potential for "false duplicates" and increases the number of invites and the potential for a corresponding increase in completes.

### Removing WaveID from Your Integration Profile

Toluna recommends that the Partner considers the combination of SurveyID+WaveID as the "unique identifier" for a Respondent's interaction with a Survey. If you wish to remove WaveID from your profile, please contact your Toluna representative. This requires a simple configuration change on the Toluna side.

---

## Response Codes

The follow are possible response code categories that a Partner may recieve when interacting with the Toluna API. More specific codes will be found in the documentation of each API route throughout this guide.

| Code | Description |
| :--- | :--- |
| 200 | OK. The request has been processed normally without issue |
| 400 | Bad Request. Possible missing information in request or Toluna database |
| 500 | Internal Error. An error has occured within Toluna. Contact Toluna as they likely have details captured in their logs |