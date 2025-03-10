---
title: SwiftUI
has_children: false
nav_order: 4
parent: SDK Offering
---

# SwiftUI
{: .no_toc }

Below are instructions on using the SDK SwiftUI package.

* TOC
{:toc}

## Step 1: Link the SDK Framework

1.	Build the SDK for obtaining the .framework folder in the Build directory
2.	Drag and drop the downloaded framework into your XCode project
3.	Make sure the framework is embedded in your General > Frameworks, Libraries, and Embedded Content section

## Step 2: Initialize the SDK

```plaintext
import SDK

@main
struct MyApp: App {
    init() {
        let partnerAuthKey = "<Your Partner Auth Key>"
        let memberDetails: MemberDetails = MemberDetails(
            PartnerGuid: "<Culture GUID>",
            MemberCode: "< Member Unique Code>",
            PostalCode: "<Member Zip Code>",
            BirthDate: "< MM/DD/YYYY >",
            IsActive: true,
            IsTest: false,
            RegistrationAnswers: [
                RegistrationAnswer(
                    QuestionId: 1,
                    Answers: [
                        AnswerId(
                            AnswerId: 3,
                            AnswersValue: "< Answer text >"
                        )
                    ]
                )
            ]
        )
        
        let customization: Customize = Customize(
            PrimaryColor: "#000000",
            SecondaryColor: "#FFFFFF",
            FontFamily: "Arial",
            MaxLOI: 20,
            SurveyViewType: 1,
            DarkMode: true,
            LogoName: nil,
            LogoEnable: false
        )
        
        let debugMode: Bool = true
        let mockMode: Bool = true
        
        SDK.initialize(
            PartnerAuthKey: partnerAuthKey,
            MemberDetails: memberDetails,
            Customization: customization,
            DebugMode: debugMode,
            MockMode: mockMode
        )
    }
    
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```

## Step 3: Use SDK Methods

### Registration Method

The below code snippet can be used to invoke the Registration method.
> Note: Only call this method if the Member is not registered or there is a need to update the details of the member. If already registered and there is no need to update the member details directly invoke the Surveys method.

```plaintext
// Registration View
SDK.Registration { response in
    if(!response.isEmpty) {
        print("Test-App: User registered with \(response)")
    }
}
```

### Surveys Method

The below code snippet can be used to invoke the Surveys method. 
> Note: Only call this method if the Member is already registered. If the Member is not registered, first invoke the Registration method to register the Member and then call this method.

```plaintext
// Survey Wall View
SDK.Surveys()
```

### SurveyFlow Method

The below code snippet can be used to invoke the SurveyFlow method. 
> Note: Call this method when the SDK needs to handle the transition between the Registration and the Survey method.

```plaintext
// Surveys Flow View Handled By SDK
SDK.SurveyFlow { result in
    if(!response.isEmpty) {
        print("Test-App: User registered with \(response)")
    }
}
```
