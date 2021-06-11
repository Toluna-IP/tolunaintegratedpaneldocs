---
title: Rejection Types
has_children: false
nav_order: 998
parent: Reference Data API
grand_parent: Mapping
---

# Cultures
{: .no_toc }

Returns a list of all rejection types and their details.

* TOC
{:toc}

---

## Request

### Route
```
GET {IP_REF_DATA_URL}/IPUtilityService/ReferenceData/RejectionTypes 
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
GET {IP_REF_DATA_URL}/IPUtilityService/ReferenceData/RejectionTypes 
Content-type: application/json
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
| RespondentRejectionTypeID | ```int``` | Toluna's unqiue identifier for a rejection type. Will be included in [Enhanced Terminate Notification](/general/changelog.html#613) details |
| PartnerRejectionName | ```string``` | Toluna's name for a rejection type |
| PartnerRejectionDescription | ```string``` | Description of the rejection explaining the nature of the scenario with which this rejection will be used |

### Example Response
```plaintext
[
...
{
    "RespondentRejectionTypeID": 70,
    "PartnerRejectionName": "IncorrectRespondentCountry",
    "PartnerRejectionDescription": "The country stated by the user does not match the country from where the web request originates."
},
...
]
```