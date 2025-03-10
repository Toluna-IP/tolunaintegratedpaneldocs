---
title: Initialization
has_children: false
nav_order: 2
parent: SDK Offering
---

# Initialization Details
{: .no_toc }

Parameters and objects needed for SDK initialization are listed and described below.

* TOC
{:toc}

## Parameters

| Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| PartnerAuthKey | ```string``` | Authorization key provided by Toluna used to pull metadata from Toluna's system | Yes |
| Customization | ```object``` | Object that includes theme and UI customization settings | No |
| MemberDetails | ```object``` | Object that includes mapped user details and responses to corresponding Toluna question options | No |
| DebugMode | ```bool``` | Enable logs in console for debugging | No |
| MockMode | ```bool``` | Enable mock data in Surveys Wall | No |

### MemberDetails Object

Members can be registered via the SDK's [Registration Method](/sdk/methods.html#registration) or through use of the [Member Management API](/membermanagement/). The Registration Method can be used directly by the Partner before providing the Member with a Survey/Offer wall. To do so, include the following properties for the MemberDetails object. Without MemberDetails, the Registration Method will prompt a Member to answer demographic questions before routing to the Survey/Offer wall.

#### Properties

- PartnerGuid: Unique Partner Code (Please request from Toluna if you don’t have one)
- MemberCode: Unique Respondent Code from the Partner
- PostalCode: Member postal code
- BirthDate: MM/DD/YYYY format
- IsActive: Defaults TRUE. When TRUE, Member is eligible to take Surveys. When FALSE, Member is excluded from the Survey Routing pool.
- IsTest: 	Defaults FALSE. When TRUE the Member by-passes all Toluna duplication validation routines. Among other things, this makes the eligible to take Surveys multiple times from the same physical machine. Should be used ONLY during testing
- RegistrationAnswers: 	Supports multi-select and open-ended answers. This will also maintain current single select responses

### Customization Object

To ensure a seamless Member experience, Partners can customization the look of the SDK pages and forms to match their own. Below are the different available configurations

#### Properties


- Primary Color (Hex Code): Primary color for UI components
- Secondary Color (Hex Code): Secondary color for UI components
- NumberOfSurveys: Maximum Number Of Surveys to Fetch
- Maximum LOI: Maximum length of the surveys in the survey list
- SurveyViewType: View type of the survey screen shown. Pop-Up = 1, Integrated = 2
- FontFamily: Font of the test shown
- DarkMode: To toggle dark theme
- LogoName: Name of the Logo file for uploading it into the SDK
- LogoEnabled: To Enable the logo in the views
