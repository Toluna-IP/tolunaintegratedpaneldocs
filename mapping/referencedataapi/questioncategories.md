---
title: Question Categories
has_children: false
nav_order: 6
parent: Reference Data API
grand_parent: Mapping

---

# Question Categories
{: .no_toc }

Returns a list of all question category names and IDs.

* TOC
{:toc}

---

## Request

### Route
```
GET {IP_REF_DATA_URL}/IPUtilityService/ReferenceData/QuestionCategories 
```

### Parameters

 - None

### Header

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| PARTNER_AUTH_KEY | ```string``` | Authorization of Reference Data access | Yes |

### Body Details

 - None

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
| Name | ```string``` | Toluna's unique name for a question |
| Description | ```string``` | Clarifying description of question |
| CategoryID | ```int``` | Toluna's identifier for the category the question is associated with |