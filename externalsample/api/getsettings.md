---
title: Get Settings
has_children: false
parent: ES API
grand_parent: External Sample Offering
nav_order: 7
---


# Get Settings
{: .no_toc }

For a Toluna-issued "PanelGUID," returns a list of settings and their associated valuse (end-pages URLs, notifaction URLs, encryption details).

* TEST
{:toc}

---


## Request

### Route
```plaintext
GET http://{IP_ES_URL}/IntegratedPanelService/api/Settings?partnerGUID={PanelGUID}
```

### Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| PanelGUID | ```Guid``` | A Toluna-issued unique identifier for a Partner’s culture-specific panel. | Yes |


### Header

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| API_AUTH_KEY | ```GUID``` | A Partner-specific GUID provided by Toluna | Yes |

### Body Details

 - None

### Example Request

```
GET http://{IP_ES_URL}.com/IntegratedPanelService/api/Settings?partnerGUID=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX
API_AUTH_KEY: XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX
```
---
## Response

### Possible Codes

| Code | Etiology, action |
| :--- | :--- |
| 200 | Request processed normally |
| 400 | Bad Request: See response for details |
| 403 | Forbidden: invalid API_AUTH_KEY. See response for details |
| 500 | Internal Error. An exception has occurred while processing the request. Toluna likely has captured the details in its logs |


### Body Details
 - None


### Example Response
```plaintext
[
  {
    "Name": "Qualified URL",
    "Description": "Url where members are sent when they complete a survey.",
    "Value": "https://example.yourdomain.com/test/001?pid=[pid]"
  },
  {
    "Name": "Terminate URL",
    "Description": "Url where members are sent when they terminate a survey.",
    "Value": "https://example.yourdomain.com/test/002?pid=[pid]"
  },
  {
    "Name": "Quota Full URL",
    "Description": "Url where members are sent when they are not able to participate in a survey due to the quota being full.",
    "Value": "https://example.yourdomain.com/test/003?pid=[pid]"
  },
  {
    "Name": "Fraud Terminate URL",
    "Description": "Url where members are sent when they are marked as fraudulent activity in a survey. ",
    "Value": "https://example.yourdomain.com/test/004?pid=[pid]"
  },
  {
    "Name": "Digital Finger Printing Failure URL",
    "Description": "Url where members are sent when they are not able to be fingerprinted (fraud reduction).",
    "Value": "https://example.yourdomain.com/test/005?pid=[pid]"
  },
  {
    "Name": "No Surveys URL",
    "Description": "Url where members are sent when there are no surveys available. ",
    "Value": "https://example.yourdomain.com/test/006?pid=[pid]"
  },
  {
    "Name": "Survey Taken URL",
    "Description": "Url where members are sent when they have already taken the survey.",
    "Value": "https://example.yourdomain.com/test/007?pid=[pid]"
  },
  {
    "Name": "No Cookies URL",
    "Description": "Url where members are sent when a member does not have cookies enabled. ",
    "Value": "https://example.yourdomain.com/test/008?pid=[pid]"
  },
  {
    "Name": "Survey Not Available URL",
    "Description": "Url where members are sent when the survey is no longer available. ",
    "Value": "https://example.yourdomain.com/test/009?pid=[pid]"
  },
  {
    "Name": "Not Qualified URL",
    "Description": "Url where members are sent when they do not qualify for a survey. ",
    "Value": "https://example.yourdomain.com/test/010?pid=[pid]"
  },
  {
    "Name": "Max Surveys Reached URL",
    "Description": "Url where members are sent when they've taken the max number of surveys for that day.",
    "Value": "https://example.yourdomain.com/test/011?pid=[pid]"
  },
  {
    "Name": "Max Surveys To Fetch",
    "Description": "Max number of surveys returned in Dashboard Get Surveys call.",
    "Value": "0"
  },
  {
    "Name": "Invite Notification URL",
    "Description": "Url where invite notifications / requests are sent.",
    "Value": null
  },
  {
    "Name": "Completion Notification URL",
    "Description": "Url where member-status qualified complete notifications are sent.",
    "Value": "https://example.yourdomain.com/test/comp.php"
  },
  {
    "Name": "Terminate Notification URL",
    "Description": "Url where member-status terminate notifications are sent.",
    "Value": "https://example.yourdomain.com/test/term.php"
  },
  {
    "Name": "Survey Notification URL",
    "Description": "Url where notifications are sent for surveys that are marked as closed.",
    "Value": "https://example.yourdomain.com/test/closed.php"
  },
  {
    "Name": "Reference Data API Auth Key",
    "Description": "Authorization key needed to access Reference Data API.",
    "Value": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX"
  },
  {
    "Name": "Panel GUID",
    "Description": "Unique Identifier for Partner and this culture.",
    "Value": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX"
  },
  {
    "Name": "Quota Notifications Enabled",
    "Description": "Denotes whether the Sample Partner is enabled to receive the quota notifications.",
    "Value": "True"
  },
  {
    "Name": "Quota Notification URL",
    "Description": "URL where notifications are sent for quota status updates.",
    "Value": "https://example.yourdomain.com/test/quota.php"
  },
  {
    "Name": "Standard EncryptionResult Parameter Name",
    "Description": "The name of parameter which will hold the encrypted value.",
    "Value": null
  }
]
```