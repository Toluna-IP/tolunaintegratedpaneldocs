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

## [Notification Offering](\notification)

This is the original integration offering in which Toluna performs the sampling and sends [Invite Notifications](/notifications/invite.html) to the Partner and they are able to pass along the opportunity to the member.


## [Dashboard Offering](\dashboard)

This offering allows Partners to request a small inventory of current survey opportunities for a member. The Partner then routes the member accordingly to the opportunity through the provided invite URL. 


## [External Sample Offering](\externalsample)

This is the newest offering and places the sampling processs (member -> survey selection) to the partner. The partner requests a real-time inventory of available quotas, selects which members qualify for which quotas, and then requests invite URLs for these member-quota pairs. Once an invite URL is provided back by the Toluna platform, the partner can route the member accordingly. 

---

## Offering-specific Integration Requirements

### Components 

|  | Notification | Dashboard | External Sample |
| :--- | :---: | :---: | :---: |
| [Member Management](\membermanagement) | Required | Required | Required |
| [End Pages](\memberrouting\endpages) | Required | Required | Required |
| [Dashboard API](\dashboard) | - | Required | - |
| [External Sample API](\externalsample\api) | - | - | Required |
| [Reporting API](\reporting) | Optional | Optional | Optional |

<br>

### [Notifications](\notifications) 

|  | Notification | Dashboard | External Sample |
| :--- | :---: | :---: | :---: |
| Invite | Required | - | - |
| Survey Closed | Recommended | Recommended | Recommended |
| Member-Status  | Recommended | Recommended | Recommended |
| Quota Status  | - | - | Required  |
| Pre-Start  | - | - | Recommended |


---

