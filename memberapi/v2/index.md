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

