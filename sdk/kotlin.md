---
title: Kotlin (Android)
has_children: false
nav_order: 5
parent: SDK Offering
---

# Kotlin (Android)
{: .no_toc }

Below are instructions on using the SDK Kotlin package.

* TOC
{:toc}

## Step 1: Add SDK to Your Project

1.	Download the SDK for the Android Kotlin
2.	Add the dependency to your build.gradle
- ```implementation "com.example:ipsdk:1.0.0"```
3. Sync your project in android studio to get all the dependencies.

## Step 2: Initialize the SDK

```
import com.example.ipsdk.IntegratedPanel

class MyApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        
        val partnerAuthKey = "<Your Partner Auth Key>"
        val member = Member(
            partnerGUID = "<Culture GUID>",
            memberCode = "<Member Unique Code>",
            isActive = true,
            isTest = true
        )
        
        val customization = Customization(
            mainColor = "#000000",
            secondaryColor = "#ffffff",
            maxLOI = 50,
            numberOfSurveys = 20,
            surveyViewType = 1,
            fontFamily = "Roboto-Regular.ttf",
            isDarkMode = _darkMode.value ?: false,
            imageAssetPath = "<Logo Image Path>",
            LogoEnable = true
        )
        
        IntegratedPanel.initialize(
            context = context,
            partnerAuthKey = partnerAuthKey,
            member = member,
            customization = customization,
            cultureAssetPath = "<Culture File path>",
            debugMode = false,
            mockMode = false,
            prodMode = true,
        )
    }
}
```

## Step 3: Use SDK Methods

### Registration Method

The below code snippet can be used to invoke the Registration method.
> Note: Only call this method if the Member is not registered or there is a need to update the details of the member. If already registered and there is no need to update the member details directly invoke the Surveys method.

```plaintext
<com.example.ipsdk.views.registration.RegistrationView
    android:id="@+id/register_view"
    android:layout_width="match_parent"    android:layout_height="match_parent"/>

register.setOnRegisterListener {
    if(it.isNotEmpty()) {
        Log.d("we have successfully received the details ${it}")
    }
}

```

### Surveys Method

The below code snippet can be used to invoke the Surveys method. 
> Note: Only call this method if the Member is already registered. If the Member is not registered, first invoke the Registration method to register the Member and then call this method.

```plaintext
<com.example.ipsdk.views.survey.SurveyView
    android:id="@+id/survey_view"
    android:layout_width="match_parent"    android:layout_height="match_parent"/>
```

### SurveyFlow Method

The below code snippet can be used to invoke the SurveyFlow method. 
> Note: Call this method when the SDK needs to handle the transition between the Registration and the Survey method.

```plaintext
<com.example.ipsdk.views.survey.SurveyFlow
    android:id="@+id/survey_flow"
    android:layout_width="match_parent"         android:layout_height="match_parent"/>     

surveyFlow.setOnRegisterListener {
    if(it.isNotEmpty()) {
        Log.d("we have successfully received the details ${it}")
    }
}

```
