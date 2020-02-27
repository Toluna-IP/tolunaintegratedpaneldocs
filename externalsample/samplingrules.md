---
title: Sampling Rules
has_children: false
nav_order: 4
parent: External Sample Offering
---

## Sampling Rules


Quotas are borken down into the following components: Surveys, [Waves](/general/common.html#tracking-surveys-and-the-waveid-property), Quotas, Layers, and Subquotas. External Sample Partners must comply with Toluna's sampling rules. To be qualified for a Survey and sampled for a Quota, a member must be an exact match to the desired Survey based on the parameters listed below.

To be sampled for a Quota, a member must:

 - Be targted for only 1 Quota per Survey
 - Match ALL Layers in the Quota
 - Match ONE of the SubQuotas
 - Match at least one "AnswerID" (SubQuotaAttribute) per SubQuota with the single QuestionID
 - Match at least one "AnswerID" (SubQuotaAttribute) per QuestionID in the SubQuota with multiple QuestionIDs
 
These rules can be consolidated into simple boolean conditions:

 - Quotas are "OR" conditions
 - Layers are "AND" conditions
 - SubQuotas are "OR" conditions
 - AnswerIDs are "OR" conditions
 - Within a SubQuota
   - "OR" for the same QuestionID
   - "AND" for multiple QuestionIDs
   
### Sampling Examples

Click each button to open a new page with the JSON file for the specific example.

<a href="http://docs.integratedpanel.toluna.com/externalsample/api/responses/quotamultiplelayer.json" target="_blank" class="btn">Quota with Multiple Layers</a>

<a href="http://docs.integratedpanel.toluna.com/externalsample/api/responses/singlelayermultipleqid.json" target="_blank" class="btn">Quota with Single Layer, Multiple QuestionIDs</a>

<a href="http://docs.integratedpanel.toluna.com/externalsample/api/responses/singlelayersingleqid.json" target="_blank" class="btn">Quota with Single Layer, Single QuestionID</a>
