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
|:---|:---|:---|
| What it is | A way for the partner to request and display a list of survey opportunities for panel members and route them via invite URLs. | A more flexible integration where the partner directly integrates with APIs |
| Control of Sampling | Sampling and routing logic handled by Toluna through the dashboard | Partners have full control over sampling and routing logic |
| API Used | Dashboard API (e.g., Gateway APIs) | External Sample API (Gateway APIs) |
| Routing Logic | Toluna’s router determines which surveys are shown to users | Partner determines which surveys are routed to users |
| Realtime Quota Information | Not available — dashboard-based visibility only | Realtime open quota details available through APIs |
| Level of Partner Effort | Lower effort — partner uses prebuilt workflows and UI | Higher effort — partner responsible for building and maintaining integration |
| Member Management Required | Yes — partner must manage member authentication and identity | Yes — partner must manage member authentication and identity |
| End Pages & Notifications | Required: End pages must be implemented by the partner | Required: End pages must be implemented by the partner |
| Quota / Survey Status Notifications | Optional (highly recommended) | Optional (highly recommended) |
| Best Fit / Use Case | Quick endpoint to show available surveys with minimal implementation effort | Custom quota targeting, custom routing logic, and advanced integrations |

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

