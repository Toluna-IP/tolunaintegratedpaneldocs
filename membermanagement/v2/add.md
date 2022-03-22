---
title: Add Member
has_children: false
parent: Dynamic (v2)
grand_parent: Member Management
nav_order: 1
---


# Adding a Member (POST)
{: .no_toc}

A partner can add new members to the Toluna IP Database using an HTTP POST. This must be done by the partner before requesting or receiving survey opportunity links.

This request is almost an exact parallel to that in the Static Member Management section, with a few key differences. The most important being the Header, shown below.

**IMPORTANT NOTE: This API will not support near-simultaneous calls. To avoid duplication errors, subsequent calls referencing the same MemberCode should be made no more frequently than once per 1000ms (1 sec)**

**In order to place a Member into a Survey, Toluna must know - at a minimum - the panelist Date of Birth and Gender.** 

* TOC
{:toc}

---

## Request

### Route
```plaintext
POST https://{IP_CORE_URL}/IntegratedPanelService/api/Respondent
```

### Request Parameters
 - None

### Headers

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| ```Accept: application/json;version=2.0``` | ```string``` | Declaration of api version | Yes |


### Body Details

| Property | Description | Type | Required? |
| :--- | :--- | :--- | :---: |
| PartnerGUID | ```GUID``` | Unique Partner Code (Please request from Toluna if you don’t have one) | Yes |
| MemberCode | ```string``` | Unique Respondent Code from the Partner | Yes |
| IsActive | ```bool``` | Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool.| No |
| Email | ```string``` | Member email. NOTE: When Supplied, this must have a valid email format | No |
| BirthDate | ```string``` | MM/DD/YYYY format | No |
| PostalCode | ```string``` | Member postal code | No |
| IsTest | ```bool``` | Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used **ONLY** during testing | No |
| AnsweredQuestions | ```string``` | A collection of 0:M demographic Question and Answer ID pairs - **Currently available - will be marked as "obsolete" and deprecated in an year**  | No |
| RegistrationAnswers | ```string``` | Supports multi-select and open-ended answers. This will also maintain current single select responses | No |

### Example - AnsweredQuestions

```plaintext
{
 "PartnerGUID": "93A6D55C-D4E7-49FC-8D68-671165ADE463",
 "MemberCode": "AUniquePartnerCode",
 "Email": "member@yopmail.com",
 "BirthDate": "6/21/1992",
 "PostalCode": "15235",
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

---


### Example - RegistrationAnswers

```plaintext
{
 "PartnerGUID": "93A6D55C-D4E7-49FC-8D68-671165ADE463",
 "MemberCode": "AUniquePartnerCode",
 "Email": "member@yopmail.com",
 "BirthDate": "6/21/1992",
 "PostalCode": "15235",
 "RegistrationAnswers":
  [
   {
      "QuestionID":1012227, 
      "Answers":
         [
           {"AnswerID":3055267}, 
           {"AnswerID":3055271}
          ]
  }
]
}
```

---

Open-Ended Answers beyond Postal code, Birthdate, and Email can be supplied as below:

```plaintext
[
   {
      "QuestionID":1001032, 
      "Answers": [
                {"AnswerID":2224508, "AnswerValue" = "New York"} ]
  }
]

```

---


## Response


### Possible Codes

| Response Code | Etiology, actions |
| :--- | :--- |
| 201 | Created. Request processed normally, resulting in a new Member |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 409 | Conflict. An attempt to add a Member that already exists. Duplication is determined by the combination of MemberCode and PartnerGUID |
| 500 | Internal Error. An exception occurred while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs |

### Body Details

> - No body will be included with a 201 response.
> - 400 and 409 responses will contain response bodies with additional details explaining the nature of the failure.


### Notes

> - Only new Members can be added. To update, use the PUT route noted below
> - Invalid Property data typically returns a 400 response that contains explanation for the rejection
> - If RegistrationAnswers is supplied, AnswerQuestions will be ignored
> - **This API will not support near-simultaneous calls. To avoid duplication errors, subsequent calls referencing the same MemberCode should be made no more frequently than once per 1000ms (1 sec)**

