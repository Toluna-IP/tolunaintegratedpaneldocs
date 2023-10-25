---
title: Common Attributes
has_children: false
parent: Member Management
nav_order: 3
---

# Common Attributes

The following are common attributes that are applicable in all cultures. These attributes are also available via the [Reference Data API](/mapping/referencedataapi/)'s "Questions and Answers" and "Question Data" routes.

## Gender

### QuestionID: 1001007

### Answers

| AnswerID | Translation |
| :--- | :--- |
| 2000246 | Female |
| 2000247 | Male |


## Age 

> Note: this question does not appear in the [Reference Data API](/mapping/referencedataapi/) for any culture.
> This answer may also show up as "AnswerValues" in the [GetQuotas Response](/externalsample/api/getquotas.html) as an age range (e.g. "18-100"). Partners should ensure their system can accommodate either syntax.

### QuestionID: 1001538

| AnswerID | Translation |
| :--- | :--- |
| 2006351 | 13-17 |
| 2006352 | 18-24 |
| 2006353 | 25-29 |
| 2006354 | 30-34 |
| 2006355 | 35-39 |
| 2006356 | 40-44 |
| 2006357 | 45-49 |
| 2006358 | 50-54 |
| 2006359 | 55-59 |
| 2006360 | 60-64 |
| 2006361 | 65 and older |

### Minimum Age Requirements

Members under a certain age may not be registered with Toluna. Attempting to register a member below the minimum age will generate an error and the member will not be created. This age differs between countries. A list of age requires can be found by clicking the following:

<a href="https://docs.integratedpanel.toluna.com/resources/resources\IP min allowed age - Aug 2023.xlsx" target="_blank" class="btn">Click Here to Access Excel File with Minimum Ages</a>