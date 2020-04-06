---
title: Question Data
has_children: false
nav_order: 8
parent: Reference Data API
grand_parent: Mapping
---

# Question Data
{: .no_toc }

Returns detailed information on a specified question in a specified culture.

* TOC
{:toc}

---

## Request

### Route
```plaintext
GET {IP_REF_DATA_URL}/IPUtilityService/ReferenceData/QuestionAndAnswersData/{questionID}/{cultureID}
```

### Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| questionID | ```int``` | Identifier for the desired question | Yes |
| cultureID | ```int``` | Identifier for the culture to which the question belongs. To find a cultureID, use the route detailed [here](/mapping/referencedataapi/cultures.html) | Yes |

### Header

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| PARTER_AUTH_KEY | ```string``` | Authorization of Reference Data Access | Yes |

### Body Details

 - None

### Example Request
```plaintext
GET {IP_REF_DATA_URL}/IPUtilityService/ReferenceData/QuestionAndAnswersData/1010876/1 HTTP/1.1
Content-Type: application/json
PARTNER_AUTH_KEY: XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
```

---

## Response

### Possible Codes

| Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 403 | Forbiddent. Invalid PARTER_AUTH_KEY |
| 500 | Internal Error. An exception occurred while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs |

### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| IsRoutable | ```bool``` | Defines whether or not a member can be routed to this question before proceeding to an invited survey. For more information, click [here])(/faq/externalsample/quotas.html#can-i-send-usersmemberspanelists-to-quotas-with-unansweredunknown-subquotas) |
| InternalName | ```string``` | Toluna's name for a question used only internally |
| TranslatedQuestion | ```list<object>``` | Shows the details for the specified question |
| ChildQuestions | ```list<object>``` | Shows details for any Childquestions associated with a TranslatedQuestion. Child questions are only associated with Questions that have the answer type “Container” |
| TranslatedAnswers | ```list<object>``` | List of question answers and their properties |
| AnswerType | ```string``` | Defines how the answer is derived. Possible responses are SingleSelect, ComputedType, MultiSelect, OpenEnded, Container |
| AnswerValidationRegularExpression | ```string``` | Declares regular expression for open-ended questions. If the question is not open-ended, response will be ‘null’ |

#### TranslatedQuestion Objects

| Name | Type | Description |
| :--- | :--- | :--- |
| QuestionID | ```int``` | Toluna's unique identifier for a question |
| CultureID | ```int``` | Toluna's unique identifier for the culture to which the quesiton belongs |
| DisplayNameTranslation | ```string``` | Toluna's name for a question shown to the Respondent |
| HelpTextTranslation | ```string``` | Additional information shown to the Respondent to help them better answer the question |

#### TranslatedAnswers Objects

| Name | Type | Description |
| :--- | :--- | :--- |
| AnswerID | ```int``` | Toluna's unique identifier for an answer |
| Translation | ```string``` | Answer text as show to the Respondent |
| AnswerInteralName | ```string``` | Answer texted used internally |

### Example Response
```plaintext
[
  {
    "IsRoutable": true,
    "InternalName": "Online Games Console and Frequency - Xbox 360",
    "TranslatedQuestion": {
      "QuestionID": 1010876,
      "CultureID": 1,
      "DisplayNameTranslation": "Xbox 360",
      "HelpTextTranslation": "",
      "SamplingSequenceNumber": null
    },
    "ChildQuestions": null,
    "TranslatedAnswers": [
      {
        "AnswerID": 3015474,
        "Translation": "Mainly play online games",
        "AnswerInternalName": "Mainly play online games"
      },
      {
        "AnswerID": 3014489,
        "Translation": "Mainly play off-line games",
        "AnswerInternalName": "Mainly play off-line games"
      },
      {
        "AnswerID": 3015475,
        "Translation": "Play online games only",
        "AnswerInternalName": "Play online games only"
      },
      {
        "AnswerID": 3015473,
        "Translation": "Play off-line games and online games about the same amount",
        "AnswerInternalName": "Play off-line games and online games about the same amount"
      },
      {
        "AnswerID": 3500202,
        "Translation": "Do not play",
        "AnswerInternalName": "Do not play"
      },
      {
        "AnswerID": 3014488,
        "Translation": "Play off-line games only",
        "AnswerInternalName": "Play off-line games only"
      }
    ],
    "AnswerType": "SingleSelect",
    "AnswerValidationRegularExpression": null
  }
]
```