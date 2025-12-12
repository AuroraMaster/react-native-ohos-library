> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-text-gradient</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/iyegoroff/react-native-text-gradient">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/iyegoroff/react-native-text-gradient/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-text-gradient)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
|-----------------------------| ------------------------------------------------------------ | ---------- |
| <= 0.1.7-0.0.4@deprecated | [@react-native-oh-tpl/react-native-text-gradient Releases(deprecated)](https://github.com/react-native-oh-library/react-native-text-gradient/releases) | 0.72       |
| 0.1.8                     | [@react-native-ohos/react-native-text-gradient Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-text-gradient/releases)               | 0.72       |
| 0.2.0                     | [@react-native-ohos/react-native-text-gradient Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-text-gradient/releases)               | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-text-gradient
```

#### **yarn**

```bash
yarn install @react-native-ohos/react-native-text-gradient
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import {StyleSheet, Text, View } from 'react-native';
import { LinearTextGradient } from 'react-native-text-gradient';
const TextGradientTest = () => {
  return (
      <View style={styles.container}>
        <LinearTextGradient
          style={styles.welcome}
          locations={[0, 1]}
          colors={['blue', 'red']}
          start={{ x: 0, y: 0 }}
          end={{ x: 1, y: 0 }}
        >Welcome to React Native!
        </LinearTextGradient>
        <Text style={styles.instructions}>To get started, edit App.js</Text>
        <Text style={styles.instructions}>{'Double tap R on your keyboard to reload,\n' +
          'Shake or press menu button for dev menu'}</Text>
      </View>
  );
}
export default TextGradientTest;


const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#ffffff',
    marginTop: 100
  },
  welcome: {
    fontSize: 20,
    width: 'auto',
    height: 'auto',
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});

```

## Link

Version >= @react-native-ohos/react-native-text-gradient@0.1.8 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks. Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

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

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
   ...
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-text-gradient": "file:../../node_modules/@react-native-ohos/react-native-text-gradient/harmony/text_gradient.har"
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

### 3. Configuring CMakeLists and Introducing LinearTextGradientPackge

> If you are using version <= 0.1.7-0.0.4, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-text-gradient/src/main/cpp" ./text_gradient)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_text_gradient)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "LinearTextGradientPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<LinearTextGradientPackage>(ctx),
    };
}
```

### 4. Introducing  LinearTextGradientPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {LinearTextGradientPackage} from '@react-native-ohos/react-native-text-gradient/ts';
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new LinearTextGradientPackage(ctx)
  ];
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

Verified successfully in the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name            |                                                                           Description                                                               |  Type  | Required | Platform     | HarmonyOS Support  |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------| ------ | -------- | -------------| ------------------ |
| start           | Coordinates declare the position that the gradient starts at, as a fraction of the overall size of the gradient, starting from the top left corner. | number |   no    | iOS/Android  |       yes          |
| end             | Same as start, but for the end of the gradient.                                                                                                     | number |   no    | iOS/Android  |       yes          |
| loactions       | An optional array of numbers defining the location of each gradient color stop, mapping to the color with the same index in prop.                   | number[]  |   no    | iOS/Android  |       yes          |
| colors          | An array of at least two color values that represent gradient colors.                                                                               | string   |   yes    | iOS/Android  |       yes          |
| useViewFrame    | Optional. If true gradient will be calculated for text view background frame rather than text frame.                                                | boolean  |   no    | iOS/Android  |       no          |
| useGlobalCache  | accessing or managing a cache that is available globally throughout the application.                                                               | boolean  |   no    | iOS  |       no         |


## Known Issues

- [ ] The useGlobalCache() is not supported in HarmonyOS[issue#7](https://github.com/react-native-oh-library/react-native-text-gradient/issues/7)
- [ ] The useViewFrame() is not supported in HarmonyOS.[issue#1](https://github.com/react-native-oh-library/react-native-text-gradient/issues/1)


## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/iyegoroff/react-native-text-gradient/blob/master/LICENSE).

