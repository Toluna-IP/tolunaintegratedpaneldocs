---
title: Get Quotas
has_children: false
parent: ES API
grand_parent: External Sample Offering
nav_order: 1
---


## Get Quotas

content here 


| Name | GetQuotas |
| :--- | :--- |
|Description | For a Toluna-issued "PanelGUID," returns a list of Surveys and their associated Quotas in need of supply. |
| Route(s) | ``` GET /ExternalSample/{PanelGUID:GUID}/Quotas?includeRoutables:bool``` |
| Header(s) | ``` API_AUTH_KEY ``` A partner-specific GUID provided by Toluna that must accompany every request |
| Parameters | <div class="table-wrapper"><table> <thead> <tr> <th style="text-align: left">Name</th> <th style="text-align: left">Type</th> <th style="text-align: left">Description</th> </tr> </thead> <tbody> <tr> <td style="text-align: left">PanelGUID</td> <td style="text-align: left">Guid</td> <td style="text-align: left">A Toluna-issue unique identifier for a Partner’s culture-specific panel.</td> </tr> <tr> <td style="text-align: left">includeRoutables</td> <td style="text-align: left">bool</td> <td style="text-align: left">(Optional) Indicates whether to include Routable questions in the result or not. This will take precedence over the panel-level setting which is OFF by default. Opt in to set Panel-level setting to be ON.</td> </tr> </tbody> </table></div> |
| Properties | N/A |
| Sample Request | ``` GET http://{ES-Root-URL}/ExternalSample/96B52BEE-32FE-4A23-8FEE-821F6AAA5CA5/Quotas API_AUTH_KEY: 10B1BF48-F141-41CD-850F-4DE5A8BA44EB``` |
| Sample 200 Response | Full request can be seen [here](https://josh-toluna.github.io/tolunaintegratedpaneldocs/externalsample/getquotasresponse.json "Sample 200 Response") |
| Possible Request Response Codes | <table> <thead> <tr> <th style="text-align: left">Code</th> <th style="text-align: left">Etiology, actions</th> </tr> </thead> <tbody> <tr> <td style="text-align: left">200</td> <td style="text-align: left">Request processed normally</td> </tr> <tr> <td style="text-align: left">400</td> <td style="text-align: left">Bad Request. See response for details</td> </tr> <tr> <td style="text-align: left">500</td> <td style="text-align: left">Internal Error. An exception occurred while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs</td> </tr> <tr> <td style="text-align: left">403</td> <td style="text-align: left">Forbidden: Invalid <code class="language-plaintext highlighter-rouge">API_AUTH_KEY</code> See response for details</td> </tr> </tbody> </table> |

### Sample 400 Response
```json
HTTP/1.1 400
Content-Type: application/json; charset=utf-8

 {
   "Result": "PANEL_DOES_NOT_EXIST",
   "ResultCode": 3
 }
```

### Response Properties

| Name | Type | Description |
| :--- | :--- | :--- |
| CountryID |	```int``` |	Toluna’s unique identifier for the country in which the available Quotas are located. |
| CacheExpires |	```dateTime``` |	Date at which Toluna’s internal cache of this Quota data expired. Repreating API calls after this time guarentees an updated result set |
| Surveys |	```list<object>``` |	A JSON object containing 1:M Surveys for which Toluna has open Quotas |
| Survey.SurveyID |	```int``` |	Toluna’s internal unique identifies for a Survey |
| Survey.SurveyName |	```string``` |	Toluna’s internal name for a Survey |
| Survey.SurveyTopic |	```string``` |	Study type of a Survey |
| Survey.WaveID |	```int``` |	Toluna’s internal unique identifier for a single iteration of a Survey. The SurveyID+WaveID is always unique |
| Survey.LOI |	```int``` |	Length of interview |
| Survey.IR |	```int``` |	Incidence Rate |
| Survey.StudyTypeID |	```int``` |	The Survey’s “category.” See mapping document for values |
| Survey.ScheduledCompletionDate |	```dateTime``` |	Date at which Survey is set to close |
| Survey.DeviceTypeIDs |	```list<int>``` |	Devices upon which the Survey can be used. See mapping document for details |
| Survey.IsSurveyRecontact |	```boolean``` |	When TRUE, the Survey is looking to engage specific Members for a follow-up study. Please see the “Recontact” section for mor einformation regarding its use |
| Survey.CompletesRequired |	```int``` |	The total number of completes required across all Quotas until the ScheduleCompletionDate. This should be considered the limit of completes available. At times, this may be less than the sum of all Quotas |
| Survey.EstimatedCopletesRemaining |	```int``` |	The estimated number of completes remaining until the ScheduleCompletionDate, across all Quotas, until the Survey is full. At times, this may be less than the sum of all Quotas |
| Survey.Price |	```<object>``` |	A JSON object containing details about price Toluna will pay per complete |
| Price.Amount |	```double``` |	The monetary amount of the payment per complete |
| Price.CurrencyID |	```int``` |	Currency in which the payment per complete is denoted. See mapping document for details |
| Survey.Quotas |	```list<object>``` |	A JSON object containing 1:M Quotas for the Survey. Members can be targeted only to one quota within the Survey |
| Quota.QuotaID |	```int``` |	Toluna’s unique identifier for a Quota |
| Quota.CompletesRequired |	```int``` |	The total number of completes required to fill the Quota |
| Quota.EstimatedCompletesRemaining |	```int``` |	The estimated number of completes remaining until the Quota is filled |
| Quota.Layers |	```list<object>``` |	A JSON object containing groups of Quotas. When sampling, all Layers must be matched |
| Layer.LayerID |	```int``` |	Toluna’s unique identifier for a Layer |
| Layer.SubQuotas |	```list<object>``` |	A JSON object contains 1:M SubQuotas. When sampling, one SubQuota must be matched |
| SubQuota.SubQuotaID |	```int``` |	Toluna’s unique identifier for a SubQuota |
| SubQuota.CurrentCompletes |	```int``` |	Current complete received for a SubQuota |
| SubQuota.MaxTargetCompletes |	```int``` |	Maximum target completes required for a SubQuota |
| SubQuota.QuestionsAndAnswers |	```list<object>``` |	A JSON object contains collection of Question and Answers per SubQuota |
| QuestionAnswers.QuestionID |	```int``` |	Toluna internal profile attribute identifier |
| QuesitonAndAnswers.AnswerIDs |	```list<int>``` |	List of Toluna internal profile attribute identifiers. When sampling, at least one AnswerID must match. See mapping document for details |
| QuestionAndAnswers.AnswerValues |	```string<int>``` |	List of Answer values of an open ended answers.Example: Custom Age values “18-100”, Postal codes, DMA and MSA. Note: “Age” will be range based. “DMA and MSA” will be comma separated Answer IDs. “Postal codes” will be comma separated postal code values. It can contain partial values. ‘Starts with’ must be applied to match it. API is limited to expose only first 1000 postal codes. |
| QuestionAndAnswers.IsRoutable |	```boolean``` |	Indicates whether the question is Routable or not |




**Example Quotas**

[Example Quota with Multiple Layers](){: .btn }

[Example Quota with Single Layer, SubQuota with Multple QuestionIDs](){: .btn }

[Example Quota with Single lyaer, SubQuota with Single QuestionIDs](){: .btn}