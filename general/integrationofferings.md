---
title: Integration Offerings
has_children: false
parent: General
nav_order: 1
---

# Integration offerings
{: .no_toc}

We offer several ways to integrate into our platform and they are listed below. Each of these has their own approaches and require varying levels of technical approaches and connection points. Please consult with a Toluna representative on which offering is most appropriate for the Partner's Integration. The tables at the bottom of this page can also add some insight on the differences between the three integration offerings.

---

* TOC
{:toc}

---


## [Dashboard Offering](\dashboard)

This offering allows Partners to request a small inventory of current survey opportunities for a member. The Partner then routes the member accordingly to the opportunity through the provided invite URL. 


## [External Sample Offering](\externalsample)

This is the newest offering and places the sampling processs (member -> survey selection) to the partner. The partner requests a real-time inventory of available quotas, selects which members qualify for which quotas, and then requests invite URLs for these member-quota pairs. Once an invite URL is provided back by the Toluna platform, the partner can route the member accordingly. 


## Which integration is best for you?

| Feature / Capability | Dashboard Offering | External Sample Offering |
| :--- | :--- | :--- |
| What it is | A way for the partner to manage sampling and routing through a dashboard | A more flexible integration using APIs |
| Control of Sampling | Sampling and routing logic handled through the dashboard | Partners have full sampling control |
| API Used | Dashboard API (e.g., Dashboard endpoints) | External Sample API |
| Routing Logic | Toluna’s router determines routing | Partner determines which surveys to route |
| Realtime Quota Information | Not available — dashboard-based | Realtime open quota details available |
| Level of Partner Effort | Lower effort — partner uses dashboard workflows | Higher effort — partner builds integration logic |
| Member Management Required | Yes — partner must manage members | Yes — partner must manage members |
| End Pages & Notifications | Required: End pages | Required: End pages |
| Quota / Survey Status Notifications | Optional (highly recommended) | Optional (highly recommended) |
| Best Fit / Use Case | Quick endpoint to show available surveys | Custom quota targeting and advanced routing |

---

## Offering-specific Integration Requirements

### Components 

|  | Dashboard | External Sample |
| :--- | :---: | :---: | :---: |
| [Member Management](\membermanagement) | Required | Required |
| [End Pages](\memberrouting\endpages) | Recommended | Recommended |
| [Dashboard API](\dashboard) | Required | - |
| [External Sample API](\externalsample\api) | - | Required |
| [Reference Data API](\mapping\referencedataapi\) | Recommended | Recommended |

<br>

### [Notifications](\notifications) 

|   | Dashboard | External Sample |
| :--- | :---: | :---: | :---: |
| [Survey Closed](/notifications/surveyclosed.html)  | Recommended | Recommended |
| [Member-Status](/notifications/memberstatus.html)  | Recommended | Recommended |
| [Quota Status](/notifications/quotastatus.html)   | Optional | Recommended  |
| [Pre-Start](/notifications/etns.html)  | Recommended | Recommended |


---

