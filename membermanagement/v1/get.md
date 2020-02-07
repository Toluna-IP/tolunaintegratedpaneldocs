---
title: Get Member
has_children: true
parent: Static (v1)
grand_parent: Member Management
nav_order: 2
---


# Member GET (v1)
{: .no_toc }

* TOC
{:toc}

---

## Introduction

A partner can receive details for members in the Toluna IP database using an HTTP **GET**.

---

## Request

### Route

```GET http://{IP-Core-URL}/IntegratedPanelService/api/Respondent```

### Parameters:

| Name | Description | Required? |
| :--- | :--- | :---: |
| memberCode | Unique Respondent Code from the Partner | Yes |
| partnerGuid | Unique Partner Code | Yes |

### Header

 - None
 
### Body Details

 - None
 
### Example
```wrap
GET http://{IP_Core_URL}/IntegratedPanelService/api/Respondent/?memberCode={MemberCode}&partnerGuid={partnerGUID}
```

---

## Responses

### Possible Codes

| Response Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, existing Member Panelist was updated without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 500 | Internal Error. An exception occured while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs | 

### Body Details

*To do*

### Example Response:
``` 
{
    "MemberCode": "1601440000",
    "LanguageID": 2000245,
    "Language": "Français",
    "CountryID": 2000073,
    "Country": "France",
    "GenderID": 2000247,
    "Gender": "Homme",
    "EducationID": 2002274,
    "Education": "Bac+4",
    "IncomeID": 2002335,
    "Income": "Je ne sais pas / préfère ne pas répondre",
    "EthnicityID": 0,
    "Ethnicity": "",
    "RaceID": 0,
    "Race": "",
    "WorkPositionID": 0,
    "WorkPosition": "",
    "Active": true,
    "Email": "",
    "BirthDate": "Tuesday, July 11, 2000",
    "PostalCode": "75001",
    "PanelistStatusTypeID": 0,
    "CultureID": 6,
    "SubProvinceID": "3091832"
}

```
---
