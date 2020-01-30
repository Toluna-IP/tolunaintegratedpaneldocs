---
title: GET
has_children: true
parent: Static (v1)
grand_parent: Member API
nav_order: 1
---


## Member GET (v1)

A partner can receive details for members in the Toluna IP database using an HTTP **GET**.

URL to **GET** new member info: http://{IP-Core-URL}/IntegratedPanelService/api/Respondent



### Parameters:
 
The following parameters are required for MemberGET

| Name        | Description          |
| :------------- | :------------------ |
| memberCode           | Unique Respondent Code from the Partner |
| partnerGuid | Unique Partner Code   |



### Route:

 - GET http://{IP-Core-URL/IntegratedPanelService/api/Respondent/?memberCode={memberCode}&partnerGuid={partnerGUID}


### Possible Responses

| Response Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, existing Member Panelist was updated without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 500 | Internal Error. An exception occured while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs | 

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