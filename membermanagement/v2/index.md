---
title: Dynamic (v2)
has_children: true
parent: Member Management
nav_order: 2
---


# V2 - Dynamic

Version 2 of the Member API is focused on speed, simplicity, improved support for demographic characteristics. It’s “closer to the metal” of the underlying Toluna Panel Management System and is optimized to remove internal dependencies. To the Partner, it’s faster and has more capability. It is independent of Static v1 and is managed separately. 

{: .label .label-red }
IMPORTANT

To access v2 of a route, supply the “Accept” header in your request as directed in the "Add Member," "Get Member," and "Update Member" pages. **This header is required for all Dynamic API Management routes.**

## Video Tutorial

<video class="video-fluid z-depth-1" loop controls muted style="width: 80%;">
  <source src="https://firebasestorage.googleapis.com/v0/b/toluna-ip.appspot.com/o/integration%2Fquick%2Fmember-mgt.mp4?alt=media&token=6b248496-fb79-4fd9-b989-1e31657d244c" type="video/mp4" />
</video>

## Question / AnswerIDs

Every Question has a static QuestionID, which maps to a series of possible static AnswerIDs. This information is clearly noted in the [Reference Data API](/mapping/referencedataapi/) each partner receives during the integration period. These are the most relevant Questions for IP:

| Question Name | QuestionID | Possible AnswerIDs |
| :-- | :--- | :--- |
| GenderID | 1001007 | See [Reference Data API](/mapping/referencedataapi/) |
| EducationID | 1001101 | See [Reference Data API](/mapping/referencedataapi/) |
| IncomeID | 1001107 | See [Reference Data API](/mapping/referencedataapi/) |
| EthnicityID | 1001012 | See [Reference Data API](/mapping/referencedataapi/) |
| WorkPositionID | 1005145 | See [Reference Data API](/mapping/referencedataapi/) |
| MaritalStatusID | 1001102 | See [Reference Data API](/mapping/referencedataapi/) |
| EmploymentStatusID | 1012395 | See [Reference Data API](/mapping/referencedataapi/) |
| RaceID | 1002790 | See [Reference Data API](/mapping/referencedataapi/) |

