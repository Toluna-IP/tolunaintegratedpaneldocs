---
title: Get Recontact Members For Quota
has_children: false
parent: ES API
grand_parent: External Sample
nav_order: 3
---


## Get Recontact Members For Quota

content here 


##### GET RecontactMembersForQuota

For the requested Quota, returns a list of MemberCodes eligible for a recontact.

*Route(s)* 
```json
GET /ExternalSample/{panelGuid:GUID}/Recontact/{quotaID:int}/MemberCodes?maxResults={maxResults:int}&lastMemberCodeReceived={lastMemberCodeReceived:string}
```
*Header(s)*

```API_AUTH_KEY: A Partner-specific GUID prvoided by Toluna that must accompany every request```

*Parameters*

| Name | Type | Description |
| :--- | :-- | :--- |
| panelGUID | Guid | A Toluna-issued unique identifier for a Partner's culture-specific panel |
| quotaID | int | Tluna's unique identifier for a Quota |
| [OPTIONAL] The maximum number of MemberCodes that will be returned for the request. If not provided, defaults to a Toluna-configurable value (for, v0.1:10000) |
| lastMemberCodeReceived | string | [OPTIONAL] When dealing with batched results for a single Quota, supply this value to signal the last result received. The batch results will start with the MemberCode AFTER this value. Note that MemberCodes for recontact are ordered alphanumerically |

*Properties*

 - None
 
*Responses*

| Code | Etiology, actions |
| :--- | :--- |
| 200 | Request processed normally |
| 400 | Bad Request: see response for details |
| 500 | Internal Error. An exception occurred while processing this request. Toluna has likely captured details in its logs |
| 403 | Forbidden: invalid API_AUTH_KEY. See response for details |

*Sample Request*
```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
 {
  "MaxResults": 25,
  "HasAdditionalMembers": false,
  "MemberCodes": [
    "MemberCode1",
    "MemberCode2",
    "MemberCode3"
  ]
 }
```

*Response Properties*

| Name | Type | Description |
| :--- | :--- | :--- |
| MaxResults | int | The number of MemberCodes included in the response |
| HasAdditionalMembers | bool | When true, the Quota has more MemberCodes for recontact. Obtain them by repeating the request with the "lastMemberCodeReceived" parameter. |
| Member codes | ```list<string>``` | The MemberCodes Toluna would like to recontact for the Quota |

*Sample 400 Response*
```json
HTTP/1.1 400
Content-Type: application/json; charset=utf-8
 {
  "Result": "NO_QUOTA_ID",
  "ResultCode": 10
 }
```
