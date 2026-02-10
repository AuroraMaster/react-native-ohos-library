> Template version: v0.4.0

<p align="center">
  <h1 align="center"> <code>react-native-worklets</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-reanimated/tree/main/packages/react-native-worklets">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/software-mansion/react-native-reanimated/blob/main/packages/react-native-worklets/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

This project is based on [react-native-worklets@0.7.1](https://github.com/software-mansion/react-native-reanimated/tree/worklets-0.7.1/packages/react-native-worklets)。

This third-party library supports direct download from npm. Its package name is: @react-native-ohos/react-native-worklets

|Name| Version                 | Release Information                                      |  Supported RN Version                |Supported Autolink| Compile API Version |Community Baseline Version |npm Address|
|---------| ------------------------- | ------------------------------------------------- |  -------------------------- | ---| ---|----|----|
|@react-native-ohos/react-native-worklets | ~1.0.0                | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-reanimated/tree/br_rnoh0.82/package/react-native-worklets)  | 0.82.* | No|API12+|0.7.1|[Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-worklets)|
## 1. Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm intstall react-native-worklets@0.7.1
npm install @react-native-ohos/react-native-worklets
```

#### **yarn**

```bash
yarn add react-native-worklets@0.7.1
yarn add @react-native-ohos/react-native-worklets
```

<!-- tabs:end -->

#### Plugin configuration

Add the `react-native-worklets/plugin` plugin to `babel.config.js`:

> [!TIP] Why is this necessary? The Babel plugin automatically converts special JavaScript functions (referred to as worklets) so that they can be passed and run on the UI thread.

```js
  module.exports = {
    presets: [
      ... // don't add it here :)
    ],
    plugins: [
      ...
      'react-native-worklets/plugin',
    ],
  };
```

Clear the cache of Metro (recommended):

<!-- tabs:start -->

#### **npm**

```bash
npm start --reset-cache
```

#### **yarn**

```bash
yarn start --reset-cache
```

<!-- tabs:end -->

The following code demonstrates the basic usage scenario of this library:

> [!WARNING] When using, the name of the imported library remains unchanged.

```js
import { runOnUIAsync} from 'react-native-worklets';
  
import React, { useState } from 'react';
import { Platform, StyleSheet, Text, View,Button } from 'react-native';

export default function RunOnUIAsync() {
const [textResult,setTextResult] = useState<string>("")

const result: Promise<string> = runOnUIAsync((): string => {
  return "runOnUIAsync";
});

 return (
    <View style={styles.container}>
        
        <Text>runOnUIAsync:{textResult}</Text>

        <Button
           title="run"
                onPress={async() => {
                  let str =  await result
                  setTextResult(JSON.stringify(str))
                }}
         />
    </View>
  );
}

  const styles = StyleSheet.create({
    container: {
      flex: 1,
      padding: 20,
      backgroundColor:"white"
    },
    text: {
      fontSize: 16,
      marginVertical: 4,
    },
    bold: {
      fontWeight: 'bold',
    },
  });
```

## 2. Manual Link

|                                      | 	Supported Autolink | Supported RN Version |
|--------------------------------------|-----------------|------------|
| ~1.0.0                                |  No              |  0.82     |

Projects using AutoLink need to be configured according to this document, AutoLink framework guide.：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you are using supports Autolink and the project has integrated Autolink, you can skip the ManualLink configuration.

<details>
  <summary>ManualLink: This step provides guidance for manually configuring native dependencies.</summary>

Open the harmony directory of the HarmonyOS project in DevEco Studio.

### 2.1. Overrides RN SDK
To ensure the project relies on the same version of the RN SDK, you need to add an overrides field in the project's root oh-package.json5 file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the official documentation.
```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony",
  }
}
```

### 2.2 .Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-worklets": "file:../../node_modules/@react-native-ohos/react-native-worklets/harmony/worklets.har"
  }
```

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md)

### 2.3. Configuring CMakeLists and Introducing ReanimatedWorkletPackage

Open  `entry/src/main/cpp/CMakeLists.txt`，and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-worklets/src/main/cpp" ./worklets)

# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_worklets)

# RNOH_BEGIN: manual_package_linking_2
```

Open  `entry/src/main/cpp/PackageProvider.cpp`， and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ReanimatedWorkletPackage.h"
using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ReanimatedWorkletPackage>(ctx)
    };
}
```

### 2.4. Introducing ReanimatedWorkletPackage Component to ArkTS

Open `entry/src/main/ets/RNPackagesFactory.ts`，and add the following code:

```diff
  ...
+ import { ReanimatedWorkletPackage } from '@react-native-ohos/react-native-worklets'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ReanimatedWorkletPackage(ctx),
  ];
}
```

</details>

### 2.5 Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1 Compatibility

This document is verified based on the following versions:

1. RNOH: 0.82.7;  SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1.260; ROM: 6.0.0.130 SP15;

## 4. API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                                                                                                                                                                                                                | Type     | Required | Platform | HarmonyOS Support |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |----------| -------- | -------- | ----------------- |
| `createWorkletRuntime`       | lets you create a new JS runtime which can be used to run worklets possibly on different threads than JS or UI thread. | function | No       | All      | yes               |
| `runOnUIAsync`       | lets you asynchronously run workletized functions on the UI thread. | function | No       | All      | yes               |
| `runOnUISync`        | lets you run a workletized function synchronously on the UI Runtime.| function | No       | All      | yes               |
| `scheduleOnRN`       | lets you schedule a function to be executed on the RN Runtime from any Worklet Runtime.| function | No       | All      | yes               |
| `scheduleOnRuntime`   | lets you schedule a worklet to be executed on a Worker Runtime.| function | No       | All      | yes               |
| `scheduleOnUI` | ulets you schedule a function to be executed on the UI Runtime.| function | No       | All      | yes               |
| `createSerializable` | recursively converts JavaScript values into Serializable references that can be passed to different JavaScript Runtimes. | function | No       | All      | yes               |
| `createSynchronizable ` | creates a new Synchronizable holding the provided initial value. Returns the created Synchronizable. | function | No       | All      | yes               |
| `isSerializableRef ` | asserts whether a value is a Serializable reference. | function | No       | All      | 
| `isSynchronizable ` | asserts whether a value is a Synchronizable. | function | No       | All      | yes               |
| `registerCustomSerializable  ` | lets you register your own pre-serialization and post-deserialization logic. | function | No       | All      | yes               |
| `getRuntimeKind` | allows you to get the kind of the current runtime.  | function | No       | All      | yes               |
| `isWorkletFunction` |  checks if a function is a worklet function.  | function | No       | All      | yes               |
| `getStaticFeatureFlag` | A function for obtaining static functionality flags (feature flags)                | function  | no       | All      | yes               |


## 5. Others

## 6. License

This project is licensed under [The MIT License (MIT)](https://github.com/software-mansion/react-native-reanimated/blob/main/packages/react-native-worklets/LICENSE) ，Please freely enjoy and participate in open source.
