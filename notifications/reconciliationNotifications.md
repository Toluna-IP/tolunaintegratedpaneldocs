---
title: Reconciliation Notifications
has_children: false
nav_order: 5
parent: Notifications
nav_exclude: true
search_exclude: true
---


# Reconciliation Notifications


After a Member completes a Survey, their response information is sent to the Buyer. The Buyer reviews the data and confirms the validity of each Respondents' attempt. In the event an attempt is rejected by a Buyer, Toluna can notify a Partner of this rejection using automated Notifications. These Notifications are not mandatory, but can be very useful to Partners as they allow for a more timely management of reconciliations. 

* TOC
{:toc}

---

## Request Details

Below are details on how Reconciliation Notifications are processed. If you are an existing Partner and would like to enable these Notifications, please contact your Toluna Representative.

### HTTP Verb

- POST

### Route

- Specified by the Partner; Toluna will configure accordingly.

### Header

- A single, custom header will be used with Notifications, both of which are specified by the Partner; Toluna will configure accordingly.

| Header Key | Value | Required? |
| :--- | :--- |
| {{ProvidedByPartner}} | {{ProvidedByPartner}} | Yes |

### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| SurveyId | ```int``` | Toluna's unique identifier for a Survey |
| SurveyRef | ```string``` | Toluna's Survey name | 
| WaveId | ```int``` | Current iteration of the Survey. Studies related to one another can be sent in “waves” that the Member will experience as a unique Survey |
| QuotaId | ```int``` | Toluna’s unique identifier for a quota |
| UniqueCode | ```string``` | Unique Respondent Code used to register the Member by the Partner |
| IsAutoRouted | ```bool``` | Indicates whether the Member was auto-routed or not |
| OriginalSurveyId | ```int``` | SurveyID to which the Member was originally invited. Nullable | 
| ReconciliationId | ```int``` | Toluna's unique identifier used to indicate the reason for Reconciliation |
| Revenue | ```int``` | Amount paid to the Partner by Toluna for the initial Complete in 1/100 of the currency units (eg 100=100 cents or $1 USD). This amount will be deducted from a future invoice issued to Toluna by the Partner |
| OriginalCompleteDateTime | ```string``` | Date and time of initial Respondent completion. Format “YYYY-MM-DD HH:MM:SS” in UTC Time |
| ReconciliationDateTime | ```string ``` | Date and time of reconciliation. Format “YYYY-MM-DD HH:MM:SS” in UTC Time | 

### Data Format

- The above body details will always be provided in JSON format.

### Example Request Body

```json
{
    "SurveyId": 123,
    "SurveyRef": "123560-US",
    "WaveId": 100,
    "QuotaId": 987654,
    "UniqueCode": "111abc",
    "IsAutoRouted": false,
    "OriginalSurveyId": null,
    "ReconciliationId": 90,
    "Revenue": 45,
    "OriginalCompleteDateTime": "2026-05-17T15:40:03.350Z",
    "ReconciliationDateTime": "2026-06-09T18:06:15.647Z"
}
```