---
title: Get Quotas
has_children: false
parent: ES API
grand_parent: External Sample Offering
nav_order: 1
---


# Get Quotas
{: .no_toc }

For a Toluna-issued "PanelGUID," returns a list of Surveys and their associated Quotas in need of supply.

* TEST
{:toc}


---

## Request


### Route
```plaintext
GET http://{IP_ES_URL}/ExternalSample/{PanelGUID:GUID}/Quotas?includeRoutables:{bool}
```

### Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| PanelGUID | ```Guid``` | A Toluna-issued unique identifier for a Partner’s culture-specific panel. | Yes |
| IncludeRoutables | ```bool``` | Indicates whether to include Routable questions in the result or not. This will take precedence over the panel-level setting which is OFF by default. Opt in to set Panel-level setting to be ON | No |


### Header

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| API_AUTH_KEY | ```GUID``` | A Partner-specific GUID provided by Toluna | Yes |


### Body Details

 - None

### Example Request

```
GET http://{IP_ES_URL}/ExternalSample/XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX/Quotas
API_AUTH_KEY: XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX
```
---

## Response

### Possible Codes

| Code | Etiology, action |
| :--- | :--- |
| 200 | Request processed normally |
| 400 | Bad Request: See response for details |
| 500 | Internal Error. An exception has occured while processing the request. Toluna likely has captured the details in its logs |
| 403 | Forbidden: invalid API_AUTH_KEY. See response for details |


### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| CountryID |	```int``` |	Toluna’s unique identifier for the country in which the available Quotas are located. |
| CacheExpires |	```dateTime``` |	Date at which Toluna’s cache of this Quota data expired. Repreating API calls after this time guarentees an updated result set |
| Surveys |	```list<object>``` |	A JSON object containing 1:M Surveys for which Toluna has open Quotas |

#### Survey Object

| Name | Type | Description |
| :--- | :--- | :--- |
| SurveyID |	```int``` |	Toluna’s unique identifies for a Survey |
| SurveyName |	```string``` |	Toluna’s name for a Survey |
| SurveyTopic |	```string``` |	Study type of a Survey |
| WaveID |	```int``` |	Toluna’s unique identifier for a single iteration of a Survey. The SurveyID+WaveID is always unique |
| LOI |	```int``` |	Length of interview in minutes |
| IR |	```int``` |	Incidence Rate |
| StudyTypeID |	```int``` |	The Survey’s “category.” See mapping document for values |
| ScheduledCompletionDate |	```dateTime``` |	Date at which Survey is set to close |
| DeviceTypeIDs |	```list<int>``` |	Devices upon which the Survey can be used. See mapping document for details |
| IsSurveyRecontact |	```boolean``` |	When TRUE, the Survey is looking to engage specific Members for a follow-up study. Please see the “Recontact” section for mor einformation regarding its use |
| CompletesRequired |	```int``` |	The total number of completes required across all Quotas until the ScheduleCompletionDate. This should be considered the limit of completes available. At times, this may be less than the sum of all Quotas |
| EstimatedCopletesRemaining |	```int``` |	The estimated number of completes remaining until the ScheduleCompletionDate, across all Quotas, until the Survey is full. At times, this may be less than the sum of all Quotas |
| Price |	```<object>``` |	A JSON object containing details about price Toluna will pay per complete |
| Quotas |	```list<object>``` |	A JSON object containing 1:M Quotas for the Survey. Members can be targeted only to one quota within the Survey |

#### Price Object

| Name | Type | Description |
| :--- | :--- | :--- |
| Amount |	```double``` |	The monetary amount of the payment per complete |
| CurrencyID |	```int``` |	Currency in which the payment per complete is denoted. See mapping document for details |

#### Quota Object

| Name | Type | Description |
| :--- | :--- | :--- |
| QuotaID |	```int``` |	Toluna’s unique identifier for a Quota |
| CompletesRequired |	```int``` |	The total number of completes required to fill the Quota |
| EstimatedCompletesRemaining |	```int``` |	The estimated number of completes remaining until the Quota is filled |
| Layers |	```list<object>``` |	A JSON object containing groups of Quotas. When sampling, all Layers must be matched |

#### Layer Object

| Name | Type | Description |
| :--- | :--- | :--- |
| LayerID |	```int``` |	Toluna’s unique identifier for a Layer |
| SubQuotas |	```list<object>``` |	A JSON object contains 1:M SubQuotas. When sampling, one SubQuota must be matched |

#### SubQuota

| Name | Type | Description |
| :--- | :--- | :--- |
| SubQuotaID |	```int``` |	Toluna’s unique identifier for a SubQuota |
| CurrentCompletes |	```int``` |	Current complete received for a SubQuota |
| MaxTargetCompletes |	```int``` |	Maximum target completes required for a SubQuota |
| QuestionsAndAnswers |	```list<object>``` |	A JSON object contains collection of Question and Answers per SubQuota |

#### QuestionAndAnswers Object

| Name | Type | Description |
| :--- | :--- | :--- |
| QuestionID |	```int``` |	Toluna's profile attribute identifier |
| AnswerIDs |	```list<int>``` |	List of Toluna's profile attribute identifiers. When sampling, at least one AnswerID must match. See mapping document for details |
| AnswerValues |	```string<int>``` |	List of Answer values of an open ended answers.Example: Custom Age values “18-100”, Postal codes, DMA and MSA. Note: “Age” will be range based. “DMA and MSA” will be comma separated Answer IDs. “Postal codes” will be comma separated postal code values. It can contain partial values. ‘Starts with’ must be applied to match it. API is limited to expose only first 1000 postal codes. |
| IsRoutable |	```boolean``` |	Indicates whether the question is Routable or not |


### Examples

#### 200 Response

[Click Here to Access JSON File](http://docs.integratedpanel.toluna.com/resources/getquotas.json){: .btn }

<a href="http://docs.integratedpanel.toluna.com/resources/getquotas.json" target="_blank" class="btn">Click Here to Access JSON File</a>


#### 400 Response
```plaintext
HTTP/1.1 400
Content-Type: application/json; charset=utf-8

 {
   "Result": "PANEL_DOES_NOT_EXIST",
   "ResultCode": 3
 }
```
