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


1. Download the SDK package for React Native
2. Run ```npm install``` command to install the necessary packages
3. Setup cultures in cultures.json file in src/assets folder.
    - Optional: Place your company logo in png format in src/assets folder. Note: company logo should have the name company_logo.png
4. Create a tarball using ```npm pack``` inside the SDK project terminal
5. Add the following packages and tarball file (.tgz) reference to the ```package.json``` file of the app
```
“dependencies”:{
"react-native-rn-ip-sdk":"<Path to the package>",
"react-native-native-log":"^0.1.3",
"react-native-svg-transformer":"^1.5.0",
"react-native-webview":"^11.23.1",
"@react-native-async-storage/async-storage":"^2.1.0",
"react-native-svg":"^15.11.2",
}
```
6. Add the support of svg and ttf in the metro.config file of the application
7. Run ```npm install``` to install the necessary packages


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

const debugMode = true;
const mockMode = true;
const prodMode = true;
const customization = new customize(
    '<Primary Color Hex Code>',
    '<Secondary Color Hex Code>',
    50,
    20,
    1,
    '<Font Family>',
    mockMode,
    prodMode,
    debugMode,
    '<Logo Name>'
);

IPSDK.initialize(
    partnerAuthKey,
    memberDetails,
    customization,
    );
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
