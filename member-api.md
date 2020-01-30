---
title: Member API
has_children: true
nav_order: 2
---

# Member Management API 

Integrated Panel (IP) is an offering for our partners that allow them to receive a request to invite their own panel to Toluna      surveys that have demographics (Age, Gender, Country, and Language etc.) that will match those of the individual panelist.

No personal information regarding the partner’s panel is received or stored by Toluna. The partner need only supply a unique    numeric “Member ID” that will be passed back to them when an invite is made.  

Toluna can receive the partner’s panel data via RESTful APIs. A partner can use these APIs to add new members or deactivate    members. Please request the mapping values for the demographics from your Toluna account representative. Most values vary by    country. The API details are outlined below.

>**Please Note:** Once members are added to the Toluna IP Database, they cannot be removed. Members may only be updated or deactivated. Details on how to peform these actions are outlined below.


## Member GET

A partner can receive details for members in the Toluna IP database using an HTTP **GET**.

URL to **GET** new member info: http://{IP-Core-URL}/IntegratedPanelService/api/Respondent

Speak to your Toluna representative to recieve your Partner-specific {IP-Core-URL}.


### Parameters:
 
 
 

| Name        | Description          | Required |
|:-------------|:------------------|:------|
| memberCode           | Unique Respondent Code from the Partner | Y  |
| partnerGuid | Unique Partner Code   | Y  |



### Route:
```http

GET http://ip.surveyrouter.com/IntegratedPanelService/api/ Respondent
/?memberCode=1601440000&partnerGuid=CC265C63-F887-4366-9ED1-7B2B3BD94C2B

````

### Sample Response:
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


