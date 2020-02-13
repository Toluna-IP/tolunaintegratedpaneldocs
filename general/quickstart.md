---
title: Quick Start
has_children: false
parent: General
nav_order: 0
---

# Quick Start
To quickly get integrated with out platform, here's how to go about it.

# Using the Toluna Platform

Within Toluna's API, all endpoints are "culture driven," meaning that Toluna requires and organizes it's information based on a Partner's culture (a combination of language and counntry, such as "en-gb" for "English-Great Britain") and a PanelGUID (provided by Toluna).

# Dashboard 

1. Register Member to [Member Management API](/membermanagement/v2/add)
2. Provide [End Page Urls](/memberrouting/endpages) to Toluna so we can know where to send the member when Survey is over. 
3. Request Surveys for Member via [Get Surveys call](/dashboard/api/getsurveys)
4. Route Member to provided Survey Url ([Member Survey Flow](/memberrouting/membersurveyflow))

# External Sample

1. Register Member to [Member Management API](/membermanagement/v2/add)
2. Provide [End Page Urls](/memberrouting/endpages) to Toluna so we can know where to send the member when Survey is over. 
3. Request Quota Inventory from Toluna via  [Get Quotas call](/externalsample/api/getquotas)
4. Match member to survey.
5. Request Invite URL for Member to Survey via [Get Invite call](/externalsample/api/getinvite)
6. Route Member to provided Invite Url ([Member Survey Flow](/memberrouting/membersurveyflow))
