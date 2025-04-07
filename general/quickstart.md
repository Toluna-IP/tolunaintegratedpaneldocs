---
title: Quick Start
has_children: false
parent: General
nav_order: 0
---

# Quick Start
Below are steps to quickly get integrated with Toluna's platform depending on the Integration Offering. If you are an existing Partner and would like help improving your integration, please see our [Best Practices Guide](/general/bestpractices.html). 

In all cases, API access to the platform will have to be given by Toluna representatives.


# Dashboard 

1. Register Member to [Member Management API](/membermanagement/v2/add)
2. Provide [End Page Urls](/memberrouting/endpages) to Toluna so we can know where to send the member when Survey is over. 
3. Request Surveys for Member via [Get Surveys call](/dashboard/api/getsurveys)
4. Route Member to provided Survey Url ([Member Survey Flow](/memberrouting/membersurveyflow))

# External Sample

1. Register Member to [Member Management API](/membermanagement/v2/add)
2. Provide [End Page Urls](/memberrouting/endpages) to Toluna so we can know where to send the member when Survey is over
3. Request Quota Inventory from Toluna via  [Get Quotas call](/externalsample/api/getquotas)
4. Match member to survey, in accordance with [Sampling Rules](/externalsample/samplingrules.html)
5. Request Invite URL for Member to Survey via [Get Invite call](/externalsample/api/generateinvite)
6. Route Member to provided Invite Url ([Member Survey Flow](/memberrouting/membersurveyflow))
