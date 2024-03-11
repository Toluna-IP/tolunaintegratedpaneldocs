---
title: Get Member
has_children: false
parent: Dynamic (v2)
grand_parent: Member Management
nav_order: 2
---



# Member GET
{: .no_toc}

A partner can receive details for members in the Toluna IP database using an HTTP **GET**.

* TOC
{:toc}

---

## Request

### Route
```plaintext
GET https://{IP_CORE_URL}/IntegratedPanelService/api/Respondent/?memberCode={memberCode}&partnerGUID={partnerGUID}
```

### Parameters

| Name | Description | Required? |
| :--- | :--- | :---: |
| memberCode | Unique Respondent Code from the Partner | Yes |
| partnerGUID | Unique Partner Code (Please request this from Toluna if you don't have one) | Yes |

### Headers

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| ```Accept: application/json;version=2.0``` | ```string``` | Declaration of api version | Yes |


### Body Details 
 - None

---

## Response

### Possible Codes

| Response Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, existing Member Panelist was updated without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 500 | Internal Error. An exception occurred while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs |

### Body Details

| Property | Description | Type | Required? |
| :--- | :--- | :--- | :---: |
| PartnerGUID | ```GUID``` | Unique Partner Code (Please request from Toluna if you don’t have one) | Yes |
| MemberCode | ```string``` | Unique Respondent Code from the Partner | Yes |
| IsActive | ```bool``` | Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool.| No |
| BirthDate | ```string``` | YYYY-MM-DD format | No |
| PostalCode | ```string``` | Member postal code | No |
| IsTest | ```bool``` | Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used **ONLY** during testing | No |
| IsPIIDataRegulated | ```bool``` | Defaults FALSE. When TRUE, all personally identifiable information is removed | No |
| AnsweredQuestions | A collection of 0:M demographic Question and Answer ID pairs - **Currently available - will be marked as "obsolete" and deprecated in an year**  | |
| RegistrationAnswers | Supports multi-select and open-ended answers. This will also maintain current single select responses |

### 200 Response - AnsweredQuestions
```
 {
  "PartnerGUID": "93A6D55C-D4E7-49FC-8D68-671165ADE463",
  "MemberCode": "AUniquePartnerCode",
  "BirthDate": "1987-01-25",
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

### 400 Response
```
{
  "Message": "No member found with member code AUniquePartnerCode and partner Guid 93A6D55C-D4E7-49FC-8D68-671165ADE463"
}
```



AnsweredQuestions and RegistrationAnswers will contain the same member responses, and Partner can use their choice. If Partner wants to supply multi-select and open-ended, then using RegistrationAnswers in all the methods will be appropriate.
Sample GET response:

### Example - RegistrationAnswers
```
 {
  "PartnerGUID": "93A6D55C-D4E7-49FC-8D68-671165ADE463",
  "MemberCode": "AUniquePartnerCode",
  "BirthDate": "6/21/1992",
  "PostalCode": "15235",
  "IsPIIDataRegulated": false,
  "RegistrationAnswers": [
        {
            "QuestionID": 1001001,
            "Answers": [
                {
                    "AnswerID": 2000223,
                    "AnswerValue": null
                }
            ]
        },
        {
            "QuestionID": 1001002,
            "Answers": [
                {
                    "AnswerID": 2000240,
                    "AnswerValue": null
                }
            ]
        },
        {
            "QuestionID": 1001007,
            "Answers": [
                {
                    "AnswerID": 2000246,
                    "AnswerValue": null
                }
            ]
        },
        {
            "QuestionID": 1012227,
            "Answers": [
                {
                    "AnswerID": 3055267,
                    "AnswerValue": null
                },
                {
                    "AnswerID": 3055271,
                    "AnswerValue": null
                }
            ]
        }
    ]
 }
```
