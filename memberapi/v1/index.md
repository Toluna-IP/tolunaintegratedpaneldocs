---
title: Static (v1)
has_children: false
parent: Member API
nav_order: 1
---


# Static v1

Within the Toluna IP Database, the Partner has a couple options on how they manage member date. The partner can choose to use either static or dymanic data. Below are insructions on using static data. Information on managing members with dynamic data can be found [here](https://josh-toluna.github.io/tolunaintegratedpaneldocs/memberapi/v2/ "v2-Dyanamic Member Management"). 


## Adding a Member (POST)

A partner can add new members to the Toluna IP Database using an HTTP POST. This must be done by the partner before requesting or receiving survey opportunity links.

#### Parameters
 - None
 
#### Request Details

| Property | Description                                                     |
| :--------| :--- |
| PartnerGUID | Unique Partner Code (Please request from Toluna if you don’t have one) |
| MemberCode | Unique Respondent Code from the Partner |
| Active | (Optional) Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool. |
| GenderID | (Optional) Values from the data mapping file |
| EducationID | (Optional) Values from the data mapping file |
| IncomeID | (Optional) Values from the data mapping file |
| EthnicityID | (Optional) Values from the data mapping file |
| RaceID | (Optional) Values from the data mapping file |
| SubProvinceID | (Optional) Values from the data mapping file |
| Email | (Optional) |
| BirthDate | (Optional) MM/DD/YYYY format |
| PostalCode | (Optional) |
| IsTest | (Optional) Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used **ONLY** during testing. |

#### Route
 - POST http://{IP-Core-URL}/IntegratedPanelService/api/Respondent
 - Example
 ```json
{
 "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",  
 "MemberCode": "111", 
 "Active": "true", 
 "GenderID": "2000247", 
 "EducationID": "2002275", 
 "IncomeID": "2796381", 
 "EthnicityID": "2000264",
 "RaceID": "0", 
 "Email": "test@test.com", 
 "BirthDate": "6/21/1914", 
 "PostalCode": "OU812", 
 "SubProvinceID": "3091832"
}
```
#### Possible Responses

| Response Code | Etiology, actions |
| :--- | :--- |
| 201 | Created. Request processed normally, resulting in a new Member Panelist |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take apporpriate action |
| 409 | Conflict. An attempt to add a Member that already exists. Duplication is determined by the combination of MemberCode and PartnerGUID |
| 500 | Internal Error. An exception occured while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs |

#### Notes
> - Only new Members can be added. To update, use the PUT route noted below
> - Option Properties can be excluded from the request. "GenderID," "EducationID," "IncomeID," "EthnicityID," "RaceID," and "SubProvinceID" can also take "0" to indicate "no value."
> - Invalid Property data typically returns a 400 response

#### Examples
 ```json
{
 "PartnerGUID": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",  
 "MemberCode": "111", 
 "Active": "true", 
 "GenderID": "2000247", 
 "EducationID": "2002275", 
 "IncomeID": "2796381", 
 "EthnicityID": "2000264",
 "RaceID": "0", 
 "Email": "test@test.com", 
 "BirthDate": "6/21/1914", 
 "PostalCode": "OU812", 
 "SubProvinceID": "3091832"
}
```

## Member GET

A partner can receive details for members in the Toluna IP database using an HTTP **GET**.

URL to **GET** new member info
 - For Partners using Notification or Dashboard Intergration Offering: http://{IP-Core-URL}/IntegratedPanelService/api/Respondent
 - **For Parters using External Sample (ES) Integration Offering: http://{ES-Core-URL}/ExternalSample/**

Speak to your Toluna representative to recieve your Partner-specific {IP-Core-URL} or {ES-Core-URL}.


#### Parameters:
 
The following parameters are required for MemberGET

| Name        | Description          |
| :------------- | :------------------ |
| memberCode           | Unique Respondent Code from the Partner |
| partnerGuid | Unique Partner Code   |



#### Route:

 - GET http://{IP-Core-URL/IntegratedPanelService/api/Respondent/?memberCode={memberCode}&partnerGuid={partnerGUID}


#### Possible Responses

| Response Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, existing Member Panelist was updated without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 500 | Internal Error. An exception occured while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs | 

#### Example Response:
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

## Member Update (PUT)

Existing Members can be updated using HTTP PUT. “PartnerGUID” and “MemberCode” are required. Combine them with optional properties to update a Member according to your requirements.

#### Parameters
 - None
 
#### Request Details

| Property | Description |
| :--- | :--- |
| PartnerGUID | Unique Partner Code (Please request from Toluna if you don't have one |
| MemberCode | Unique Respondent Code from the Partner (alphanumeric 256 character limit |
| Active | (Optional) Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool |
| GenderID | (Optional) Values from the data mapping file |
| EducastionID | (Optional) Values from the data mapping file |
| EthicityID | (Optional) Values from the data mapping file |
| RaceID | (Optional) Values from the data mapping file |
| SubProvinceID | (Optional) Values from the data mapping file |
| Email | (Optional) |
| BirthDate | (Optional) MM/DD/YYYY format |
| PostalCode | (Optional) |
| IsTest | (Optional) Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used **ONLY** during testing. |
| IsPIIDataRegulated | (Optional) Defaults FALSE. When TRUE, all personally identifiable information is removed. |

#### Route
**PUT** http://{IP-Core-URL}/IntegratedPanelService/api/Respondent

#### Possible Responses

| Response Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, existing Member Panelist was updated without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 404 | Not Found. An attempt to update a Member that does not exist. Existence is determined by the combination of MemberCode and PartnerGUID |
| 500 | Internal Error. An exception occured while processing the request. Contact Toluna for resolution. Toluna will likely have the details captured in its logs |
