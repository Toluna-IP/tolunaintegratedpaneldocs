---
title: Questions and Answers
has_children: false
nav_order: 2
parent: Reference Data API
grand_parent: Mapping

---

# Questions and Answers
{: .no_toc }

Returns a list of all platform questions and their details. Due to the large inventory of questions, Toluna recommends that this tool be used periodically and with a maximum of 5 cultures per call. This will ensure the response is delivered in a timely and easily-absorbable manner.

* TOC
{:toc}

---

## Request

### Route
```
POST {IP_REF_DATA_URL}/IPExternalSamplingService/ReferenceData/QuestionsAndAnswersData 
```

### Parameters

 - None

### Header

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| PARTNER_AUTH_KEY | ```string``` | Authorization of Reference Data access | Yes |

### Body Details

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| CultureIDs | ```array<int>``` | Culture identifiers for requested cultures. Limit 5 cultures per request. For a list of available cultures, click [here](/mapping/referencedataapi/cultures.html) | Yes |
| CategoryIDs | ```array<int>``` | Category identifiers that limit the response to questions and answers tied to the specific Category | No |
| LastUpdateDate | ```dateTime``` | Format YYYY-MM-DDTHH:MM:SS. Any questions and answers modified after the date given will be included in the results. If omitted, all questions and answers will be given regardles of modificaiton date | No |
| IncludeComputed | ```bool``` | Default false. When true, questions with answer type "Computed" will be included in results. Set to "false" to exclude these questions | No |
| IncludeRoutables | ```bool``` | Default false. When true, routable questions (IsRoutable=true) will be included in the results. Set to false to exclude these questions | No |
| IncludeDemographics | ```bool``` | Defaults false. When true, questions regarding member Demographics (i.e. Ethnicity) are included. Set to false to exclude these questions | No |


### Example Request
```
 {
    "CultureIDs": [{{qAndaCultures}}],                        
    "CategoryIDs": [],
    "LastUpdateDate": "2000-11-10T13:59:47.0969632+02:00",
    "IncludeComputed" : "true",
    "IncludeRoutables": "true",
    "IncludeDemographics": "true"
}
```

---

## Response

### Possible Codes

| Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 403 | Forbidden. Invalid PARTNER_AUTH_KEY |
| 500 | Internal Error. An exception occurrec while processing the request. Contact Toluna for resolution. Toluna will likely have the details caputred in its logs |

### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| IsRoutable | ```bool``` | Declares whether a question is routable or not |
| InternalName | ```string``` | Toluna's name for a question used only internally |
| TranslatedQuestion | ```list<object>``` | Shows details for the specific question |
| ChildQuestions | ```list<object>``` | Shows details for any Childquestions associated with a TranslatedQuestion. Child questions are only associated with Questions that have the answer type "Container" |
| TranslatedAnswers | ```list<object>``` | List of question answers and their properties |


#### TranslatedQuestion Objects

| Name | Type | Description | 
| :--- | :--- | :--- |
| QuestionID | ```int``` | Toluna's unique identifier for a question |
| CultureID | ```int``` | Toluna's unique identifier for a culture |
| DisplayNameTranslation | ```string``` | Toluna's name for a question shown to the Repondent |

#### ChildQuestions Objects

| Name | Type | Description | 
| :--- | :--- | :--- |
| QuestionID | ```int``` | Toluna's unique identifier for a question |
| CultureID | ```int``` | Toluna's unique identifier for a culture |
| DisplayNameTranslation | ```string``` | Toluna's name for a question shown to the Repondent |


#### TranslatedAnswers Objects

| Name | Type | Description |
| :--- | :--- | :--- |
| AnswerID | ```int``` | Toluna's unique identifier for an answer |
| Translation | ```string``` | Answer text as shown to the Respondent |
| AnswerInternalName | Answer text used internally |
| AnswerType | ```string``` | Defines how the answer is derived. Possible responses are SingleSelect, ComputedType, MultiSelect, OpenEnded, Container |
| AnswerValidationRegularExpression | ```string``` | Declares regular expression for open-ended questions. If the question is not open-ended, response will be 'null' |

### Example Response
```plaintext
[
...
  {
    "IsRoutable": true,
    "InternalName": "routable question lee",
    "TranslatedQuestion": {
      "QuestionID": 20002866,
      "CultureID": 1,
      "DisplayNameTranslation": "routable question lee",
      "HelpTextTranslation": "",
      "SamplingSequenceNumber": null
    },
    "ChildQuestions": null,
    "TranslatedAnswers": [
      {
        "AnswerID": 50006863,
        "Translation": "routable question lee1",
        "AnswerInternalName": "routable question lee1"
      },
      {
        "AnswerID": 50006864,
        "Translation": "routable question lee2",
        "AnswerInternalName": "routable question lee2"
      }
    ],
    "AnswerType": "SingleSelect",
    "AnswerValidationRegularExpression": null
  },
...
]
```