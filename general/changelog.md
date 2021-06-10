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
| June 13, 2021 | **replace** | **replace** | **replace** | [See more]
| February 23, 2021 | 15.5.1289 | 3.0.1304 |  2.5.7  | [See more](/general/changelog.html#257){: .btn .btn-green } |
| June 7, 2020 | 15.5.1020 | 3.0.1013.0 |  2.5.6 | [See more](/general/changelog.html#256){: .btn .btn-green } |
| March 1, 2020 | 15.8.7 | 3.0.1013.0 |  2.5.5 | [See more](/general/changelog.html#255){: .btn .btn-green } |


## **replace**
### Changes

• (Change) [Standard Encryption](\memberrouting\encryption.html) has been expanded to enclude encryption of all end page redirects. For a list of our redirect events, please click [here.](\memberrouting\endpages.html)
> Note: If Standard Encryption was enabled for your integration prior to this update, you will be automatically opted in to encrypt all redirects. If for any reason this cannot be supported on your end, please contact your Toluna Business Representative.
 

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

