---
title: Dynamic (v2)
has_children: false
parent: Member API
nav_order: 2
---


# V2 - Dynamic

Version 2 of the Member API is focused on speed, simplicity, improved support for demographic characteristics. It’s “closer to the metal” of the underlying Toluna Panel Management System and is optimized to remove internal dependencies. To the Partner, it’s faster and has more capability. It is independent of Static v1 and is managed separately. For the time being, both versions will continue to exist and be supported. To access v2 of a route, supply the “Accept” header in your request as directed below.

## Question / AnswerIDs
Please note the primary difference with v1 is that demographic characteristics are listed as a series of Question and Answer IDs. Though less readable in JSON notation, this provides true extensibility (all Toluna Demographic information is supported), and provides for much faster results. Every Question has a static QuestionID, which maps to a series of possible static AnswerIDs. This information is clearly noted in the mapping document each partner receives during the integration period. These are the most relevant Questions for IP:

| Question Name | QuestionID | Possible AnswerIDs |
| :-- | :--- | :--- |
| GenderID | 1001007 | See mapping document |
| EducationID | 1001101 | See mapping document |
| IncomeID | 1001107 | See mapping document |
| EthnicityID | 1001012 | See mapping document |
| WorkPositionID | 1005145 | See mapping document |
| MaritalStatusID | 1001102 | See mapping document |
| EmploymentStatusID | 1012395 | See mapping document |
| RaceID | 1002790 | See mapping document |

## Member Add / POST

#### Headers

All requests made using Dynamic member management (v2) must include the following header:
```json
Accept: application/json;version=2.0
```

#### Request Details

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

#### Route
POST http://{IP-Core-URL}/IntegratedPanelService/api/Respondent

#### Possible Responses

| Response Code | Etiology, actions |
| :--- | :--- |
| 201 | Created. Request processed normally, resulting in a new Member |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 409 | Conflict. An attempt to add a Member that already exists. Duplication is determined by the combination of MemberCode and PartnerGUID |
| 500 | Internal Error. An exception occurred while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs |

#### Notes
> - Only new Members can be added. To update, use the PUT route noted below
> - Invalid Property data typically returns a 400 response that contains explanation for the rejection

#### Example
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
