---
title: Update Member
has_children: true
parent: Static (v1)
grand_parent: Member Management
nav_order: 3
---


## Member Update (PUT)

Existing Members can be updated using HTTP PUT. “PartnerGUID” and “MemberCode” are required. Combine them with optional properties to update a Member according to your requirements.

### Parameters
 - None
 
### Request Details

| Property | Description |
| :--- | :--- |
| PartnerGUID | Unique Partner Code (Please request from Toluna if you don't have one |
| MemberCode | Unique Respondent Code from the Partner (alphanumeric 256 character limit |
| Active | (Optional) Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool |
| GenderID | (Optional) Values from the data mapping file |
| EducastionID | (Optional) Values from the data mapping file |
| EthicityID | (Optional) Values from the data mapping file |
| RaceID | (Optional) Values from the data mapping file |
| SubProvinceID | (Optional) Values from the data mapping file |
| Email | (Optional) |
| BirthDate | (Optional) MM/DD/YYYY format |
| PostalCode | (Optional) |
| IsTest | (Optional) Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used **ONLY** during testing. |
| IsPIIDataRegulated | (Optional) Defaults FALSE. When TRUE, all personally identifiable information is removed. |

### Route
**PUT** http://{IP-Core-URL}/IntegratedPanelService/api/Respondent

### Possible Responses

| Response Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, existing Member Panelist was updated without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 404 | Not Found. An attempt to update a Member that does not exist. Existence is determined by the combination of MemberCode and PartnerGUID |
| 500 | Internal Error. An exception occured while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs |

### Notes
> - Only Updates Existing Members. To Add a new Member, use the POST route noted above.
> - Optional Properties can be excluded from the request. "GenderID," "EducationID," "EthnicityID," "RaceID," and "SubProvinceID" can also take "0" to indicate "no value."
> - Invalid Property data typically returns a 400 response.

### Examples
>All examples below shown in JSON

Deactivate Member
```json
{
 "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
 "MemberCode": "111",
 "Active": "false"
}
```

Change Email
```json
{
 "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
 "MemberCode": "111",
 "Email": "test@test.com"
}
```

Use Member for Testing
```json
{
 "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
 "MemberCode": "111",
 "IsTest": "true"
}
```

Remove Personal Information
```json
{
 "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
 "MemberCode": "111",
 "IsPIIDataRegulated": true
}
```
