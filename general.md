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


## Survey Profiles

Toluna’s client Surveys are always looking for rich profile information for all Respondents. Additional profile information for a Respondent increases the likelihood of a respondent qualifying for a Survey. Toluna provides a RESTful way to get access to these Survey Profiles that can be filled out by your Respondents.

### Route
```
**GET**  http://{IP_CORE_URL/IntegratedPanelService/api/Profile/GetNextProfileURL/
```

>Note: This request can be made multiple times. Toluna keeps track of the profiles filled by each respondent and will not offer to fill an already filled profile for a respondent.

### Request Parameters

| Name | Description |
| :--- | :--- |
| MemberCode | Unique Respondent code from the Partner |
| PartnerGUID | Unique Partner code provided by Toluna |
| cancelURl | URL the Respondent should be redirected to if they click cancel on the Profiler |
| returnURL | URL the Respondent should be redirected to if tey click save on teh Profiler |

### Possible Response Codes

| Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally; results returned without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 500 | Internal Error. An exception occurred while processing the request. Toluna likely has details captured in its logs |

### Example Response

To view a sample result, paste the following URL in your browser.

http://ups.surveyrouter.com/TrafficUI/MSCUI/Profilepage.aspx?guid=ce009f76-2076-4a16-89a1-714fe356af38&rt=9&pt=1000080&bid=200&cid=1&brandcss=1&redirect=http%3a%2f%2fwww.google.com&cancel=http%3a%2f%2fwww.google.com

This page can be hosted in an iframe on your website. When the respondent clicks save, the data will be saved on Toluna’s site and the user will be able to qualify for more surveys

---

## Branded Survey Pages

Toluna understands that it is desirable to have the Panelist experience branded to the Partner offering the invite. What the Panelist will see then is starting and ending pages that show a combination of logos, banners and copy matching the partner’s site.

### Routing Respondents

When a Respondent attempts to take a Survey they have been invited to, there are times when the Survey is no longer available (e.g. if the quota fills before the Respondent responds). The Toluna system offers the Partner and the respondent and automated routing capability in this scenario where the Respondent can be automatically routed to another Survey that the Respondent may qualify for in the system. This routing mechanism is also available to the Partner and Respondent when a Respondent terminates from a Survey as well. In both cases, the Partner is notified with the new SurveyID and Revenue amounts based on the notification HTTP POST mechanism outline [here.]() *To do: Add link to Notifications page*

#### Example Scenario

1) Respondent gets an invite for a Survey

2) Survey is closed on Toluna's end because the Respondent answered 12 hours after the invite was sent and the necessary completes were achieved.

3) If this routing is turned off, the Respondent is returned to the Partner and the Partner is notified through the Terminates Notiication method desribed [here.]() *To do: Add link to Notification page*

4) If this routing is turned on, the Terminates Notification in step 3 still occurs but the Respondent is redirected to another qualifying Survey in the Toluna platform (if a qualifying Survey is available).

5) For Partners who are getting additional Parameters on their Completions and Terminates based on the Invite will get the same Parameters on the notifications for all Surveys taken through the routing mechanism.

6) If the Respondent qualifies and completes the new Survey, the Partner is notified using the Completion notification method described [here.]() *To do: add link to Notifications page*

7) If the Respondent terminates from the new Survey, the Partner is notified through the Terminates Notiication method desribed [here.]() *To do: Add link to Notification page*

8) If the routing is turned ON, the Respondent can be offered another Survey directly from the system. The routing feature can be turned on/off at the request of the Partner within 4-8 hours during USA business hours (8am - 5pm EST).


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


---


## trackers

A "Tracker" is a series of related Surveys. Toluna calls each iteration of these Surveys a "Wave." Each iteration will share a common SurveyID and its own WaveID. Toluna recommends that the Partner considers the combination of SurveyID+WaveID as the "unique identifier" for a Member's interation with a Survey. For the complete details of trackers and their benefits, pleae refer to the main Integration Guide.
