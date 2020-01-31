---
title: Get Member
has_children: true
parent: Dynamic (v2)
grand_parent: Member API
nav_order: 2
---



## Member Get

### Request Parameters

| Name | Description |
| :--- | :--- |
| memberCode | Unique Respondent Code from the Partner |
| partnerGUID | Unique Partner Code (Please request this from Toluna if you don't have one) |


### Headers

All requests made using Dynamic member management (v2) must include the following header:
```json
Accept: application/json;version=2.0
```

### Route
```plaintext
GET http://{IP-Core-URL}/IntegratedPanelService/api/Respondent/?memberCode={memberCode}&partnerGUID={partnerGUID}
```

### Possible Request Responses

| Response Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, existing Member Panelist was updated without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 500 | Internal Error. An exception occurrec while processing the request. Contact Toluna for resolution. Toluna will likely have the details caputred in its logs |

