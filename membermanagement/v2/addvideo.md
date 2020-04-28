---
title: Add Member
has_children: false
parent: Dynamic (v2)
grand_parent: Member Management
nav_exclude: true
search_exclude: true
---


# Adding a Member (POST)
{: .no_toc}

A partner can add new members to the Toluna IP Database using an HTTP POST. This must be done by the partner before requesting or receiving survey opportunity links.

This request is almost an exact parallel to that in the Static Member Management section, with a few key differences. The most important being the Header, shown below.

* TOC
{:toc}

---

## Request


<video class="video-fluid z-depth-1" loop controls muted style="max-width: 800px;">
  <source src="https://firebasestorage.googleapis.com/v0/b/toluna-ip.appspot.com/o/integration%2Fquick%2Fmember-mgt.mp4?alt=media&token=6b248496-fb79-4fd9-b989-1e31657d244c" type="video/mp4" />
</video>

### Route
```plaintext
POST http://{IP_CORE_URL}/IntegratedPanelService/api/Respondent
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
| IsPIIDataRegulated | ```bool``` | Defaults FALSE. When TRUE, all personally identifiable information is removed | No |
| AnsweredQuestions | ```string``` | A collection of 0:M demographic Question and Answer ID pairs, | No |

### Example

```plaintext
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

| Property | Description |
| :--- | :--- |
| PartnerGUID | Unique Parnter Code (Please request from Toluna if you don't have one) |
| MemberCode | Unique Respondent Code from the Partner |
| IsActive | Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool |
| Email | Member email. NOTE: when supplied, this must have a valid email format |
| BirthDate | MM/DD/YYYY format |
| PostalCode | Member postal code |
| IsTest | Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used **ONLY** during testing |
| IsPIIDataRegulated | Defaults FALSE. When TRUE, all personally identifiable information is removed |
| AnsweredQuestions | A collection of 0:M demographic Question and Answer ID pairs, |


### Notes

> - Only new Members can be added. To update, use the PUT route noted below
> - Invalid Property data typically returns a 400 response that contains explanation for the rejection

