> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-bars</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/zoontek/react-native-bars">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/zoontek/react-native-bars/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-bars)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                                                                                  | Supported RN Version |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| <= 2.4.3-0.0.3@deprecated   | [@react-native-oh-tpl/react-native-bars Releases(deprecated)](https://github.com/react-native-oh-library/react-native-bars/releases) | 0.72       |
| 2.4.4                       | [@react-native-ohos/react-native-bars Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-bars/releases)                | 0.72       |
| 2.5.0                       | [@react-native-ohos/react-native-bars Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-bars/releases)                | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-bars
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-bars
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from "react";
import { Switch, Text, View } from "react-native";
import { StatusBar } from "react-native-bars";

export function BarExample() {
  const [isEnabled, setIsEnabled] = React.useState(false);
  const toggleSwitch = () => setIsEnabled((previousState) => !previousState);

  return (
    <View>
      <StatusBar barStyle={isEnabled ? "light-content" : "dark-content"} />
      <Text style={{ color: "white" }}>close dark-content/ open light-content</Text>
      <Switch
        trackColor={{ false: "#767577", true: "#81b0ff" }}
        thumbColor={isEnabled ? "#f5dd4b" : "#f4f3f4"}
        ios_backgroundColor="#3e3e3e"
        onValueChange={toggleSwitch}
        value={isEnabled}
      />
    </View>
  );
}
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink  | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~2.5.0                               |  No                   |  0.77                |
| ~2.4.4                               |  Yes                  |  0.72                |
| <= 2.4.3-0.0.3@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md.

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

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
    "@react-native-ohos/react-native-bars": "file:../../node_modules/@react-native-ohos/react-native-bars/harmony/bars.har"

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

### 3.Configuring CMakeLists and Introducing RNBarsPackage

> If you are using version <=  2.4.3-0.0.3, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-bars/src/main/cpp" ./native-bars)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
        ${GENERATED_CPP_FILES}
        ./PackageProvider.cpp"
        "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_native-bars)
# RNOH_END: manual_package_linking_2
```
Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:
```diff
#include "RNOH/PackageProvider.h"
+ #include "RNBarsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx)
{
     return {
+    std::make_shared<RNBarsPackage>(ctx)
    };
}
```
### 4. Introducing RNBarsPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {RNBarsPackage} from '@react-native-ohos/react-native-bars/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNBarsPackage(ctx)
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

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### StatusBar

| Name     | Description                                                                                   | Type    | Required | Platform | HarmonyOS Support |
| -------- | --------------------------------------------------------------------------------------------- | ------- | -------- | -------- | ----------------- |
| barStyle | Status Bar Style                                                                              | string  | yes      | all      | yes               |
| animated | Should transition between status bar property changes be animated? (has no effect on Android) | boolean | no       | all      | no             |

### NavigationBar

| Name     | Description          | Type   | Required | Platform | HarmonyOS Support |
| -------- | -------------------- | ------ | -------- | -------- | ----------------- |
| barStyle | Navigation Bar Style | string | yes      | all      | no                |

### SystemBar

| Name     | Description                                                                                   | Type    | Required | Platform | HarmonyOS Support |
| -------- | --------------------------------------------------------------------------------------------- | ------- | -------- | -------- | ----------------- |
| barStyle | System Style                                                                                  | string  | yes      | all      | no                |
| animated | Should transition between status bar property changes be animated? (has no effect on Android) | boolean | no       | all      | no                |

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### StatusBar

| Name              | Description                            | Type                                                                     | Required | Platform | HarmonyOS Support |
| ----------------- | -------------------------------------- | ------------------------------------------------------------------------ | -------- | -------- | ----------------- |
| pushStackEntry    | Add an instance to the heap queue      | StatusBar.pushStackEntry(props)                                          | no       | all      | yes               |
| popStackEntry     | Delete an instance from the heap queue | StatusBar.popStackEntry(entry/_: StatusBarProps_/): void;                | no       | all      | yes               |
| replaceStackEntry | Replace an instance of the heap queue  | const entry: StatusBarProps = StatusBar.replaceStackEntry(entry ,props ) | no       | all      | yes               |

### NavigationBar

| Name              | Description                            | Type                                                                             | Required | Platform | HarmonyOS Support |
| ----------------- | -------------------------------------- | -------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| pushStackEntry    | Add an instance to the heap queue      | NavigationBar.pushStackEntry(props)                                              | no       | all      | no                |
| popStackEntry     | Delete an instance from the heap queue | NavigationBar.popStackEntry(entry/_: NavigationBarProps_/): void;                | no       | all      | no                |
| replaceStackEntry | Replace an instance of the heap queue  | const entry: NavigationBarProps = NavigationBar.replaceStackEntry(entry ,props ) | no       | all      | no                |

## Known Issues

- [ ] react-native-bars 不支持 NavigationBar 问题: [issue#16](https://github.com/react-native-oh-library/react-native-bars/issues/16)
- [ ] StatusBar不支持属性animated: [issue#21](https://github.com/react-native-oh-library/react-native-bars/issues/21)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/zoontek/react-native-bars/blob/main/LICENSE).

