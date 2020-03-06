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

* TOC
{:toc}

---

## Example Scenario

1) Respondent gets an invite for a Survey

2) Survey is closed on Toluna's end because the Respondent answered 12 hours after the invite was sent and the necessary completes were achieved.

3) If this routing is turned off, the Respondent is returned to the Partner and the Partner is notified through the Terminates Notiication method desribed [here.](/notifications/memberstatus.html#terminates)

4) If this routing is turned on, the Terminates Notification in step 3 still occurs but the Respondent is redirected to another qualifying Survey in the Toluna platform (if a qualifying Survey is available).

5) For Partners who are getting additional Parameters on their Completions and Terminates based on the Invite will get the same Parameters on the notifications for all Surveys taken through the routing mechanism.

6) If the Respondent qualifies and completes the new Survey, the Partner is notified using the Completion notification method described [here.](/notifications/memberstatus.html#completions)

7) If the Respondent terminates from the new Survey, the Partner is notified through the Terminates Notiication method desribed [here.](/notifications/memberstatus.html#terminates)

8) If the routing is turned ON, the Respondent can be offered another Survey directly from the system. The routing feature can be turned on/off at the request of the Partner within 4-8 hours during USA business hours (8am - 5pm EST)
