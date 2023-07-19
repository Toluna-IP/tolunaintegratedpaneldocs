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

## Informational Video

<video class="video-fluid z-depth-1" loop controls muted style="width: 80%;">
  <source src="https://firebasestorage.googleapis.com/v0/b/toluna-ip.appspot.com/o/integration%2Fquick%2FRedirect%20and%20Notifiation%20URLs.mp4?alt=media&token=996c1c08-4520-4aa2-9a5c-896a88b28800" type="video/mp4" />
</video>


## Routing Respondents

When a Respondent attempts to take a Survey they have been invited to, there are times when the Survey is no longer available (e.g. if the quota fills before the Respondent responds). The Toluna system offers the Partner and the respondent and automated routing capability in this scenario where the Respondent can be automatically routed to another Survey that the Respondent may qualify for in the system. This routing mechanism is also available to the Partner and Respondent when a Respondent terminates from a Survey as well. In both cases, the Partner is notified with the new SurveyID and Revenue amounts based on the notification HTTP POST mechanism outline [here.](/notifications/memberstatus)

---

## AutoRouting

Toluna allows Members to be automatically routed to a separate Survey when they attempt to connect to a Survey that is no longer available or that they no longer qualify for. When a Member is AutoRouted, the Partner will NOT receive a Terminated notification. Instead, Partner's will receive a Notification when the Member completes the Survey to which they were routed. Included in this Notification will be the following addendum:

```
...
"IsAutoRouted": true,
"OriginalSurveyID": {OriginalSurveyID}
...
```

Where the “OriginalSurveyID” will be the SurveyID of the Survey from which the Member was Routed (typically the Survey to which they received the link from the Partner).

This feature is not automatically enabled when a Partner connects with Toluna's Integrated Panel Platform. To enable this feature, please contact your Toluna representative.


---

## Routing Options

In order to route respondents accordingly, partners will need to provide endpages for their users to return to upon completing the survey flow. The specific events required for Partner-Hosted pages are outlined [here.](\memberrouting\endpages)

