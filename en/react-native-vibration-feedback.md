> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-vibration-feedback</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/nascimentorafael/react-native-vibration-feedback">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-vibration-feedback/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-vibration-feedback)

## Installation and Usage

Find the matching version information in the release address of a third-party library：

| Version | Post Information                                                     | Support RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.0.1     | [@react-native-ohos/react-native-vibration-feedback Releases](https://github.com/react-native-oh-library/react-native-vibration-feedback/releases) | 0.72       |
| 1.1.0     | [@react-native-ohos/react-native-vibration-feedback Releases](https://github.com/react-native-oh-library/react-native-vibration-feedback/releases) | 0.77       |


Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-vibration-feedback
```


#### **yarn**

```bash
yarn add @react-native-ohos/react-native-vibration-feedback
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:
> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { View, Button} from "react-native";
import RNVibrationFeedback from 'react-native-vibration-feedback';

const App = (props) => {

  return (
    <View style={{ margin: 50, flexDirection: "column", justifyContent: "space-between" }}>
      <View>
        <Button
          title="Peek"
          onPress={() => RNVibrationFeedback.vibrateWith(1519)}
        />
        <Button
          title="Pop"
          onPress={() => RNVibrationFeedback.vibrateWith(1520)}
        />
        <Button
          title="Nope"
          onPress={() => RNVibrationFeedback.vibrateWith(1521)}
        />
      </View>
    </View>
  );
};

export default App
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

### 2.Introducing Native Code

Currently, two methods are available:

1. Use the HAR file (this method will be deprecated once the IDE supports the relevant functionality and is preferred currently).
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:
```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-vibration-feedback": "file:../../node_modules/@react-native-ohos/react-native-vibration-feedback/harmony/vibration_feedback.har"
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

### 3.Configuring CMakeLists and Introducing ReactNativeVibrationFeedbackPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-vibration-feedback/src/main/cpp" ./vibration-feedback)
# RNOH_BEGIN: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_vibration_feedback)
# RNOH_BEGIN: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp`，add：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ReactNativeVibrationFeedbackPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ReactNativeVibrationFeedbackPackage>(ctx)
    };
}
```

### 4.Introducing RNVibrationFeedbackPackage to ArkTS

Open `entry/src/main/ets/RNPackagesFactory.ts`，add：

```diff
  ...
+   import {RNVibrationFeedbackPackage} from '@react-native-ohos/react-native-vibration-feedback/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNVibrationFeedbackPackage(ctx)
  ];
}
```

### 5.Running

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

- Some functions and APIs of this library require the **normal** permission **ohos.permission.VIBRATE**.
## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### RNVibrationFeedback

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- |----------| -------- |-------------------|
| vibrateWith(id: number)  | Trigger the vibration of the specified ID       | void | yes | iOS/Android      | yes |

## Known Issues

## Others
Provide the following three types of vibration

|  ID  | Name |           Description           |
|:----:|:----:|:-------------------------------:|
| 1519 | Peek | Weak short vibration            |
| 1520 | Pop  | Strong short vibration          |
| 1521 | Nope | Three pops in a short interval  |

The vibration of 1521 needs to be above API18 to take effect. If the vibration is changed below API18, it will automatically change to the vibration type of 1519.
## License

This project is licensed under [Apache License 2.0](https://github.com/react-native-oh-library/react-native-vibration-feedback/blob/sig/LICENSE).

