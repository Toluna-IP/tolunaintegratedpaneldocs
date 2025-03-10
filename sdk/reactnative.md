---
title: React Native
has_children: false
nav_order: 7
parent: SDK Offering
---

# React Native
{: .no_toc }

Below are instructions on using the SDK React Native package.

* TOC
{:toc}

## Step 1: Download and Link the SDK


1.	Download the SDK package for React Native
2.	Create a package of the SDK using ```npm pack``` inside the SDK project terminal
3.	Add the package (.tgz) reference to the package.json file of the app
- ``` “dependencies”:{ "react-native-rn-ip-sdk":"<Path to the package>"}```
4. Install the package in the app project
- ```npm install 'react-native-rn-ip-sdk'```

## Step 2: Initialize the SDK

```plaintext
import { IPSDK } from 'react-native-rn-ip-sdk';

const partnerAuthKey = '<Your Partner Auth Key>';
const memberDetails = new memberDetails(
    "<Culture GUID>",
    "< member unique key >",
    "12345",
    "1990-01-01",
    true,
    false,
    [
        new registrationAnswers(
            101,
            [
                new answerId(1, "Yes")
            ]
        )
    ]
);

const customization = new customize(
    '<Primary Color Hex Code>',
    '<Secondary Color Hex Code>',
    50,
    20,
    1,
    '<Font Family>',
    true,
    true,
    '<Logo Name>'
);

const debugMode = true;
const mockMode = true;

IPSDK.initialize(
    partnerAuthKey,
    memberDetails,
    customization,
    debugMode,
    mockMode
);
```

## Step 3: Use SDK Methods


### Registration Method

The below code snippet can be used to invoke the Registration method.
> Note: Only call this method if the Member is not registered or there is a need to update the details of the member. If already registered and there is no need to update the member details directly invoke the Surveys method.

```plaintext
const RegistrationView = () => {
    var [registeredCulture, setRegisteredCulture] = useState('');
    
    useEffect(() => {
        console.log("Test-App: User registered with " + registeredCulture);
    }, [registeredCulture]);
    
    return (
        <View>
            {IPSDK.Registration(setRegisteredCulture)}
        </View>
    );
};

export default RegistrationView;

```

### Surveys Method

The below code snippet can be used to invoke the Surveys method. 
> Note: Only call this method if the Member is already registered. If the Member is not registered, first invoke the Registration method to register the Member and then call this method.

```plaintext
const SurveyWallView = () => {
    
    return (
        <View>
            {IPSDK.Surveys()}
        </View>
    );
};

export default SurveyWallView;

```

### SurveyFlow Method

The below code snippet can be used to invoke the SurveyFlow method. 
> Note: Call this method when the SDK needs to handle the transition between the Registration and the Survey method.

```plaintext
const SurveyFlowView = () => {
    var [registeredCulture, setRegisteredCulture] = useState('');
    
    useEffect(() => {
        console.log("Test-App: User registered with " + registeredCulture);
    }, [registeredCulture]);
    
    return (
        <View>
            {IPSDK.SurveyFlow(setRegisteredCulture)}
        </View>
    );
};

export default SurveyFlowView;

```
