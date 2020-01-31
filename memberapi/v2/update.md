---
title: Update Member
has_children: true
parent: Dynamic (v2)
grand_parent: Member API
nav_order: 3
---


## Member Update / PUT

Existing Members can be updated using HTTP PUT. “PartnerGUID” and “MemberCode” are required. Combine them with optional properties to update a Member according to your requirements.

### Request Parameters

 - None
 
### Headers

All requests made using Dynamic member management (v2) must include the following header:
```json
Accept: application/json;version=2.0
```

### Request Details

| Property | Description |
| :--- | :--- |
| PartnerGUID | Unique Partner Code (Please request from Toluna if you don’t have one) |
| MemberCOde | Unique Respondent Code from the Partner |
| IsActive | (Optional) Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool.|
| Email | (Optional) NOTE: When Supplied, this must have a valid email format |
| BirthDate | (Optional) MM/DD/YYYY format |
| PostalCode | (Optional) |
| IsTest | (Optional) Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used **ONLY** during testing. |


### Request Parameters

 - None
 
### Route

```plaintext
PUT http://{IP-Core-URL}/IntegratedPanelService/api/Respondent
```

### Possible Request Responses

| Response Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, existing Member Paneling was updated without issue |
| 400 | Bad Request. Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 404 | Not Found. An attempt to update a Member that does not exist. Existence is determined by the combination of MemberCode and PartnerGUID |
| 500 | Internal Error. An exception occurred while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs |


### Notes

> - Only updates existing members. To add a new Member, use thne POST route noted [here]().
> - Optional Properties can be excluded from the request. "GenderID," "EducationID," "EthnicityID," "RaceID," and "SubProvinceID" can also take "0" to indicate "no value."
> - Invalud Property data typically returns a 400 response.

### Examples

Deactivate Member
```json
 {
  "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "MemberCode": "111",
  "IsActive": "false"
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
 
 Change Member EducationID
 ```json
 {
  "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "MemberCode": "111",
  "AnsweredQuestions":
    [
     {"QuestionID":1001101,"AnswerID":2796531}
   ]
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
