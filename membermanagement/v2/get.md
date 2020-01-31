---
title: Get Member
has_children: true
parent: Dynamic (v2)
grand_parent: Member Management
nav_order: 2
---



## Member Get
Adds new Members to the Toluna IP database using an HTTP POST

URL to **GET** member info: http://{IP-Core-URL}/IntegratedPanelService/api/Respondent


### Headers

{: .label .label-red}
IMPORTANT

All requests made using Dynamic member management (v2) must include the following header:
```json
Accept: application/json;version=2.0
```

### Request Parameters

| Name | Description |
| :--- | :--- |
| memberCode | Unique Respondent Code from the Partner |
| partnerGUID | Unique Partner Code (Please request this from Toluna if you don't have one) |




### Route
```plaintext
GET http://{IP-Core-URL}/IntegratedPanelService/api/Respondent/?memberCode={memberCode}&partnerGUID={partnerGUID}
```

### Possible Request Responses

| Response Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, existing Member Panelist was updated without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 500 | Internal Error. An exception occurrec while processing the request. Contact Toluna for resolution. Toluna will likely have the details caputred in its logs |

### Example Response
```
 {
  "PartnerGUID": "93A6D55C-D4E7-49FC-8D68-671165ADE463",
  "MemberCode": "AUniquePartnerCode",
  "Email": "member@yopmail.com",
  "BirthDate": "6/21/1992",
  "PostalCode": "15235",
  "IsPIIDataRegulated": false,
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
