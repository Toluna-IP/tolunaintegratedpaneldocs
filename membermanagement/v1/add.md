---
title: Add Member
has_children: true
parent: Static (v1)
grand_parent: Member Management
nav_order: 1
---


## Adding a Member (POST)

A partner can add new members to the Toluna IP Database using an HTTP POST. This must be done by the partner before requesting or receiving survey opportunity links.

 
### Route

```plaintext
POST http://{IP-Core-URL}/IntegratedPanelService/api/Respondent
```

### Request Parameters

 - None

### Request Body Details

| Property | Description                                                     |
| :--------| :--- |
| PartnerGUID | Unique Partner Code (Please request from Toluna if you don’t have one) |
| MemberCode | Unique Respondent Code from the Partner |
| Active | (Optional) Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool. |
| GenderID | (Optional) Values from the data mapping file |
| EducationID | (Optional) Values from the data mapping file |
| IncomeID | (Optional) Values from the data mapping file |
| EthnicityID | (Optional) Values from the data mapping file |
| RaceID | (Optional) Values from the data mapping file |
| SubProvinceID | (Optional) Values from the data mapping file |
| Email | (Optional) |
| BirthDate | (Optional) MM/DD/YYYY format |
| PostalCode | (Optional) |
| IsTest | (Optional) Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used **ONLY** during testing. |

### Example Request

 ```json
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

### Possible Request Responses

| Response Code | Etiology, actions |
| :--- | :--- |
| 201 | Created. Request processed normally, resulting in a new Member Panelist |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take apporpriate action |
| 409 | Conflict. An attempt to add a Member that already exists. Duplication is determined by the combination of MemberCode and PartnerGUID |
| 500 | Internal Error. An exception occured while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs |

### Notes

> - Only new Members can be added. To update, use the PUT route noted below
> - Option Properties can be excluded from the request. "GenderID," "EducationID," "IncomeID," "EthnicityID," "RaceID," and "SubProvinceID" can also take "0" to indicate "no value."
> - Invalid Property data typically returns a 400 response

### Examples
**To-Do** Add more examples where partner adds member with varying properties

 ```json
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