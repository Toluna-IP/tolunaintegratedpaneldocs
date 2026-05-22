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
|---|---|---|
| What it is | A way for the partner to request and display a list of survey opportunities for panel members and route them via invite URLs. | A more flexible integration where the partner obtains real-time quota data and uses their own sampling logic to match members to quotas. |
| Control of Sampling | Sampling and routing logic stays largely with Toluna — partners request surveys and show them. | Partners have full sampling control — request open quotas, pick the best target respondents, then get invite URLs. |
| API Used | Dashboard API (e.g., GetSurveys) to pull available surveys for a member. | External Sample API (GetQuotas, GenerateInvite, etc.) to receive quotas and invite links. |
| Routing Logic | Toluna’s router determines which survey links to serve based on eligibility | Partner determines which panelist fits which Toluna quota, then Toluna returns an invite |
| Realtime Quota Information | Not available — dashboard returns surveys that are cached for ~1 minute (no live quota state). | Realtime open quota details — partners can evaluate quotas before inviting respondents. |
| Level of Partner Effort | Lower effort — partner calls API, gets list of surveys, and routes respondent. | Higher effort — partner must manage quota logic and targeting. |
| Member Management Required | Yes — partner must manage and update member details using Member Management API | Yes — partner must manage and update member details using Member Management API |
| End Pages & Notifications | Required: End pages; Optional (highly recommended): Notifications | Required: End pages; Optional (highly recommended): Notifications |
| Quota/ Survey Status Notifications | Optional | Optional (highly recommended) since quotas drive invitation logic |
| Best Fit / Use Case | Quick endpoint to show surveys | Custom quota targeting and control over who gets invited |

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

