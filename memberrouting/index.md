---
title: Member Routing
has_children: true
nav_order: 3
---


# Member Routing
{: .no_toc}

* TOC
{:toc}

---

[in progress]

## Routing Respondents

When a Respondent attempts to take a Survey they have been invited to, there are times when the Survey is no longer available (e.g. if the quota fills before the Respondent responds). The Toluna system offers the Partner and the respondent and automated routing capability in this scenario where the Respondent can be automatically routed to another Survey that the Respondent may qualify for in the system. This routing mechanism is also available to the Partner and Respondent when a Respondent terminates from a Survey as well. In both cases, the Partner is notified with the new SurveyID and Revenue amounts based on the notification HTTP POST mechanism outline [here.](/notifications/memberstatus)

---

## AutoRouting

Toluna allows Members to be automatically routed to a separate Survey when they attempt to connect to a Survey that is no longer available or that they no longer qualify for. When a Member is AutoRouted, the Partner will NOT recieve a Terminated notification. Instead, Partner's will receive a Notification when the Member completes the Survey to which they were routed. Included in this Notification will be the following addendum:

```
...
"IsAutoRouted": true,
"OriginalSurveyID": {OriginalSurveyID}
...
```

Where the "OriginalSurveyID" will the SurveyID of the Survey from which the Member was Routed (typically the Survey to which they received the link from the Partner).

This feature is not automatically enabled when a Partner connects with Toluna's Integrated Panel Platform. To enable this feature, please contact your Toluna representative.


---

## Routing Options

When autorouting Respondents, Partners have two options for their end pages: Self-Hosted or Toluna-Hosted.

### Self-Hosted Pages

This is the standard and most desired option for Partners. The specific events required Partner-Hosted pages are outlined [here.]\(memberrouting\endpages)

### Toluna-Hosted Pages

Toluna understands that it is desirable to have the Panelist experience branded to the Partner offering the invite. What the Panelist will see then is starting and ending pages that show a combination of logos, banners and copy matching the partner’s site.