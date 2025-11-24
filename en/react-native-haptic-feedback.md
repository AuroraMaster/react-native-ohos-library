> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-haptic-feedback</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/mkuczera/react-native-haptic-feedback">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mkuczera/react-native-haptic-feedback/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-haptic-feedback)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.2.1@deprecated      | [@react-native-oh-tpl/react-native-haptic-feedback Releases(deprecated)](https://github.com/react-native-oh-library/react-native-haptic-feedback/releases) | 0.72       |
| 2.2.2      | [@react-native-ohos/react-native-haptic-feedback Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-haptic-feedback/releases)    | 0.72       |
| 2.3.4      | [@react-native-ohos/react-native-haptic-feedback Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-haptic-feedback/releases)    | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install @react-native-ohos/react-native-haptic-feedback
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-haptic-feedback
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react"
import { SafeAreaView, ScrollView, Button } from "react-native"
import ReactNativeHapticFeedback from "react-native-haptic-feedback"
const options = {
  enableVibrateFallback: false,
  ignoreAndroidSystemSettings: false,
}

const methods: Array<
  | "impactLight"
  | "impactMedium"
  | "impactHeavy"
  | "notificationSuccess"
  | "notificationWarning"
  | "notificationError"
  | "rigid"
  | "soft"
  | "selection"
  | "clockTick"
  | "contextClick"
  | "keyboardPress"
  | "keyboardRelease"
  | "keyboardTap"
  | "longPress"
  | "textHandleMove"
  | "virtualKey"
  | "virtualKeyRelease"
  | "effectClick"
  | "effectDoubleClick"
  | "effectHeavyClick"
  | "effectTick"
> = [
  "impactLight",
  "impactMedium",
  "impactHeavy",
  "notificationSuccess",
  "notificationWarning",
  "notificationError",
  "rigid",
  "soft",
  "selection",
  "clockTick",
  "contextClick",
  "keyboardPress",
  "keyboardRelease",
  "keyboardTap",
  "longPress",
  "textHandleMove",
  "virtualKey",
  "virtualKeyRelease",
  "effectClick",
  "effectDoubleClick",
  "effectHeavyClick",
  "effectTick",
]

export const HapticFeedbackExample = () => {
  return (
    <SafeAreaView>
      <ScrollView>
        {methods.map((item) => {
          return (
            <Button
              title={item}
              onPress={() => ReactNativeHapticFeedback.trigger(item, options)}
              key={item}
            ></Button>
          )
        })}
      </ScrollView>
    </SafeAreaView>
  )
}

export default HapticFeedbackExample;
```

## Use Codegen

> [!TIP] V2.2.2 no need to execute Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-haptic-feedback@2.2.2 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-haptic-feedback": "file:../../node_modules/@react-native-ohos/react-native-haptic-feedback/harmony/haptic_feedback.har"
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

### 3. Configure CMakeLists and import RNHapticFeedbackPackage

> [!TIP] If using version 2.2.1, please skip this chapter

open `entry/src/main/cpp/CMakeLists.txt`，add：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-haptic-feedback/src/main/cpp" ./haptic-feedback)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_haptic_feedback)
# RNOH_END: manual_package_linking_2
```

open `entry/src/main/cpp/PackageProvider.cpp`，add：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNHapticFeedbackPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<RNHapticFeedbackPackage>(ctx),
    };
}
```

### 4. Introducing RNImageColorsPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...
+  import { RNHapticFeedbackPackage } from '@react-native-ohos/react-native-haptic-feedback/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNHapticFeedbackPackage(ctx)
  ]
}
```

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.2.1@deprecated      | [@react-native-oh-tpl/react-native-haptic-feedback Releases(deprecated)](https://github.com/react-native-oh-library/react-native-haptic-feedback/releases) | 0.72       |
| 2.2.2      | [@react-native-ohos/react-native-haptic-feedback Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-haptic-feedback/releases)    | 0.72       |
| 2.3.4      | [@react-native-ohos/react-native-haptic-feedback Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-haptic-feedback/releases)    | 0.77       |

### Permission Requirements

Add the configuration to the **entry/src/main/module.json5** file.
```js
"requestPermissions": [ { "name": "ohos.permission.VIBRATE" }, ]
```

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### Available Methods

`trigger(method, options)`
Use this method to trigger haptic feedback

| Name                                  | Description                                                  | Type    | Required | Platform    | HarmonyOS Support |
| ------------------------------------- | ------------------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| `method`                              | Specifies the type of haptic feedback. See the list of available methods below. | string  | yes      | iOS/Android | yes               |
| `options.enableVibrateFallback`       | iOS only. If haptic feedback is unavailable (iOS < 10 OR Device < iPhone6s), vibrate with default method (heavy 1s) (default: false). | boolean | no       | iOS         | no                |
| `options.ignoreAndroidSystemSettings` | Ignoreing phone mute mode setting and triggering haptic feedback. (default: false). | boolean | no       | Android     | yes               |

### method Overview

Here's an overview of the available methods and their compatibility
| Name                  |         Description          |  Type  | Required |  Platform   | HarmonyOS Support |
| --------------------- | :--------------------------: | :----: | :------: | :---------: | :---------------: |
| `impactLight`         |     impactLight feedback     | string |    no    | iOS/Android |        yes        |
| `impactMedium`        |    impactMedium feedback     | string |    no    | iOS/Android |        yes        |
| `impactHeavy`         |     impactHeavy feedback     | string |    no    | iOS/Android |        yes        |
| `rigid`               |        rigid feedback        | string |    no    | iOS/Android |        yes        |
| `soft`                |        soft feedback         | string |    no    | iOS/Android |        yes        |
| `notificationSuccess` | notificationSuccess feedback | string |    no    | iOS/Android |        yes        |
| `notificationWarning` | notificationWarning feedback | string |    no    | iOS/Android |        yes        |
| `notificationError`   |  notificationError feedback  | string |    no    | iOS/Android |        yes        |
| `selection`           |      selection feedback      | string |    no    |     iOS     |        yes        |
| `clockTick`           |      clockTick feedback      | string |    no    |   Android   |        yes        |
| `contextClick`        |    contextClick feedback     | string |    no    |   Android   |        yes        |
| `keyboardPress`       |    keyboardPress feedback    | string |    no    |   Android   |        yes        |
| `keyboardRelease`     |   keyboardRelease feedback   | string |    no    |   Android   |        yes        |
| `keyboardTap`         |     keyboardTap feedback     | string |    no    |   Android   |        yes        |
| `longPress`           |      longPress feedback      | string |    no    |   Android   |        yes        |
| `textHandleMove`      |   textHandleMove feedback    | string |    no    |   Android   |        yes        |
| `virtualKey`          |     virtualKey feedback      | string |    no    |   Android   |        yes        |
| `virtualKeyRelease`   |  virtualKeyRelease feedback  | string |    no    |   Android   |        yes        |
| `effectClick`         |     effectClick feedback     | string |    no    |   Android   |        yes        |
| `effectDoubleClick`   |  effectDoubleClick feedback  | string |    no    |   Android   |        yes        |
| `effectHeavyClick`    |  effectHeavyClick feedback   | string |    no    |   Android   |        yes        |
| `effectTick`          |     effectTick feedback      | string |    no    |   Android   |        yes        |

## Known Issues

- [ ] Custom vibration file configuration: [issue#6](https://github.com/react-native-oh-library/react-native-haptic-feedback/issues/6)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mkuczera/react-native-haptic-feedback/blob/master/LICENSE).
