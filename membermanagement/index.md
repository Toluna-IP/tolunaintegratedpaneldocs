---
title: Member API
has_children: true
nav_order: 1
---

# Member Management API 

Integrated Panel (IP) is an offering for our partners that allow them to receive a request to invite their own panel to Toluna      surveys that have demographics (Age, Gender, Country, and Language etc.) that will match those of the individual panelist.

No personal information regarding the partner’s panel is received or stored by Toluna. The partner need only supply a unique    numeric “Member ID” that will be passed back to them when an invite is made.  

Toluna can receive the partner’s panel data via RESTful APIs. A partner can use these APIs to add new members or deactivate    members. Please request the mapping values for the demographics from your Toluna account representative. Most values vary by    country. The API details are outlined below.

>The following are important notes on the practice of Member Management:
> - All members are created in an unregulated state.
> - A Member's data regulation is immutable; once done, it is permanent.
> - All versions of the Member API support PII regulation.
>   - Once regulated, Members will no longer surface via API.
>   - Once regulated, Members are no longer eligible for survey invites. 
> - A PUT request for a regulated Member will result in "no member found."
> - A GET request for a regulated Member will result in "no member found."
> - A "GetSurveys" request for a regulated Member will result in "no member found."
