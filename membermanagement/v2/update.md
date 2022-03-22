---
title: Update Member
has_children: false
parent: Dynamic (v2)
grand_parent: Member Management
nav_order: 3
---


# Member Update (PUT)
{: .no_toc}

Existing Members can be updated using HTTP PUT. “PartnerGUID” and “MemberCode” are required. Combine them with optional properties to update a Member according to your requirements.

 **This API will not support near-simultaneous calls. To avoid duplication errors, subsequent calls referencing the same MemberCode should be made no more frequently than once per 1000ms (1 sec)**

* TOC
{:toc}

---

## Request

### Route
```plaintext
PUT https://{IP_CORE_URL}/IntegratedPanelService/api/Respondent
```

### Request Parameters

 - None 

### Headers

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| ```Accept: application/json;version=2.0``` | ```string``` | Declaration of api version | Yes |


### Body Details

| Property | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| PartnerGUID | ```GUID``` | Unique Partner Code (Please request from Toluna if you don’t have one) | Yes |
| MemberCode | ```string``` | Unique Respondent Code from the Partner | Yes |
| IsActive | ```bool``` | Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool.| No |
| Email | ```string``` | Member email. NOTE: When Supplied, this must have a valid email format | No |
| BirthDate | ```string``` | MM/DD/YYYY format | No |
| PostalCode | ```string``` | Member postal code | No |
| IsTest | ```bool``` | Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used **ONLY** during testing | No |
| AnsweredQuestions | ```string``` | A collection of 0:M demographic Question and Answer ID pairs - **Currently available - will be marked as "obsolete" and deprecated in an year**  | No |
| RegistrationAnswers | ```string``` | Supports multi-select and open-ended answers. This will also maintain current single select responses| No |
| IsPIIDataRegulated | ```bool``` | Defaults FALSE. When TRUE, all personally identifiable information is removed | No |

### Examples

#### Deactivate Member
```plaintext
 {
  "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "MemberCode": "111",
  "IsActive": "false"
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

 #### Add RegistrationAnswers
 ```plaintext
 {
  "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "MemberCode": "111",
  "Email": "test@test.com",
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

 #### Add Open-Ended Answers beyond Postal code, Birthdate and Emai
 ```plaintext
 {
  "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "MemberCode": "111",
  "Email": "test@test.com",
   "RegistrationAnswers":
[
   {
      "QuestionID":1001032, 
      "Answers": [
          {"AnswerID":2224508, "AnswerValue" = "New York"} 
        ]
  }
]
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
 
#### Change Member EducationID
 ```plaintext
 {
  "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "MemberCode": "111",
  "AnsweredQuestions":
    [
     {"QuestionID":1001101,"AnswerID":2796531}
   ]
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

## Response

### Possible Codes

| Response Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, existing Member Paneling was updated without issue |
| 400 | Bad Request. Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 404 | Not Found. An attempt to update a Member that does not exist. Existence is determined by the combination of MemberCode and PartnerGUID |
| 500 | Internal Error. An exception occurred while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs |

### Body Details

> - No body will be included with a 201 response.
> - 400 and 409 responses will contain response bodies with additional details explaining the nature of the failure.


### Notes

> - Only updates existing members. To add a new Member, use the POST route noted [here](/membermanagement/v2 "v2 Post").
> - Optional Properties can be excluded from the request. "GenderID," "EducationID," "EthnicityID," "RaceID," and "SubProvinceID" can also take "0" to indicate "no value."
> - Invalid Property data typically returns a 400 response.
> - If RegistrationAnswers is supplied, AnswerQuestions will be ignored
> - **This API will not support near-simultaneous calls. To avoid duplication errors, subsequent calls referencing the same MemberCode should be made no more frequently than once per 1000ms (1 sec)**