---
title: Methods
has_children: false
nav_order: 3
parent: SDK Offering
---

# Methods
{: .no_toc }

Partners can trigger methods defined by the SDK to register Members and display available surveys to them. Below is an explanation of each method available.

* TOC
{:toc}


## Registration

The Registration method is responsible for rendering a registration form to collect the Member's missing information. It determines which questions to display based on the following conditions:
- Country: Displayed if the culture is not provided.
- Zip Code: Displayed if the zip-code is not provided.
- Date Of Birth: Displayed if the birth date is not provided. 
- Gender: Displayed if the gender is not provided.

If all the above details are provided, no questions will be displayed, and the Member will either be registered or updated depending on their current registration status. In this case, the method renders a loading screen to ensure seamless Member experience without leaving the screen blank. Once the form is submitted, a callback is triggered with the memberCode and cultureGuid parameters, providing the necessary Member details.

## Surveys

The Surveys method displays all available surveys for the Member in a survey wall, presented in a list-box style layout. If there are no surveys available or the Member has not completed the registration process, the method will display a "No Surveys Available" message, informing the Member about the absence of surveys.

## SurveyFlow Method

The SurveyFlow method combines the functionality of the Registration and Surveys methods to create a streamlined experience. Based on the Member's status:
- If the Member is already registered, the method directly calls the Surveys method to show the available surveys.
- If the Member is not registered, the method first invokes the Registration method to gather the Member's information. After successfully completing registration, it automatically calls the Surveys method to display the available surveys.


This method simplifies the integration process by managing the flow between registration and surveys seamlessly based on the Member's state.

## Method Flowchart

The following flowchart provides a detailed explanation of each method in the SDK

![SDKmethodFlowchart](https://github.com/Toluna-IP/tolunaintegratedpaneldocs/blob/master/resources/SDKflowchart.png)