---
title: Flutter
has_children: false
nav_order: 6
parent: SDK Offering
---

# Flutter
{: .no_toc }

Below are instructions on using the SDK Flutter package.

* TOC
{:toc}

## Step 1: Add SDK to Your Project

1.	Download the SDK package for Flutter
2.	Add the SDK dependency to the configuration file pubspec.yaml.
- ``` dependencies: integrated_panel: ^1.0.0  ```
3. Get all the package dependencies of Android by running ```flutter pub get. ```
4. To get all the package dependencies of IOS, run flutter pod update

## Step 2: Initialize the SDK

```plaintext
import 'package:integrated_panel/integrated_panel.dart';

void main() {
    Member member = Member(
        memberCode: "< Member Unique Code>",
        partnerGUID: "<Culture Guid >",
        isActive: true,
        isTest: true,
    );
    
    final customization = SDKCustomization(
        mainColor: Color(0xff003399),
        secondaryColor: Colors.green,
        fontFamily: 'Roboto',
        surveyViewType: 1,
        isDarkMode: false,
        maxLOI: 10,
        numberOfSurveys: 20,
        logoAssetPath: "<Logo path same as in the pubspec yaml>",
        LogoEnable: true
    );
    
    const appkey = '<Partner Auth Key>';
    
    await IntegratedPanel.initialize(
        partnerAuthKey: appkey,
        debugMode: false,
        mockMode: false,
        prodMode: false,
        customization: customization,
        member: member,
        cultureAssetPath: "< Culture path same as in the pubspec         yaml>",
    );
    
    runApp(MyApp());
}
```

## Step 3: Use SDK Methods


### Registration Method

The below code snippet can be used to invoke the Registration method.
> Note: Only call this method if the Member is not registered or there is a need to update the details of the member. If already registered and there is no need to update the member details directly invoke the Surveys method.

```plaintext
IntegratedPanel.registrationView(
    onSaved: (response) {
        if(!response.isEmpty) {
            print("Test-App: User registered with \(response)")
        }
    },
);

```

### Surveys Method

The below code snippet can be used to invoke the Surveys method. 
> Note: Only call this method if the Member is already registered. If the Member is not registered, first invoke the Registration method to register the Member and then call this method.

```plaintext
IntegratedPanel.getSurveyView();
```

### SurveyFlow Method

The below code snippet can be used to invoke the SurveyFlow method. 
> Note: Call this method when the SDK needs to handle the transition between the Registration and the Survey method.

```plaintext
IntegratedPanel.getSurveyFlow(
    onSaved: (response) {
        if(!response.isEmpty) {
            print("Test-App: User registered with \(response)")
        }
    },
);

```
