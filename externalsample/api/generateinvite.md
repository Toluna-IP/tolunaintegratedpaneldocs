---
title: Generate Invite
has_children: false
parent: ES API
grand_parent: External Sample Offering
nav_order: 2
---


# Generate Invite
{: .no_toc }

* TOC
{:toc}

---

## Introduction

Once a Member has been matched to a Toluna Quota, this reoute can be used to generate an invitation.

---

## Request

### Route

```GET http:///{IP_ES_URL}/ExternalSample/{PanelGuid:GUID}/{MemberCode:string}/Invite/{QuotaID:int}```


### Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| PanelGUID | ```Guid``` | A Toluna-issued unique identifier for a Partner's culture-specific panel | Yes |
| MemberCode | ```string``` | Partner's unique identifier for the Member as define when registered with Toluna. The PanelGUID+MemberCode is always unique within the Toluna system | Yes |
| QuotaID | ```int``` | Toluna's unqiue identifier for a Quota | Yes |

### Header(s) 

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| API_AUTH_KEY | ```GUID``` | A Partner-specific GUID provided by Toluna | Yes |


### Body Details

 - None

### Example Request
```json
GET http://{IP_ES_URL}/ExternalSample/XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX/MyMemberCode/Invite/12345
API_AUTH_KEY: XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX
cache-control: no-cache
```

---

## Responses
 
### Possible Codes

| Code | Etiology, actions |
| :--- | :--- |
| 200 | Request processed normally |
| 400 | Bad Request: see response for details |
| 500 | Internal Error: An exception occured while processing the request. Toluna likely has captured details in its logs |
| 403 | Forbidden: Invalid API_AUTH_KEY. See response for details |



### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| SurveyID | int | Toluna's internal unique identifier for a Survey |
| WaveID | int | Toluna's internal unique indentifier for a single iteration of a Survey. The SurveyID+WaveID is always unique |
| QuotaID | int | Toluna's unqiue identifier for a Quota |
| Member Amount | double | Amount Partner has agreed to pay it’s Member for a complete. This is rarely used and Toluna prefers to avoid direct engagement with the Partner-Member relationship |
| Partner Amount | double | Amount Toluna has agreed to pay Partner for a complete |
| URL | string | Link to Invite Member to Quota |
| LOI | int | Length of Interview at the time fo invite generation |
| IR | int | Incidence Rate at the time fo invite generation |

### Examples

#### 200 Response
```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
 "SurveyId": 2349720,
 "WaveID": 34839308,
 "QuotaID": 3445365,
 "MemberAmount": 0.5,
 "PartnerAmount": 1,
 "URL": "http://[ROOT]/TrafficUI/MSCUI/Page.aspx?pgtid=20&od=kqe0mda072UagaQSVQIlgUX1QE4E41107",
 "LOI": 5,
 "IR": 40
}
```

#### 400 Response
```json
HTTP/1.1 400
Content-Type: application/json; charset=utf-8
 {
  "Result": "NO_QUOTA_ID",
  "ResultCode": 10
 }
```
