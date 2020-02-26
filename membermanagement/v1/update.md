---
title: Update Member
has_children: false
parent: Static (v1)
grand_parent: Member Management
nav_order: 3
---


# Member Update (PUT)
{: .no_toc }

Existing Members can be updated using HTTP PUT. “PartnerGUID” and “MemberCode” are required. Combine them with optional properties to update a Member according to your requirements.


* TOC
{:toc}

---

## Request

### Route
```plaintext
PUT http://{IP_CORE_URL}/IntegratedPanelService/api/Respondent
```

### Parameters
 - None
 
### Body Details

| Property | Description | Required? |
| :--- | :--- | :---: |
| PartnerGUID | Unique Partner Code (Please request from Toluna if you don't have one | Yes |
| MemberCode | Unique Respondent Code from the Partner (alphanumeric 256 character limit | Yes |
| Active | Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool | No |
| GenderID | Values from the data mapping file | No |
| EducationID | Values from the data mapping file | No |
| EthicityID | Values from the data mapping file | No |
| RaceID | Values from the data mapping file | No |
| SubProvinceID | Values from the data mapping file | No |
| Email | Member email | No |
| BirthDate | MM/DD/YYYY format | No |
| PostalCode | Member postal code | No |
| IsTest | Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used **ONLY** during testing | No |
| IsPIIDataRegulated | Defaults FALSE. When TRUE, all personally identifiable information is removed. | No |

>Note: only the information being updated needs to be included in the request (i.e. education, , active, IsPIIDataRegulated, etc)

### Examples

All examples below shown in JSON

#### Deactivate Member
```plaintext
{
 "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
 "MemberCode": "111",
 "Active": "false"
}
```

#### Change Email
```plaintext
{
 "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
 "MemberCode": "111",
 "Email": "test@test.com"
}
```

#### Use Member for Testing
```plaintext
{
 "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
 "MemberCode": "111",
 "IsTest": "true"
}
```

#### Remove Personal Information
```plaintext
{
 "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
 "MemberCode": "111",
 "IsPIIDataRegulated": true
}
```

---

## Responses

### Possible Codes

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