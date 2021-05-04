---
title: Integration Details 
has_children: false
nav_order: 1
parent: External Sample Offering
---


# ES Integration Details
{: .no_toc }

* TOC
{:toc}

---

## How is ES Different than other offerings?

Toluna’s “External Sample” (ES) capability is an integration option offered as part of the Integrated Panel program. Its adoption permits the Partner to receive near real-time details about Toluna’s open quotas. Once obtained, Partners can use their own sampling capabilities to target the most appropriate respondents. This differs from the traditional IP model where Toluna maintains complete control over the sampling, routing, and invitation processes.

---

## What is the Standard ES Flow?

Within the realms of the ES Offering, there are two kinds of Quotas Toluna uses with its Partners. The first is the Standard Quota, similar to our traditional offerings, but with ES-specific parameters. The second kind is the Recontact Quota, the definition of which will be explained further below. Detailed information on the Standard Flow can be found [here.](\externalsample\standardflow)

---

## "Recontact" Flow for ES

At times, Toluna will seek to “reconnect” specific Members for a Quota. Typically this is done to facilitate follow-up information for an original study. Since the target Members are already known, the partner has no requirement to sample its membership for the Quota. Instead, they query a Toluna API which will return the list of MemberCodes applicable for recontact. Once obtained, the Partner should sample the list against the Recontact Quota to validate the targeting and generate an invite request for each match. From here, the process is identical to the interaction with a typical Quota.

Detailed information on the Recontact Flow can be found [here.](\externalsample\recontactflow "Recontact ES Flow")
