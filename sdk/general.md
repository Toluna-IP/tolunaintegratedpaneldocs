---
title: General
has_children: false
nav_order: 1
parent: SDK Offering
---

# General
{: .no_toc }

Below you will find information on the SDK stack that is applicable to its general use.

* TOC
{:toc}

## Supported Platforms

- [SwiftUI](/sdk/swiftui.html) (iOS) - Version 14.2 and above
- [Fluter](/sdk/flutter.html) - Version 2.10.0 and above
- [React Native](sdk\reactnative.md) - Version 0.64 and above
- [Kotlin](/sdk/reactnative.html) (Android) - Version 6 and above

## Prerequisites

IDE needed for each platform:
- Xcode: SwiftUI
- Android Studio: Kotlin, Flutter, or React Native
- Visual Studio Code: Flutter or React Native

A link to the appropriate SDK package for your target platform will be provided by your Toluna representative.

## Culture Configuration

Toluna operates on a **culture** basis, where culture is defined as a country-language pairing. A list of available cultures can be found [here.](/general/common.html#culture-driven)

Before launching in a culture, the Partner will need to acquire a cultureGuid from Toluna. To make a culture available to their members, a Partner must add it to a file named culture.json. This file must, in turn, be added to the assests folder of the SDK package.

### cultures.json Objects

| Object Name | Type | Description | Required? |
| :--- | :--- | :--- | :---: |
| cultureId | ```int``` | Toluna's unqiue identifier for a culture. These IDs can be pulled and identified from the [Culture Route](/mapping/referencedataapi/cultures.html) of the Reference Data API | Yes|
| cultureGuid | ```guid``` | A Toluna-provided Guid used to identify the panel when connecting to Toluna's APIs | Yes|
| name | ```string``` | A descriptor for the culture which will be shown to the member in the event the partner does not the cultureGuid beforehand in the member flow. The partner can choose how to present the culture to the member (e.g. English-United States, USA (English), etc.) | Yes |
| isDefault | ```bool``` | Defines if the culture should be used as the default for members. Only one culture can have this value as "true". | Yes |

### Example cultures.json File

```plaintext
[
  {
    "cultureId": 5,
    "cultureGuid": "AC7286DF-XXXX-XXXX-XXXX-F1EB8509AB10",
    "name": "United Kingdom (English)",
    "isDefault": false
  },
  {
    "cultureId": 1,
    "cultureGuid": "5EEBF4DD-XXXX-XXXX-XXXX-928B66FC043F",
    "name": "United States (English)",
    "isDefault": true
  }
]
```


## Optional Assets

### Logo

The Partner can add a custom logo to be shown on the Member's survey/offer wall. To do so, add a Logo.png file to the assets folder.

### Fonts

The Partner can add custom fonts to be used when displaying information to the Member on their survey/offer wall. To do so, add the font file(s) to the assets folder.


## Incentivizing Members

Partner's utilizing the SDK can specify how much a Member can expect to be incentivized based on the metrics (Length of survey, incidence rate, etc.) of a survey. They may also specify the currency used when displaying the incentive to the member or opt to display the reward in points. To set up the incentives and currency, please speak with your Toluna Representative.

In any case, Member incentives will be managed by the Partner. Toluna recommends Partners develop an API endpoint to which they can receive notice when a Member completes a Survey. This feature is known as a Member Status Notification, the details of which can be found [here](/notifications/memberstatus.html#completions).

> Note: Partners may also subscribed to [Termination Member Status Notifications](/notifications/memberstatus.html#terminates) if they want to be notified of non-completes as well.