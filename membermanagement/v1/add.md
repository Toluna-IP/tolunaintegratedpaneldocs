---
title: Add Member
has_children: false
parent: Static (v1)
grand_parent: Member Management
nav_order: 1
---


# Adding a Member (POST)
{: .no_toc }

A partner can add new members to the Toluna IP Database using an HTTP POST. This must be done by the partner before requesting or receiving survey opportunity links.

* TOC
{:toc}

---

## Request

### Route

```plaintext
POST http://{IP_CORE_URL}/IntegratedPanelService/api/Respondent
```

### Parameters

 - None
 
### Header
 - None

### Body Details

| Property | Description | Required? |
| :--------| :--- | :---: |
| PartnerGUID | Unique Partner Code (Please request from Toluna if you don’t have one) | Yes |
| MemberCode | Unique Respondent Code from the Partner | Yes |
| Active | Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool. | No |
| GenderID | Values from the [Reference Data API](/mapping/referencedataapi/) | No |
| EducationID | Values from the [Reference Data API](/mapping/referencedataapi/) | No |
| IncomeID | Values from the [Reference Data API](/mapping/referencedataapi/) | No |
| EthnicityID | Values from the [Reference Data API](/mapping/referencedataapi/) | No |
| RaceID | Values from the [Reference Data API](/mapping/referencedataapi/) | No |
| SubProvinceID | Values from the [Reference Data API](/mapping/referencedataapi/) | No |
| Email | Member email | No |
| BirthDate | MM/DD/YYYY format | No |
| PostalCode | Member postal code | No |
| IsTest | Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used **ONLY** during testing. | No |

### Example

 ```plaintext
{
 "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",  
 "MemberCode": "111", 
 "Active": "true", 
 "GenderID": "2000247", 
 "EducationID": "2002275", 
 "IncomeID": "2796381", 
 "EthnicityID": "2000264",
 "RaceID": "0", 
 "Email": "test@test.com", 
 "BirthDate": "6/21/1914", 
 "PostalCode": "OU812", 
 "SubProvinceID": "3091832"
}
```

---

## Responses

### Possible Codes

| Response Code | Etiology, actions |
| :--- | :--- |
| 201 | Created. Request processed normally, resulting in a new Member Panelist |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 409 | Conflict. An attempt to add a Member that already exists. Duplication is determined by the combination of MemberCode and PartnerGUID |
| 500 | Internal Error. An exception occurred while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs |

### Notes

> - Only new Members can be added. To update, use the PUT route noted below
> - Option Properties can be excluded from the request. "GenderID," "EducationID," "IncomeID," "EthnicityID," "RaceID," and "SubProvinceID" can also take "0" to indicate "no value."
> - Invalid Property data typically returns a 400 response

### Examples
**To-Do** Add more examples where partner adds member with varying properties

 ```plaintext
{
 "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",  
 "MemberCode": "111", 
 "Active": "true", 
 "GenderID": "2000247", 
 "EducationID": "2002275", 
 "IncomeID": "2796381", 
 "EthnicityID": "2000264",
 "RaceID": "0", 
 "Email": "test@test.com", 
 "BirthDate": "6/21/1914", 
 "PostalCode": "OU812", 
 "SubProvinceID": "3091832"
}
```
