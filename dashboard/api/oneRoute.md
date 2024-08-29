---
title: Single-Route GetSurveys
has_children: false
nav_order: 99
parent: Dashboard API
grand_parent: Dashboard Offering
nav_exclude: true
search_exclude: true
---

# Single-Route Member Registration and GetSurveys
{: .no_toc }

* TOC
{:toc}

--- 

## Background

Toluna offers a one-route option to register a new member and retrieve a number of surveys for the newly-created member using a single API call. Details of this call can be found below. Notably, the parameters included in the body of the call are identical to the parameter of the [Register Member API](membermanagement\v2\add.md) and [GetSurvey API](dashboard\api\getsurveys.md).

This route can be used for preexisting members. In the case of an existing member, any updates or changes made to the "NewIPMemberInfo" object will be ignored. If you would like to update an existing member, you must use the [Update Member API](membermanagement\v2\update.md).

## Request

### Route
```plaintext
POST https://{IP_CORE_URL}/IntegratedPanelService/api/Surveys/RegisterMemberAndGetSurveys
```

### Body Details

| Name | Type | Description | Required? | 
| :--- | :--- | :---: |
| NewIPMemberInfo | ```list<object>``` | New member's registration information | Yes |
| SurveysRequest | ```list<object>``` | Survey request information | Yes |

#### NewIPMemberInfo Object 

> Note: while the object states "New", this route can also be used for existing members.

| Property | Description | Type | Required? |
| :--- | :--- | :--- | :---: |
| PartnerGUID | ```GUID``` | Unique Partner Code (Please request from Toluna if you don’t have one) | Yes |
| MemberCode | ```string``` | Unique Respondent Code from the Partner | Yes |
| IsActive | ```bool``` | Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool.| No |
| BirthDate | ```string``` | MM/DD/YYYY format | No |
| PostalCode | ```string``` | Member postal code | No |
| IsTest | ```bool``` | Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used **ONLY** during testing | No |
| AnsweredQuestions | ```string``` | A collection of 0:M demographic Question and Answer ID pairs - **Currently available - will be marked as "obsolete" and deprecated in an year**  | No |
| RegistrationAnswers | ```string``` | Supports multi-select and open-ended answers. This will also maintain current single select responses | No |


#### SurveysRequest Object

| Property | Description | Type | Required? |
| :--- | :--- | :--- | :---: |
| NumberOfSurveys | Number of Surveys the Partner is requesting to receive to show the Member (maximum 5 available) | ```int``` | Yes |
| DeviceTypeIDs | Indicated the device types for which Surveys should be returned. Supported values: 1=Desktop/Laptop, 2=Tablet, 3=Phone | ```list<int>``` | Yes |

#### Example API Body

```plaintext
{
    "NewIPMemberInfo": {
        "PartnerGUID": "{{partnerGuid}}",
        "MemberCode": "OneRouteAPI-test-01",
        "BirthDate": "3/7/1982",
        "IsActive": true,
        "IsTest": false,
        "AnsweredQuestions": [
        {
            "QuestionID": 1001007,
            "AnswerID": 2000246
        }
        ]
    },
    "SurveysRequest":{
        "NumberOfSurveys":5,
        "DeviceTypeIDs": [1]
    }
}
```


## Response

### Possible Codes

| Code | Etiology, actions |
| :--- | :--- |
| 200 | OK. Request processed normally, results returned without issue |
| 400 | Bad Request. Request is malformed or incomplete. Review message details and take appropriate action |
| 500 | Internal Error. An exception occurred while processing the request. Toluna likely has the details captured in its logs |

### Body Details

| Name | Type | Description |
| :--- | :--- | :--- |
| SurveyID | ```int``` | Toluna-specified Survey identifier |
| Name | ```string``` | Toluna-specified Survey name |
| URL | ```string``` | Clicking on the URL will take this specific Respondent to the survey. URL’s are unique to the respondent and are **NOT** to be used by other respondents. |
| Duration | ```int``` | Estimated length of interview |
| IR | ```int``` | Incidence rate fo the Survey in % |
| MemberAmount | ```decimal``` | This is currently only returned as a value > 0 if the partner has a specific amount that is paid to each of their respondents for a survey |
| PartnerAmount | ```decimal``` | Amount Toluna has agreed to pay Partner for a complete. The value shown is linked to the URL and is valid for any complete generated from a member's interaction with the link, regardless of changes to the LOI and IR of the survey |
| WaveId | ```int``` | Current iteration of the survey. Studies related to one another can be sent in “waves” that the Member experiences as unique surveys. SurveyID+WaveId is always unique |

### Example 200 Response
```plaintext
    {
        "SurveyID": 3588164,
        "WaveId": 2083231,
        "Name": "3403954_US_84006872",
        "URL": "https://ups.surveyrouter.com/TrafficUI/MSCUI/Page.aspx?pgtid=20&di=L9tWZRI0726x5Pz0DxeCf3LnTO8sxWE2reRxBBrBleV9prmymw63ezE33sbdQ6nXJvVQE30vBi1IoS60bCztUTmr3xHwE4E41107",
        "Duration": "15",
        "IR": 70,
        "MemberAmount": 0.0,
        "PartnerAmount": 0.20
    },
```