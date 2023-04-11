---
title: Integration Details 
has_children: false
nav_order: 1
parent: Dashboard Offering
---


# Dashboard Integration Details
{: .no_toc }

* TOC
{:toc}

---

## What is the Flow?

The basic flow of the Dashboard integration is to first use the [Member Management API](/membermanagement/) to register a member with as many attributes as known to the partner. Then, the [GetSurveys Call](/dashboard/api/getsurveys.html) will be used to pull a list of surveys for which the member is eligible. This list can be used as the discetion of the Partner and may provide varying opportunities upon subsequent calls.
