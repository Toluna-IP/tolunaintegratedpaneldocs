---
title: Get Member
has_children: false
parent: Static (v1)
grand_parent: Member Management
nav_order: 2
---


# Member GET (v1)
{: .no_toc }

A partner can receive details for members in the Toluna IP database using an HTTP **GET**.

* TOC
{:toc}

---

## Request

### Route

```GET http://{IP_CORE_URL}/IntegratedPanelService/api/Respondent```

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

```GET http://{IP_Core_URL}/IntegratedPanelService/api/Respondent/?memberCode={MemberCode}&partnerGuid={partnerGUID}```

---

## Responses

### Possible Codes

| Response Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, existing Member Panelist was updated without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 500 | Internal Error. An exception occured while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs | 

### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| MemberCode | ```int``` | Toluna's unique identifier for a Member |
| LanguageID | ```int``` | Member's selected language profiler code |
| Language | ```string``` | Member's selected language profiler identification |
| CountryID | ```int``` | Member's selected country profiler code |
| Country | ```string``` | Member's selected country profiler identification |
| GenderID | ```int``` | Member's selected gender profiler code |
| Gender | ```string``` | Member's selected gender profiler identification |
| EducationID | ```int``` | Member's selected education profiler code |
| Education | ```string``` | Member's selected education profiler identification |
| IncomeID | ```int``` | Member's selected income profiler code |
| Income | ```string``` | Member's selected income profiler identification |
| EthnicityID | ```int``` | Member's selected ethnicity profiler code |
| Ethnicity | ```string``` | Member's selected ethnicity profiler identification |
| RaceID | ```int``` | Member's selected race profiler code |
| Race | ```string``` | Member's selected race profiler identification |
| WorkPositionID | ```int``` | Member's selected work position profiler code |
| WorkPosition | ```int``` | Member's selected work position profiler identification |
| IsActive | ```bool``` | Defaults TRUE. Allows member to be selected for Surveys. If Members opts out of Survey, use PUT call to disallow Surveys sent to Member |
| Email | ```string``` | Member's email |
| BirthDate | ```date``` | Member's birthdate. Format: {DayofWeek}, {Month} DD, YYYY |
| PostalCode | ```int``` | Member's selected postal code profiler |
| PanelistStatusTypeID | ```int``` | Integer value defining the current state of the Member in the Toluna platform. Possible values are: 1=Active, 2=OptOut, 3=Suspended, 4=BlockedForAbuse, 5=PIIDateRegulated. **Note:** Any value other that "1" will prohibit Members from participating in Toluna's Surveys |
| CultureID | ```int``` | Integer identifier for the culture the Member is associated with. See data mapping document for further detailsInte |
| SubProvinceID | ```int``` | Integer identifier for the Sub Province the Member is associated with. See data mapping document for further details |

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
