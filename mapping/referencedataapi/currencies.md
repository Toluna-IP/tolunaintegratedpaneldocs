---
title: Currencies
has_children: false
nav_order: 4
parent: Reference Data API
grand_parent: Mapping

---

# Currencies
{: .no_toc }

Returns a list of all currency types.

* TOC
{:toc}

---

## Request

### Route
```
GET {IP_REF_DATA_URL}/IPUtilityService/ReferenceData/Currencies 
```

### Parameters

 - None

### Header

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| PARTNER_AUTH_KEY | ```string``` | Authorization of Reference Data access | Yes |

### Body Details

 - None

### Example Request
```plaintext
GET {IP_REF_DATA_URL}/IPUtilityService/ReferenceData/Currencies 
Content-Type: application/json
PARTNER_AUTH_KEY: XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
```

---

## Response

### Possible Codes

| Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 403 | Forbidden. Invalid PARTNER_AUTH_KEY |
| 500 | Internal Error. An exception occurred while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs |

### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| CurrencyID | ```int``` | Unique identifier for a currency |
| Name | ```string``` | Name of currency |

### Example Response
```plaintext
[
...
  {
    "CurrencyID": 12,
    "Name": "New Zealand Dollar"
  },
...
]
```