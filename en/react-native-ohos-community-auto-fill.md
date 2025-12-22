> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-ohos/auto-fill</code> </h1>
</p>
<p align="center">
    <img src="https://img.shields.io/badge/platforms-%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    <a href="https://github.com/react-native-oh-library/auto-fill/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


Based on the HarmonyOS [autoFillManager](https://developer.huawei.com/consumer/en/doc/harmonyos-references-V5/js-apis-app-ability-autofillmanager-V5) module, auto-fill provides the feature of saving the form input data to the recent forms for automatic filling. This feature is supported only in OpenHarmony OS.

<video controls src="https://github.com/user-attachments/assets/19be83fb-2afb-4a31-9e7f-cba3848a5892" title="auto-fill-demo" width="180"></video>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/auto-fill)

## Prerequisites

1. Apply for the SmartFill service. Currently, SmartFill is in the beta phase. You can send an email to apply for access. For details about the email template, see [Application Email Template](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/scenario-fusion-introduction-to-smart-fill-V5#section107231967593).
2. Enable SmartFill by choosing **Settings** > **Privacy & security** > **SmartFill**.
3. Connect the device to the Internet.
4. Log in to a HUAWEI ID on the device.
5. Pass the [textContentType](https://reactnative.cn/docs/textinput#textcontenttype) attribute to the **TextInput** component on the service side.

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <=1.0.1@deprecated | [@react-native-ohos-community/auto-fill Releases(deprecated)](https://github.com/react-native-oh-library/auto-fill/releases) | 0.72       |
| 1.0.2             | [@react-native-ohos/auto-fill Releases](https://gitcode.com/openharmony-sig/rntpc_auto-fill/releases)   | 0.72       |
| 1.1.0             | [@react-native-ohos/auto-fill Releases](https://gitcode.com/openharmony-sig/rntpc_auto-fill/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instructions:

#### npm

```bash
npm install @react-native-ohos/auto-fill
```

#### **yarn**

```bash
yarn add @react-native-ohos/auto-fill
```

## Description

### How to Use

```tsx
import React, { useState } from 'react';
import { View, TextInput, Button, StyleSheet } from 'react-native';
import AutoFill from '@react-native-ohos/auto-fill';

const MyFormComponent = () => {
  const [fullName, setFullName] = useState('');
  const [phoneNumber, setPhoneNumber] = useState('');

  const handleSubmit = () => {
    AutoFill.autoSave(
      () => {
        console.log('AutoFillTurboModule success in js is been called');
      },
      () => {
        console.log('AutoFillTurboModule failed in js is been called');
      }
    );
  };

  return (
    <View style={styles.container}>
      <TextInput
        style={styles.input}
        placeholder="Full Name"
        value={fullName}
        onChangeText={setFullName}
        autoCapitalize="words"
        textContentType="name"
      />
      <TextInput
        style={styles.input}
        placeholder="Phone Number"
        value={phoneNumber}
        onChangeText={setPhoneNumber}
        keyboardType="phone-pad"
        textContentType="telephoneNumber"
      />

      <Button title="Submit" onPress={handleSubmit} />
    </View>
  );
};

export default MyFormComponent;
```

When **AutoFill.autoSave** is called for the first time, the saving sheet that asks the user whether to save the input to recent forms is displayed.

- If the user touches the **Save** button, SmartFill is enabled and the input data is saved to the recent forms.
- If the user touches the **Ignore** button, the same device will not ask the user again within 24 hours. After the user touches the **Ignore** button for five times, the user will be prompted to choose whether they don't want to be asked again.

### When to Use

- Contact information filling: applicable to forms related to contact data such as ticket purchase information and delivery information.
- Account and password filling: applicable to forms related to the login page.
- Automatic form filling during page redirection.
- For details about the sample code, see [ContactsComponent.tsx](https://gitcode.com/openharmony-sig/rntpc_auto-fill/blob/br_rnoh0.72/tester/App.tsx).

> For details about the password saving and filling rules, see [Password Autofill Service](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/passwordvault-V5).

### The Mapping of ContentType

The following lists the mapping between [textContentType](https://reactnative.cn/docs/textinput#textcontenttype) received by the **TextInput** component in React Native and [ContentType](https://developer.huawei.com/consumer/en/doc/harmonyos-references-V5/ts-basic-components-textinput-V5#contenttype12) in HarmonyOS.

```js
// The key is the value of textContentType in React Native,
// The value is the value of ContentType in HarmonyOS.

//Instructions:
// 1. The textContentType configuration item 'name' and ('familyName', 'givenName') cannot be used in the same form at the same time (they can be used together in the passport information scenario).
// 2. 'nickName', 'organization', and 'taxId' cannot be saved, but they can be autofilled, provided that the logged-in Huawei account is real-name verified and has set a nickname, company name, and company tax ID.
// 3. The use of 'licensePlate' requires the logged-in Huawei account to be real-name verified, and a record of the Huawei account owner's data (name and email, with the name being the real name in the real-name verification) must be added to the autofill history form first.
{
    "countryName": COUNTRY_ADDRESS, // Country
    "fullStreetAddress": FULL_STREET_ADDRESS, // Detailed address
    "telephoneNumber": PHONE_NUMBER, // Phone number
    "username": USER_NAME, // Username
    "password": PASSWORD, // Password
    "emailAddress": EMAIL_ADDRESS, //  Email address
    "name": PERSON_FULL_NAME, // Full name
    "idCardNumber":ID_CARD_NUMBER,//ID card number
    "familyName":PERSON_LAST_NAME,//Last name
    "givenName":PERSON_FIRST_NAME,//First name
    "passportNumber":PASSPORT_NUMBER,//passportNumber
    "validity":VALIDITY,//validity
    "issueAt":ISSUE_AT,//issueAt
    "nickName":NICKNAME,//nickName
    "formatAddress":FORMAT_ADDRESS,//format address
    "detailInfoWithoutStreet":DETAIL_INFO_WITHOUT_STREET,//detail info without street
    "licensePlate":LICENSE_PLATE,//license plate
    "organization":ORGANIZATION,//organization
    "taxId":TAX_ID,//tax id
    
}
```

### Link

|                                      | Is supported autolink | Supported RN Ve
|--------------------------------------|------------------|------------|
| ~1.1.0                               |  No              |  0.77     |
| ~1.0.2                               |  Yes             |  0.72     |
| <=1.0.1@deprecated                   |  No              |  0.72     |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

#### 1. Adding the **overrides** Field to the **oh-package.json5** File in the Root Directory of the Project

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "./react_native_openharmony"
  }
}
```

#### 2. Introducing Native Code

Currently, two methods are available:

(1) Use the HAR file (this method will be deprecated once DevEco Studio supports the relevant functionality; currently, this is the preferred method).

(2) Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the **harmony** directory in the installation path of the third-party library.

Open **entry/oh-package.json5** and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/auto-fill": "file:../../node_modules/@react-native-ohos/auto-fill/harmony/auto_fill.har"
  }
```

Click the **sync** button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

For details, see [Direct Linking of Source Code](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/link-source-code.md).

#### 3. Configuring CMakeLists and Introducing AutoFillPackage

> If you are using version <=1.0.1, please skip this chapter.

Open **entry/src/main/cpp/CMakeLists.txt** and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
...
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/auto-fill/src/main/cpp" ./auto-fill)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC auto_fill)
# RNOH_END: manual_package_linking_2
```

Open **entry/src/main/cpp/PackageProvider.cpp** and add the following code:

```diff
#include "RNOH/PackageProvider.h"
+ #include "AutoFillPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(
    Package::Context ctx) {
  return {
+       std::make_shared<AutoFillPackage>(ctx),
  };
}
```

#### 4. Introducing AutoFillPackage to ArkTs

Open **entry/src/main/ets/RNPackagesFactory.ts** and add the following code:

```diff
  ...
+ import { AutoFillPackage } from '@react-native-ohos/auto-fill/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new AutoFillPackage(ctx),
  ];
}
```
</details>

## Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.



## Constraints

### Compatibility

To use this library, you need to use the correct React Native and RNOH versions. In addition, use the matching DevEco Studio and the ROM on your phone.

Verified successfully in the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;


## API Description

auto-fill exposes only the **autoSave** API, which is used to save the current form information.

| API                              | Description                         |                    Parameter                     | Return Value |
| :------------------------------- | ----------------------------------- | :----------------------------------------------: | :----------: |
| autoSave(onSuccess?, onFailure?) | Saves the current form information. | (onSuccess?: () => void, onFailure?: () => void) |     void     |

> The **autoSave** API can be invoked only once within 2 seconds on the native side. If the API is invoked multiple times, the **onFailure** callback is triggered and the message "autoSave called too frequently, please wait for 2 seconds" is displayed.


## License

This project is licensed under [Apache License 2.0](https://github.com/react-native-oh-library/auto-fill/blob/sig/LICENSE).