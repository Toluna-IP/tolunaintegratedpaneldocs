---
title: Member Management
has_children: true
nav_order: 2
---

# Member Management
{: .no_toc }

For all Toluna Integration offerings, the Toluna requires partner's members to be registered on the platform.  

Toluna can receive the partner’s panel data via RESTful APIs. A partner can use these APIs to add new members or deactivate  members. 

No personal information regarding the partner’s panel is received or stored by Toluna. The partner needs only supply a unique value, “MemberCode”, that will be used to identify the member when interacting with the Toluna platform. 

Mapping Data is available via our [Reference Data API](/mapping/referencedataapi) which will aid in mapping demographic values. These values can vary by culture. 

* TOC
{:toc}

---

## Member Management Practices 

The following are important notes on the practice of Member Management:
> - All members are created in an unregulated state.
> - A Member's data regulation is immutable; once done, it is permanent.
> - All versions of the Member API support PII regulation.
>   - Once regulated, Members will no longer surface via API.
>   - Once regulated, Members are no longer eligible for survey invites. 
> - A PUT request for a regulated Member will result in "no member found."
> - A GET request for a regulated Member will result in "no member found."
> - A "GetSurveys" request for a regulated Member will result in "no member found."

---
---

## Member Status Type 
Every member that is registered on the Toluna platform has a corresponding status that indicates a general level of their ability to participate on the Toluna platform. We call this the Member Status Type, or also known as PanelistStatusType. The details of each status are outlined below. 


| PanelistStatusTypeID | Name | Description | 
| :--- | :--- | :--- |
| 1 | Registered | Member is able to participate on Toluna platform |
| 2 | OptOut | Member is opted-out of future involvement on the Toluna Platform |
| 3 | Suspended | Member is temporarily not able to participate on Toluna Platform |
| 4 | BlockedForAbuse | Member has been blocked from participating on Toluna platform |
| 5 | PII Data Regulated | Member Data obfuscated due to PII Data Regulation |



### Blocked For Abuse

An IP Member can be blocked for abuse by the Toluna Administrators due to several reasons. Some of the indicators to block a Member are multiple fraudulent attempts, multiple terminations due to Toluna Platform qualify check failure, encrypted URL mismatch, and more.

IP APIs will return 400 Bad Requests (except Member ```POST(s)```, which will return 401 Conflict) along with an appropriate message in the response. Please review the response message details and take appropriate action.

### PII Regulation

All versions of the Member API support PII regulation. For technical details, please refer to the route
documentation [v2](/membermanagement/v2/update.html#remove-personal-information)
 
After a Member is PII Regulated, Partners will no longer be able to use the [GET](/membermanagement/v1/get.html) API to retrieve the Member's data.

When PII regulation is requested, Toluna removes all data points connected to a member’s profile.


