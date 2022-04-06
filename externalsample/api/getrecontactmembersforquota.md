---
title: Get Recontact Members For Quota
has_children: false
parent: ES API
grand_parent: External Sample Offering
nav_order: 3
---


# Get Recontact Members For Quota
{: .no_toc }

For the requested Quota, returns a list of MemberCodes eligible for a recontact.

* TOC
{:toc}

---

## Request

### Route 
```plaintext
GET https://{IP_ES_URL}/IPExternalSamplingService/ExternalSample/{panelGuid}/Recontact/{quotaID}/MemberCodes?maxResults={maxResults}&lastMemberCodeReceived={lastMemberCodeReceived}
```

### Parameters

| Name | Type | Description | Required? |
| :--- | :-- | :--- | :---: |
| panelGUID | ```Guid``` | A Toluna-issued unique identifier for a Partner's culture-specific panel | Yes |
| quotaID | ```int``` | Tluna's unique identifier for a Quota | Yes |
| maxResult| ```int``` | The maximum number of MemberCodes that will be returned for the request. If not provided, defaults to a Toluna-configurable value (for, v0.1:10000) | No |
| lastMemberCodeReceived | ```string``` | When dealing with batched results for a single Quota, supply this value to signal the last result received. The batch results will start with the MemberCode AFTER this value. Note that MemberCodes for recontact are ordered alphanumerically | No |

### Header

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| API_AUTH_KEY | ```GUID``` | A Partner-specific GUID provided by Toluna | Yes|

### Body Details
 - None
 
### Example Request
```plaintext
GET https://{IP_ES_URL}/IPExternalSamplingService/ExternalSample/XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX/Recontact/12345/MemberCodes?maxResults=25&lastMemberCodeReceived=myLastResult
API_AUTH_KEY: XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX
```

---

## Responses

### Possible Responses

| Code | Etiology, actions |
| :--- | :--- |
| 200 | Request processed normally |
| 400 | Bad Request: see response for details |
| 500 | Internal Error. An exception occurred while processing this request. Toluna has likely captured details in its logs |
| 403 | Forbidden: invalid API_AUTH_KEY. See response for details |


### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| MaxResults | ```int``` | The number of MemberCodes included in the response |
| HasAdditionalMembers | ```bool``` | When true, the Quota has more MemberCodes for recontact. Obtain them by repeating the request with the "lastMemberCodeReceived" parameter. |
| Member codes | ```list<string>``` | The MemberCodes Toluna would like to recontact for the Quota |


### Examples

#### 200 Response
```plaintext
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
 "MaxResults": 25,
 "HasAdditionalMembers": false,
 "MemberCodes": [
 "memberCode1",
 "memberCode2",
 "memberCode3"
 ]
}
```

### Sample 400 Response
```plaintext
HTTP/1.1 400
Content-Type: application/json; charset=utf-8
 {
  "Result": "NO_QUOTA_ID",
  "ResultCode": 10
 }
```

#### 400 Response
```plaintext
HTTP/1.1 400
Content-Type: application/json; charset=utf-8

{
 "Result": "NO_QUOTA_ID",
 "ResultCode": 10
}
```