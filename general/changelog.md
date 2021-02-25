---
title: Change Log
has_children: false
parent: General
nav_order: 10
---

# Changelog
As the platform matures, any recent changes to its behavior will be noted here. 

| Release Date | UPS Version | TEF Version | IP Version | See more details |
| :--- | :---: | :---: | :--- | :--- | :--- |
| March 1, 2020 | 15.8.7 | 3.0.1013.0 | 2.5.5 | [See more](http://example.com/){: .btn .btn-purple } |
| June 7, 2020 | 15.5.1020 | 3.0.1013.0 | 2.5.6 | [See more](http://example.com/){: .btn .btn-purple } |
| February 23, 2021 | 15.5.1289 | 3.0.1304 | 2.5.7 | [See more](http://example.com/){: .btn .btn-purple } |


## IP Version 2.5.5
### Update 
New Feature: GetQuotaDetails 

### Notes
A detailed explanation of the new feature can be found [here.](/externalsample/api/QuotaDetails.html)


## IP Version 2.5.5
### Update
New Feature: Standard Encryption

### Notes
A detailed explanation of the new feature can be found [here.](/memberrouting/encryption)


## IP Version 2.5.5
### Update
New Feature: Multiple Select/ Open-ended questions

### Notes
IP Member API v2 will now support both multipleselect and open-ended answers along with the existing single-select answers. A detailed explanation of the new change can be found [here.](/membermanagement/v2/add.html)

IP Member Add endpoint (v1 &v2): a minor change in the response message when a duplicate member add request sent for a member in blocked status. It is updated to align with our standard duplication handling process. Below is an example of the response message.

Three new Questions added to the system namely Hashed Email, Hash Type and Mobile Advertising ID.

| QuestionId        | Name         | 
|:-------------|:------------------|
| 2910040  | MobileAdvertisingID | 
| 2910041  | HashedEmail   | 
| 2910042  | HashType      | 
