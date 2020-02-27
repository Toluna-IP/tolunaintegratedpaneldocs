---
title: Quota Status
has_children: false
parent: Notifications
nav_order: 4
---

# Quota Status Notifications
{: .no_toc}

A new feature for the ES Integration, Toluna will deliver these notifications when one of its Quotas is no longer available for sampling or any of its perviously on-hold Quotas become available for sampling. 

* TOC
{:toc}

---


## Notification from Toluna to Partner API

Toluna will deliver this via HTTP POST when one of its Quotas is no longer available for sampling or any of its previously on-hold Quotas becomes available for sampling. It is the Partner’s responsibility to create an endpoint capable of consuming this information. Please note that subscribers will receive updates for all Quotas, not just those with which they are engaged. Partners should construct their endpoint in a manner in which non-relevant Quota updates are ignored.

### HTTP Verb

- POST

### Route(s)

- Specified by Partner; Toluna will confingure accordingly

### Notification Properties

| Name | Type | Description |
| :--- | :--- | :--- |
| QuotaID | ```int``` | Toluna's unique identifier for a Quota |
| SurveyID | ```int``` | Toluna's unique identifier for a Survey |
| WaveID | ```int``` | Toluna's unique identifier for a single iteration of a Survey. The SurveyID+WaveID is always unique |
| IsLive | ```Bool``` | Is the Quota currently capable of accepting Sample? |
| UpdateDateTimeUTC | ```dateTime``` | The date/time, in UTC, of the quota status change |

### Formats Available

Quota status notifications are avialable in JSON and XML formats. Below are examples in the JSON format.

### Example JSON Request
```plaintext
POST {Partner-Specified URL}
```

### Example JSON Notification
```plaintext
 {
  "QuotaID": 3445365,
  "SurveyID": 45367678,
  "WaveID": 45367678,
  "IsLive": false,
  "UpdateDateTimeUTC": “2018-10-22 19:58:42.99 +00:00“
 }
```

