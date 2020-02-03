---
title: Quota Status
has_children: false
parent: Notifications
nav_order: 4
---

# Quota Status Notifications

A new feature for the ES Integration, Toluna will deliver these notifications when one of its Quotas is not longer available for sompling or any of its perviously on-hold Quotas become available for sampling. 
>A Partner must consume this event so that its sampling efforts can be discontinued when no longer viable.

#### Notification from Toluna to Partner API

Toluna will deliver this via HTTP POST when one of its Quotas is no longer available for sampling or any of its previously on-hold Quota becomes available for sampling. It is the Partner’s responsibility to create an endpoint capable of consuming this information. Please note that subscribers will receive updates for all Quotas, not just those with which they are engaged. Partners should construct their endpoint in a manner in which non-relevant Quota updates are ignored.

#### Route(s)

- Specified by Partner; Toluna will confingure accordingly
 
#### HTTP Verb

- POST
 
#### Sample Request
```json
POST [Partner-Specified URL]
```

#### Sample POST
```json
 {
  "QuotaID": 3445365,
  "SurveyID": 45367678,
  "WaveID": 45367678,
  "IsLive": false,
  "UpdateDateTimeUTC": “2018-10-22 19:58:42.99 +00:00“
 }
```

#### Response Properties

| Name | Type | Description |
| :--- | :--- | :--- |
| QuotaID | int | Toluna's unique identifier for a Quota |
| SurveyID | int | Toluna's internal unique identifier for a Survey |
| WaveID | int | Toluna's internal unique identifier for a single iteration of a Survey. The SurveyID+WaveID is always unique |
| IsLive | Bool | Is the Quota currently capable of accepting Sample? |
| UpdateDateTimeUTC | dateTime | The date/time, in UTC, of the quota status change |