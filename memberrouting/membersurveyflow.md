---
title: Member-Survey Flow 
has_children: false
parent: Member Routing
nav_order: 1
---


# Member-Survey Flow
{: .no_toc}

---

![Member survey flow](https://github.com/josh-toluna/tolunaintegratedpaneldocs/blob/master/resources/flows/IP%20Flow%20Diagrams-Member%20Survey%20Flow.png?raw=true)

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




