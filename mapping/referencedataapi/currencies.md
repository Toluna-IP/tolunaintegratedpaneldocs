---
title: Currencies
has_children: false
nav_order: 4
parent: Reference Data API
grand_parent: Mapping

---

# Currencies
{: .no_toc }

Returns a list of all study types and their details.

* TOC
{:toc}

---

## Request

### Route
```
GET {IP_REF_DATA_URL}/IPExternalSamplingService/ReferenceData/Currencies HTTP/1.1
```

### Parameters

 - None

### Header

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| Partner_AUTH_Key | ```string``` | Authorization of Reference Data access | Yes |

### Body Details

 - None

---

## Response

### Possible Codes

| Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 403 | Forbidden. Invalid Partner_AUTH_Key |
| 500 | Internal Error. An exception occurrec while processing the request. Contact Toluna for resolution. Toluna will likely have the details caputred in its logs |

### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| CurrencyID | ```int``` | Unique identifier for a currency |
| Name | ```string``` | Name of currency |
