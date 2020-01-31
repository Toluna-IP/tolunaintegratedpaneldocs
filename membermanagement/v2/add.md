---
title: Add Member
has_children: true
parent: Dynamic (v2)
grand_parent: Member Management
nav_order: 1
---


## Member Add / POST

### Headers

{: .label .label-red }
IMPORTANT

All requests made using Dynamic member management (v2) must include the following header:
```json
Accept: application/json;version=2.0
```

### Route

```plaintext
POST http://{IP-Core-URL}/IntegratedPanelService/api/Respondent
```

### Request Parameters
 - None
 

### Request Body Details

| Property | Description |
| :--- | :--- |
| PartnerGUID | Unique Parnter Code (Please request from Toluna if you don't have one) |
| MemberCode | Unique Respondent Code from the Partner |
| IsActive | (Optional) Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool |
| Email | (Optional) NOTE: when supplied, this must have a valid email format |
| BirthDate | (Optional) MM/DD/YYYY format |
| PostalCode | (Optional) |
| IsTest | (Optional) Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used **ONLY** during testing. |
| IsPIIDataRegulated | (Optional) Defaults FALSE. When TRUE, all personally identifiable information is removed. |
| AnsweredQuestions | (Optional) A collection of 0:M demographic Question and Answer ID pairs, |

### Example Request

```json
{
 "PartnerGUID": "93A6D55C-D4E7-49FC-8D68-671165ADE463",
 "MemberCode": "AUniquePartnerCode",
 "Email": "member@yopmail.com",
 "BirthDate": "6/21/1992",
 "PostalCode": "15235",
 “IsPIIDataRegulated”: false
 "AnsweredQuestions":
   [
    {"QuestionID":1001007,"AnswerID":2000247},
    {"QuestionID":1001101,"AnswerID":2002275},
    {"QuestionID":1001107,"AnswerID":2002330},
    {"QuestionID":1001012,"AnswerID":2000270},
    {"QuestionID":1005145,"AnswerID":2796316},
    {"QuestionID":1001102,"AnswerID":2002280},
    {"QuestionID":1012395,"AnswerID":3056609}
   ]
}
```


### Possible Request Responses

| Response Code | Etiology, actions |
| :--- | :--- |
| 201 | Created. Request processed normally, resulting in a new Member |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 409 | Conflict. An attempt to add a Member that already exists. Duplication is determined by the combination of MemberCode and PartnerGUID |
| 500 | Internal Error. An exception occurred while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs |


### Notes

> - Only new Members can be added. To update, use the PUT route noted below
> - Invalid Property data typically returns a 400 response that contains explanation for the rejection

### Examples
**To-do** add more examples where partner adds member with varying properties

