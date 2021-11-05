---
title: Change Log
has_children: false
parent: General
nav_order: 10
---

# Changelog
As the platform matures, any recent changes to its behavior will be noted here. 

| Release Date | UPS Version | TEF Version | IP Version |    |
| :--- | :---: | :---: | :--- | :--- | :--- |
| November 7, 2021 | 15.5.1516 | 3.0.1477 | 2.5.8 | Improved Geo Computation for Registered Members, Minor bug fixes, and platform optimization |
| July 18, 2021 | 15.5.1454 | 3.0.1359 | 2.5.8 | Minor bug fixes and platform optimization |
| June 20, 2021 | 15.5.1425 | 3.0.1359 | 2.5.8 | [See more](/general/changelog.html#258){: .btn .btn-green } |
| May 23, 2021 | 15.5.1393 | 3.0.1330 | 2.5.7 | Minor bug fixes and platform optimization |
| May 2, 2021 | 15.5.1361 | 3.0.1330 | 2.5.7 | Minor bug fixes and platform optimization |
| February 23, 2021 | 15.5.1289 | 3.0.1304 |  2.5.7  | [See more](/general/changelog.html#257){: .btn .btn-green } |
| June 7, 2020 | 15.5.1020 | 3.0.1013.0 |  2.5.6 | [See more](/general/changelog.html#256){: .btn .btn-green } |
| March 1, 2020 | 15.8.7 | 3.0.1013.0 |  2.5.5 | [See more](/general/changelog.html#255){: .btn .btn-green } |


## 2.5.8
### Changes

• (Change) [Standard Encryption](/memberrouting/encryption.html) now applies to all redirect URLs. For full list of end page scenarios, please click [here](/memberrouting/endpages.html).
> Note: If you had encryption enabled in your API Instance, you will be automatically upgraded to the enhanced encrytion. To opt out of this, please contact your Toluna Business Representative.

• (Change) [PreStart Notifications](/notifications/prestart.html) now available to partners utilizing the [Dashboard API](/dashboard/integrationdetails.html). To opt in to these Notifications, please contact your Toluna Business Representative.

• (New Feature) Enhanced Terminate Notifications: [Terminate Notifications](/notifications/memberstatus.html#terminates) can now include additional objects defining the nature of the respondent's rejection. Top opt-in, please contact your Toluna Representative. If opted-in, parameters will also be automatically added to End Pages. Please see [Enhanced Terminate Parameters](/memberrouting/endpages.html#enhanced-terminate-parameter) for more details.


## 2.5.7
### Changes


• (New Feature) IP Member API v2 will now support both multipleselect and open-ended answers along with the existing single-select answers. A detailed explanation of the new change can be found [here.](/membermanagement/v2/add.html)

• (Change) IP Member Add endpoint (v1 &v2): a minor change in the response message when a duplicate member adds a request sent for a member in blocked status. It is updated to align with our standard duplication handling process. Below is an example of the response message.

_An IP Member for MemberCode {MemberCode} and PartnerGUID {PartnerGUID} already exists. To update a Member, please use the PUT verb._


• Three new Questions were added to the system, namely Hashed Email, Hash Type, and Mobile Advertising ID.

| QuestionId        | Name         | 
|:-------------|:------------------|
| 2910040  | MobileAdvertisingID | 
| 2910041  | HashedEmail   | 
| 2910042  | HashType      | 


## 2.5.6
### Changes
#### • New Feature: Standard Encryption

• A detailed explanation of the new feature can be found [here.](/memberrouting/encryption)



##  2.5.5
### Changes 
#### • New Feature: GetQuotaDetails 

• A detailed explanation of the new feature can be found [here.](/externalsample/api/QuotaDetails.html)

