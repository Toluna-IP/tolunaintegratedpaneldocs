---
title: General
has_children: true
nav_order: 1
---

# General
{: no_toc}

* TOC
{:toc}

---



---

## "Tracking" Surveys and the WaveID Property

A “Tracker” is a series of related surveys. Toluna calls each iteration of these Surveys a “Wave”. From the Respondent’s perspective, each Wave is experienced like an individual Survey. To the Partner, each Wave of a Tracker carries its own “WaveID” but shares a common SurveyID. All new partners are opted-in to use WaveID by default. WaveID will appear on Invites, Reports, Redirects, and in all Notifications (completion, termination, and surveyClosed).

### Benefits of Using WaveID

Since each iteration of the Tracker shares the same SurveyID, a Survey can be interpreted as duplicate if the WaveID is not included. Including WaveID eliminates the potential for "false duplicates" and increases the number of invites and the potential for a corresponding increase in completes.

### Removing WaveID from Your Integration Profile

toluna recommends that the Partner considers the combination of SurveyID+WaveID as the "unique identifier" for a Respondent's interaction with a Survey. If you wish to remove WaveID from your profile, please contact your Toluna representative. This requires a simple configuration change on the Toluna side.

---

## Blocked For Abuse

An IP Member can be blocked for abuse by the Toluna Administrators due to several reasons. Some of the indicators to block a Member are multiple fraudulent attempts, multiple terminations due to internal qualify check failture, encrypted URL mismatch, and more.

IP APIs will return 400 Bad Requests (except Member ```POST(s)```, which will return 401 Conflict) along with an appropriate message in the response when a request is received for a Member in a blocked status. Please review the response message details and take appropriate action.


