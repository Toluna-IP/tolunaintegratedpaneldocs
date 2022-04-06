---
title: Respondent Rejection Types
has_children: false
nav_order: 10
parent: Reference Data API
grand_parent: Mapping

---

# Respondent Rejection Types
{: .no_toc }

Returns a list of all rejection types and their details.

* TOC
{:toc}

---

## Request

### Route
```
GET {IP_REF_DATA_URL}/IPUtilityService/ReferenceData/Rejectiontypes 
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
GET {IP_REF_DATA_URL}/IPUtilityService/ReferenceData/Rejectiontypes 
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
| RespondentRejectionTypeID | ```int``` | Toluna's unqiue identifier for a rejection |
| PartnerRejectionName | ```string``` | Name of a rejection |
| PartnerRejectionDescription | ```string``` | Description of the rejection |

 - Please note: RespondentRejectionTypeID 99 refers to a screenout after a member has entered the survey.

### Example Response
```plaintext
[
...
{
    "RespondentRejectionTypeID": 4,
    "PartnerRejectionName": "SurveyTaken",
    "PartnerRejectionDescription": "Respondent has already taken the survey."
},
...
]
```