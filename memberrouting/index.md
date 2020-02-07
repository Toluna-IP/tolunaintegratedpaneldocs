---
title: Member Routing
has_children: true
nav_order: 3
---


# Member Routing

---

replace below 


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






## Branded Survey Pages

Toluna understands that it is desirable to have the Panelist experience branded to the Partner offering the invite. What the Panelist will see then is starting and ending pages that show a combination of logos, banners and copy matching the partner’s site.