> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>jverification-react-native</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jpush/jverification-react-native">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/jverification-react-native/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/jpush/jverification-react-native)

## Installation and Usage

Find the matching version information in the release address of a third-party library：

| Version | Post Information                                                     | Support RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.4.7     | [@react-native-ohos/jverification-react-native Releases](https://github.com/react-native-oh-library/jverification-react-native/releases) | 0.72/0.77       |


Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/jverification-react-native
```


#### **yarn**

```bash
yarn add @react-native-ohos/jverification-react-native
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:
> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import {
  View,
  StyleSheet,
  Button,
  Alert,
  ScrollView,
} from "react-native";
import JVerification from "jverification-react-native";

const customConfigParams = {
  showWindow: false,
  dialogWidth: 275, 
  dialogHeight: 400,
  topSafeAreaHeight: 38,
  BottomSafeAreaHeight: 38,
  /**
   * Back button
   */
  returnBtnImgPath: "back",
  returnBtnHidden: false,
  returnBtnWidth: 100,
  returnBtnHeight: 80,
  returnBtnOffsetX: 10,
  returnBtnOffsetY: 43,
  /**
   * Phone number style
   */
  numberTextBold: true,
  numberSize: 30,
  numberColor: "#B22222",
  numberX: 0,
  numberY: 30,
  numberW: "100%",
  numberH: 100,
  /**
   * login
   */
  loginBtnText: "One-Click Login",
  loginBtnTextSize: 20,
  loginBtnTextColor: "rgb(0,0,0)",
  loginBtnColor: "rgb(197,34,34)",
  loginBtnImage: "loginBtn",
  loginBtnX: -1,
  loginBtnY: 20,
  loginBtnW: "60%",
  loginBtnH: 56,
  loginBtnTextBold: true,
  backgroundImage: "background",
  /**
   * Privacy Agreement Page
   */
  privacyWebNavTitleColor: "rgb(29,211,29)",
  privacyWebNavColor: "rgb(202,193,16)",
  privacyWebNavTitleSize: 20,
  privacyWebNavReturnImage: "back",
  privacyNavTitleTextBold: true,
  /**
   * logo
   */
  logoHidden: false,
  logoImage: "logo",
  logoX: -1,
  logoY: 175,
  logoW: 100,
  logoH: 100,
  /**
   * slogan
   */
  sloganTextSize: 20,
  sloganTextColor: "rgb(216,213,30)",
  sloganX: -1,
  sloganY: 70,
  sloganTextBold: true,
  /**
   * Privacy Agreement Section
   */
  privacyOne: ["Privacy Policy 1", "https://www.csdn.net"],
  privacyTwo: ["Privacy Policy 2", "https://www.baidu.com"],
  privacyColor: ["#bed442ff", "#d61e9fff"],
  privacyText: ["Log in to agree", ", and log in using the local phone number"],
  privacyTextSize: 15,
  privacyTextGravityMode: "center",
  privacyCheckEnable: false,
  privacyCheckedImage: "check",
  privacyUncheckedImage: "unCheck",
  privacyCheckboxSize: 20,
  privacyX: 5,
  privacyY: 5,
  privacyBookSymbolEnable: true,
  privacyUnderlineText: true,
  privacyTextBold: true,
  enableHintToastText: "Please check the privacy agreement",
  privacyCheckboxInCenter: true,
  privacyMargin: { left: 5, right: 5, bottom: 10 },
  /**
   * CM
   */
  loginBtnBorderRadius: 45,
  checkBoxShape: 0,
  checkTipText: "No prompt text selected",
  setClauseNavMarginTop: 10,
};

const customConfigParamsCM = {
  showWindow: false,
  /**
   * Privacy Agreement Section
   */
  privacyOne: ["Privacy Policy 1", "https://www.csdn.net"],
  privacyTwo: ["Privacy Policy 2", "https://www.baidu.com"],
  privacyColor: ["rgb(30,73,216)", "rgb(39,39,9)"],
  privacyText: ["Log in to agree", ", and log in using the local phone number"],
  privacyTextSize: 16,
  privacyBookSymbolEnable: false,
  privacyX: 40,
  privacyY: 0,
  privacyTextBold: true,
  privacyTextGravityMode: "center",
  privacyCheckEnable: false,
  checkBoxShape: 0,
  checkTipText: "Mobile unchecked prompt text",
  privacyCheckboxSize: 20,
  privacyCheckedImage: "check",
  privacyUncheckedImage: "unCheck",
  checkBoxX: 20,
  checkBoxY: 15,
  clauseNavMarinTop: 30,
  /**
   * Privacy Agreement Page
   */
  privacyWebNavTitleColor: "rgb(29,211,29)",
  privacyWebNavColor: "rgb(202,193,16)",
  privacyWebNavTitleSize: 20,
  /**
   * Navigation bar, status bar
   */
  statusBarMode: "light",
  navColor: "rgb(63,196,36)",
  navTitleColor: "rgb(211,208,29)",
  /**
   * login
   */
  loginBtnText: "One-Click Login",
  loginBtnTextSize: 20,
  loginBtnTextColor: "rgb(0,0,0)",
  loginBtnColor: "rgb(197,34,34)",
  loginBtnImage: "loginBtn",
  loginBtnDisabledImage: "background",
  loginBtnX: -1,
  loginBtnY: 335,
  loginBtnW: "60%",
  loginBtnH: 56,
  loginBtnDisabledTextColor: "rgb(0,0,0)",
  loginBtnDisabledColor: "rgb(212,24,39)",
  loginBtnBorderColor: "rgb(197,32,212)",
  loginBtnDisabledBorderColor: "rgb(0,0,0)",
  loginBtnBorderWidth: 10,
  loginBtnDisabledBorderWidth: 2,
  loginBtnBorderRadius: 45,
  /**
   * Phone number style
   */
  numberTextBold: true,
  numberSize: 30,
  numberColor: "rgb(158,19,19)",
  numberX: 160,
  numberY: 250,
  numberW: "100%",
  numberH: 100,
};

let customViewParams = {};

class JverificationTest extends React.Component {
  state = { code: "", msg: "", operator: "", enable: true };
  render() {
    const { code, msg, operator, enable } = this.state;

    return (
      <ScrollView>
         <View style={styles.container}>
        <View style={styles.space}>
          <Button
            title="setLoggerEnable (true)"
            onPress={() => {
              JVerification.setLoggerEnable(false);
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="init"
            onPress={() => {
              JVerification.init(
                { appkey: "373cb7214054aae64525fdf4" },
                (result) => {
                  Alert.alert("SDK initialization", JSON.stringify(result));
                }
              );
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="isInitSuccess"
            onPress={() => {
              JVerification.isInitSuccess((result) => {
                Alert.alert("Is initialization successful", JSON.stringify(result));
              });
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="checkLoginEnable"
            onPress={() => {
              // SDK determines whether the network environment supports it
              JVerification.checkLoginEnable((result) => {
                Alert.alert("Does the network environment support it", JSON.stringify(result.enable));
              });
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="getToken"
            onPress={() => {
              JVerification.getToken(5000, (result) => {
                Alert.alert("Obtain number authentication token", JSON.stringify(result));
              });
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="preLogin"
            onPress={() => {
              JVerification.preLogin(5000, (result) => {
                Alert.alert("Get pre fetch token", JSON.stringify(result));
              });
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="clearPreLoginCache"
            onPress={() => {
              JVerification.clearPreLoginCache();
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="addLoginCustomConfig CT CU"
            onPress={() => {
              JVerification.addLoginCustomConfig(
                customConfigParams,
                customViewParams
              );
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="addLoginCustomConfig CM"
            onPress={() => {
              JVerification.addLoginCustomConfig(
                customConfigParamsCM,
                customViewParams
              );
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="addLoginEventListener"
            onPress={() => {
              JVerification.addLoginEventListener((result) => {
                Alert.alert("addLoginEventListener: ", JSON.stringify(result));
              });
            }}
          />
        </View>
        
        <View style={styles.space}>
          <Button
            title="addUncheckBoxEventListener"
            onPress={() => {
              JVerification.addUncheckBoxEventListener((result) => {
                Alert.alert(
                  "addUncheckBoxEventListener: ",
                  JSON.stringify(result)
                );
              });
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="login"
            onPress={() => {
              JVerification.login(true);
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="dismissLoginPage"
            onPress={() => {
              JVerification.dismissLoginPage();
            }}
          />
        </View>
        
        </View>
      </ScrollView>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    flexDirection: "column",
    alignItems: "center",
    padding: 10,
    marginTop: 38
  },
  label: {
    fontSize: 30,
  },
  viewBox: {
    padding: 5,
    backgroundColor: "white",
    width: "100%",
    marginBottom: 10,
    matginTop: 10,
    justifyContent: "flex-start",
  },
  space: {
    flex: 1,
marginTop: 10
  }
});

export default JverificationTest;

```

## Link

This step is a guide for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.Add the `products` field to the `build-profile.json5` file in the project root directory

```json
{
  ...
  products: [
      {
        ...
        buildOption: {
          strictMode: {
            useNormalizedOHMUrl: true,
          },
        },
      },
  ]
}
```

### 3.Introducing Native Code

Currently, two methods are available:

1. Use the HAR file (this method will be deprecated once the IDE supports the relevant functionality and is preferred currently).
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:
```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/jverification-react-native": "file:../../node_modules/@react-native-ohos/jverification-react-native/harmony/jverification_react_native.har"
  }
```
Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 4.Configuring CMakeLists and Introducing JVerificationPackage.h

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
...

project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/jverification-react-native/src/main/cpp" ./jverification)
# RNOH_BEGIN: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_jVerification_react_native)
# RNOH_BEGIN: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp`，add：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "JVerificationPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<JVerificationPackage>(ctx)
    };
}
```

### 5.Introducing JVerificationPackage to ArkTS

Open `entry/src/main/ets/RNPackagesFactory.ts`，add：

```diff
  ...
+   import {JVerificationPackage} from '@react-native-ohos/jverification-react-native/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new JVerificationPackage(ctx)
  ];
}
```

### 6.Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

The content of this document has been validated based on the following version:

1. RNOH：0.72.90; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.112;
2. RNOH：0.72.90; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 6.0.0.858; ROM：5.0.0.102;
3. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.112;
4. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 6.0.0.858; ROM：5.0.0.102;

### Permission Requirements

- This library involves the Bluetooth system control function. Therefore, you need to configure the corresponding permission in the **module.json5** file in the **entry/src/main** directory when using the corresponding APIs. Some permissions need to be requested from users in a pop-up window. For details about the permission configuration, see [Application Access Control](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/Readme-CN.md#/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/app-permission-mgmt-overview.md)。

- Some functions and APIs of this library require the **normal** permission **ohos.permission.INTERNET**.
## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| setLoggerEnable(enable: boolean): void  | Set debug mode        | function | no | iOS/Android      | yes |
| init(params, callback)  | Initialize SDK        | function | no | iOS/Android      | yes |
| isInitSuccess(callback) | Check if initialization is successful        | function | no | iOS/Android      | yes |
| checkLoginEnable(callback)  | Check if the current network environment can initiate authentication       | function | no | iOS/Android      | yes |
| getToken(time, callback) | Get token       | function | no | iOS/Android      | yes |
| preLogin(time, callback)  | Verify if the current carrier network can perform one-click login operation. This method will cache the number retrieval information      | function | no | iOS/Android      | yes |
| clearPreLoginCache()  | Clear pre-login cache      | function | no | iOS/Android      | yes |
| login(enable)  | Launch one-click login authorization page      | function | no | iOS/Android      | yes |
| addLoginEventListener(callback)  | Add one-click login event listener   | function | no | iOS/Android      | yes |
| addUncheckBoxEventListener(callback)  | Add checkbox listener event      | function | no | iOS/Android      | yes |
| dismissLoginPage()  | Hide login authorization page      | function | no | iOS/Android      | yes |
| removeListener(callback)  | Remove listener event      | function | no | iOS/Android      | no |
| getVerifyCode(params,callback)  | Get verification code      | function | no | iOS/Android      | no |
| setCodeTime(time)  | Get the interval between two verification codes     | function | no | iOS/Android      | no |
| addCustomViewsClickCallback  | Add custom view callback      | function | no | iOS/Android      | no |
| addLoginCustomConfig(customConfigParams, customViewParams)  | Custom configuration parameters      | function | no | iOS/Android      | yes |

### init params

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| appkey  | JPush application unique identifier      | string | no | iOS/Android      | yes |

### init callback

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| code  | Status code      | number | no | iOS/Android      | yes |  
| content  | Initialization result information      | string | no | iOS/Android      | yes |  

### getToken time parameter

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| time  | Set initialization timeout time in milliseconds. Valid range is (0,10000], default value is 5000      | number | no | iOS/Android      | yes |

### getToken callback parameter

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| code  | Status code      | number | no | iOS/Android      | yes |  
| content  | Get token result information      | string | no | iOS/Android      | yes |  
| operator  | Carrier information      | string | no | iOS/Android      | yes |  

### preLogin time parameter

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| time  | Set timeout time in milliseconds. Valid range is (0,30000], default value is 10000     | number | no | iOS/Android      | yes |

### preLogin callback parameter

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| code  | Status code      | number | no | iOS/Android      | yes |  
| content  | Result information indicating whether one-click login operation can be performed      | string | no | iOS/Android      | yes |  

### login enable parameter

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| enable  |  Whether to automatically close the authorization page      | number | no | iOS/Android      | yes |  

### addLoginEventListener callback parameter

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| code  |  Status code      | number | no | iOS/Android      | yes |  
| msg  |  One-click login event listener information      | string | no | iOS/Android      | yes |  
| operator  |  Carrier information      | string | no | iOS/Android      | yes |  

### customConfigParams

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| backgroundImage  | Background image (China Unicom, China Telecom)        | string | no | iOS/Android      | yes |
| statusBarHidden  | Whether to hide the status bar        | boolean | no | iOS/Android      | no |
| statusBarMode  | Status bar mode (China Mobile only)       | function | no | iOS/Android      | yes |
| navHidden | Whether to hide the navigation bar       | boolean | no | iOS/Android      | no |
| navColor  | Navigation bar color        | number | no | iOS/Android      | no |
| navTitle  | Navigation bar title        | string | no | iOS/Android      | no |
|navTitleSize  | Navigation bar title font size        | number | no | iOS/Android      | no |
| navTitleColor  | Navigation bar title text color (China Mobile only)        | number | no | iOS/Android      | no |
| navReturnHidden  | Whether to hide the navigation bar return button        | boolean | no | iOS/Android      | no |
| navReturnImage  | Navigation bar left return button icon        | string | no | iOS/Android      | no |
| navReturnX  | Navigation bar left return button icon offset from the top of the screen        | number | no | iOS/Android      | no |
| navReturnY  | Navigation bar left return button icon offset from the left side of the screen        | number | no | iOS/Android      | no |
| navReturnW  | Navigation bar left return button icon width        | number | no | iOS/Android      | no |
| navReturnH  | Navigation bar left return button icon height        | number | no | iOS/Android      | no |
| logoHidden  | Whether to hide logo (China Unicom, China Telecom)      | boolean | no | iOS/Android      | yes |
| logoImage  | Logo image (China Unicom, China Telecom)        | string | no | iOS/Android      | yes |
| logoX  | Logo x-axis offset (China Unicom, China Telecom)       | number | no | iOS/Android      | yes |
| logoY  | Logo y-axis offset (China Unicom, China Telecom)       | number | no | iOS/Android      | yes |
| logoW  | Logo width (China Unicom, China Telecom)       | number | no | iOS/Android      | yes |
| logoH  | Logo height (China Unicom, China Telecom)       | number | no | iOS/Android      | yes |
| numberSize  | Phone number font size (China Unicom, China Telecom, China Mobile)        | number | no | iOS/Android      | yes |
| numberColor  | Phone number color (China Unicom, China Telecom, China Mobile)        | number | no | iOS/Android      | yes |
| numberTextBold  | Whether the phone number is bold (China Unicom, China Telecom, China Mobile)        | boolean | no | -      | yes |
| numberX  | Phone number x-axis offset (China Unicom, China Telecom, China Mobile)        | number | no | iOS/Android      | yes |
| numberY  | Phone number y-axis offset (China Unicom, China Telecom, China Mobile)        | number | no | iOS/Android      | yes |
| numberW  | Phone number text width (China Unicom, China Telecom, China Mobile)        | number | no | iOS/Android      | yes |
| numberH  | Phone number text height (China Unicom, China Telecom, China Mobile)        | number | no | iOS/Android      | yes |
| sloganHidden  | Whether to hide slogan        | boolean | no | iOS/Android      | no |
| sloganTextSize  | Slogan font size (China Unicom, China Telecom)        | number | no | iOS/Android      | yes |
| sloganTextColor  | Slogan color (China Unicom, China Telecom)        | number | no | iOS/Android      | yes |
| sloganX  | Slogan x-axis offset (China Unicom, China Telecom)        | number | no | iOS/Android      | yes |
| sloganY  | Slogan y-axis offset (China Unicom, China Telecom)        | number | no | iOS/Android      | yes |
| sloganW  | Slogan width        | number | no | iOS/Android      | no |
| sloganH  | Slogan height        | number | no | iOS/Android      | no |
| sloganTextBold | Whether slogan is bold (China Unicom, China Telecom)        | boolean | no | -      | yes |
| loginBtnText | Authorization login button text content (China Unicom, China Telecom, China Mobile)        | string | no | iOS/Android       | yes |
| loginBtnTextSize | Authorization login button text font size (China Unicom, China Telecom, China Mobile)        | number or string | no | iOS/Android      | yes |
| loginBtnDisabledTextColor | Authorization login button text color when disabled (China Mobile only)        | number or string | no | -      | yes |
| loginBtnTextColor | Authorization login button text color (China Unicom, China Telecom, China Mobile)        | number or string | no | iOS/Android      | yes |
| loginBtnTextBold | Whether the authorization login button text is bold (China Unicom, China Telecom)        | boolean | no | -      | yes |
| loginBtnColor | Authorization login button background color (China Mobile only)        | number or string | no | -      | yes |
| loginBtnDisabledColor | Authorization login button background color when disabled (China Mobile only)        | number | no | -      | yes |
| loginBtnImage | Authorization login button background image (China Unicom, China Telecom, China Mobile)        | string | no | iOS/Android      | yes |
| loginBtnNormalImage | Login button normal image        | string | no | iOS/Android      | no |
| loginBtnDisabledImage | Login button disabled image (China Mobile only)        | string | no | iOS/Android      | yes |
| loginBtnSelectedImage | Login button pressed image (China Unicom, China Telecom, China Mobile)        | string | no | iOS/Android      | no |
| loginBtnBorderColor | Authorization login button border color (China Mobile only)        | number | no | -      | yes |
| loginBtnDisabledBorderColor | Authorization login button border color when disabled (China Mobile only)        | number | no | -      | yes |
| loginBtnBorderWidth | Authorization login button border width (China Mobile only)        | number | no | -      | yes |
| loginBtnDisabledBorderWidth | Authorization login button border width when disabled (China Mobile only)        | number or string | no | -      | yes |
| loginBtnBorderRadius | Authorization login button border radius (China Mobile only)        | number | no | -      | yes |
| loginBtnX | Login button x-axis offset relative to the left side of the screen (China Unicom, China Telecom, China Mobile)        | number or string | no | iOS/Android      | yes |
| loginBtnY | Login button y-axis offset relative to the bottom edge of the title bar (China Unicom, China Telecom, China Mobile)        | number or string | no | iOS/Android      | yes |
| loginBtnW | Login button width (China Unicom, China Telecom, China Mobile)        | number or string | no | iOS/Android      | yes |
| loginBtnH | Login button height (China Unicom, China Telecom, China Mobile)        | number or string | no | iOS/Android      | yes |
| privacyOne | Privacy clause one (China Unicom, China Telecom, China Mobile)        | Array<string> | no | iOS/Android      | yes |
| privacyTwo | Privacy clause two (China Unicom, China Telecom, China Mobile)        | Array<string> | no | iOS/Android      | yes |
| privacyColor | Privacy clause color (China Unicom, China Telecom, China Mobile)        | Array<string> | no | iOS/Android      | yes |
| privacyText | Text outside the privacy clause name (China Unicom, China Telecom, China Mobile)        | Array<string> | no | iOS/Android      | yes |
| privacyTextSize | Privacy clause text font size (China Unicom, China Telecom, China Mobile)        | number | no | iOS/Android      | yes |
| privacyTextGravityMode | Privacy clause text alignment (China Unicom, China Telecom, China Mobile)        | string | no | iOS/Android      | yes |
| privacyTextBold | Whether the privacy agreement text is bold (China Unicom, China Telecom, China Mobile)        | boolean | no | -      | yes |
| privacyBookSymbolEnable | Whether to display quotation marks for privacy clause (China Unicom, China Telecom, China Mobile)        | boolean | no | iOS/Android      | yes |
| privacyUnderlineText | Whether to add underline to privacy agreement (China Unicom, China Telecom)        | boolean | no | -      | yes |
| privacyMargin | Privacy agreement edge distance (China Unicom, China Telecom)        | object | no | -      | yes |
| privacyX | Privacy clause x-axis offset relative to the left side of the screen (China Mobile only)        | number or string | no | iOS/Android      | yes |
| privacyY | Privacy clause y-axis offset relative to the bottom edge of the authorization page (China Mobile only)        | number or string | no | iOS/Android      | yes |
| privacyW | Privacy clause width        | number or string | no | iOS/Android      | no |
| privacyH | Privacy clause height        | number or string | no | iOS/Android      | no |
| privacyCheckboxHidden | Whether to hide checkBox, default is not hidden        | boolean | no | iOS/Android      | no |
| privacyCheckEnable | checkBox default state (China Unicom, China Telecom, China Mobile)        | boolean | no | iOS/Android      | yes |
| privacyCheckedImage | checkBox selected image (China Unicom, China Telecom, China Mobile)        | string | no | iOS/Android      | yes |
| privacyUncheckedImage | checkBox unselected image (China Unicom, China Telecom, China Mobile)        | string | no | iOS/Android      | yes |
| privacyCheckboxSize | Set privacy clause checkbox size (China Unicom, China Telecom, China Mobile)        | number or string | no | iOS/Android      | yes |
| privacyCheckEnable | Whether the privacy agreement is checked (China Unicom, China Telecom, China Mobile)        | boolean | no | iOS/Android      | yes |
| checkBoxX | checkbox x-axis offset (China Mobile only)        | number | no | -      | yes |
| checkBoxY | checkbox y-axis offset (China Mobile only)        | number | no | -      | yes |
| privacyCheckboxInCenter | Whether the privacy agreement checkbox is vertically centered (China Unicom, China Telecom)        | boolean | no | -      | yes |
| checkBoxShape | Privacy agreement checkbox type (China Mobile only)        | number | no | -      | yes |
| enableHintToastText | Prompt text when clicking login without checking privacy agreement (China Unicom, China Telecom, China Mobile)        | string | no | -      | yes |
| clauseAlignRuleOption | Privacy clause relative layout offset rule (China Mobile only)        | object | no | -      | yes |
| privacyWebNavColor | Privacy agreement page navigation bar color (China Unicom, China Telecom, China Mobile)        | number | no | iOS/Android      | yes |
| privacyWebNavTitleSize | Privacy agreement page navigation bar title font size (China Unicom, China Telecom, China Mobile)        | number | no | iOS/Android      | yes |
| privacyWebNavTitleColor | Privacy agreement page navigation bar title color (China Unicom, China Telecom, China Mobile)        | number | no | iOS/Android      | yes |
| privacyWebNavReturnImage | Privacy agreement page navigation bar return button image (China Unicom, China Telecom)        | string | no | iOS/Android      | yes |
| privacyNavTitleTextBold | Whether the privacy agreement page navigation bar title is bold (China Unicom, China Telecom)        | boolean | no | -     | yes |
| navColor | Navigation bar color (China Mobile only)        | number | no | iOS/Android      | yes |
| clauseNavMarginTop | Privacy agreement page title bar margin top (China Mobile only)        | number | no | -      | yes |
| showWindow | Whether to show popup window (China Unicom, China Telecom, China Mobile)        | boolean | no | iOS/Android      | yes |
| maskRect | Popup window mask layer area (China Mobile only)        | Rectangle | no | -      | yes |
| dialogColor | Popup window background color (China Unicom, China Telecom, China Mobile)        | number | no | -      | yes |
| topSafeAreaHeight | Popup window mask layer area (China Unicom, China Telecom interface)        | number | no | -      | yes |
| bottomSafeAreaHeight | Bottom safe area height (China Unicom, China Telecom interface)        | number | no | -      | yes |
| returnBtnImgPath | Return button image (China Unicom, China Telecom)        | string | no | -      | yes |
| returnBtnHidden | Whether to hide return button (China Unicom, China Telecom)        | boolean | no | -      | yes |
| returnBtnWidth | Return button width (China Unicom, China Telecom)        | number | no | -      | yes |
| returnBtnHeight | Return button height (China Unicom, China Telecom)        | number | no | -      | yes |
| returnBtnOffsetX | Return button x-axis offset (China Unicom, China Telecom)        | number | no | -      | yes |
| returnBtnOffsetY | Return button y-axis offset (China Unicom, China Telecom)        | number | no | -      | yes |
| logoConstraints | LOGO image layout object      | array | no | iOS/Android      | no |
| numberConstraints | Phone number bar layout object      | array | no | iOS/Android      | no |
| sloganConstraints | Slogan layout object      | array | no | iOS/Android      | no |
| logBtnConstraints | Button layout object      | array | no | iOS/Android      | no |
| privacyConstraints | Privacy clause layout object      | array | no | iOS/Android      | no |
| checkViewConstraints | checkBox layout object      | array | no | iOS/Android      | no |
| loadingConstraints | Loading layout object      | array | no | iOS/Android      | no |
| windowBackgroundImage | Popup window internal background image      | string | no | iOS/Android      | no |
| windowBackgroundAlpha | Popup window external transparency      | number | no | iOS/Android      | no |
| windowCornerRadius | Popup window corner radius value      | number | no | iOS/Android      | no |
| windowConstraints | Popup window layout object      | array | no | iOS/Android      | no |
| windowCloseBtnImgs | Popup window close button images      | array | no | iOS/Android      | no |
| windowCloseBtnConstraints | Popup window close button layout      | array | no | iOS/Android      | no |

#### customViewParams

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- |----------| -------- |-------------------|
| customViewParams | Custom view parameters  | object | yes | iOS/Android  | no |

## Known Issues
- [ ] removeListener，getVerifyCode，setCodeTime，addCustomViewsClickCallback，statusBarHidden，navHidden，navColor，navTitle，navTitleSize，navTitleColor，navReturnHidden，navReturnImage，navReturnX，navReturnY，navReturnW，navReturnH，sloganHidden，sloganW，sloganH，loginBtnNormalImage，loginBtnSelectedImage，privacyW，privacyH，privacyCheckboxHidden，logoConstraints，numberConstraints，sloganConstraints，logBtnConstraints，privacyConstraints，checkViewConstraints，loadingConstraints，windowBackgroundImage，windowBackgroundAlpha，windowCornerRadius，windowConstraints，windowCloseBtnImgs，windowCloseBtnConstraints，customViewParams These interface properties are not supported in the Aurora Security Authentication Harmony SDK
[issue#6](https://github.com/react-native-oh-library/jverification-react-native/issues/6)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/jverification-react-native/blob/master/LICENSE).
