> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-compass-heading</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/firofame/react-native-compass-heading">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/firofame/react-native-compass-heading/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/react-native-oh-library/react-native-compass-heading)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 1.5.0-0.0.2@deprecated   | [@react-native-oh-tpl/react-native-compass-heading Releases(deprecated)](https://github.com/react-native-oh-library/react-native-compass-heading/releases) | 0.72                 |
| 1.5.1             | [@react-native-ohos/react-native-compass-heading Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-compass-heading/releases)   | 0.72       |
| 2.0.3             | [@react-native-ohos/react-native-compass-heading Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-compass-heading/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-compass-heading
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-compass-heading
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from "react";
import { useState, useEffect } from "react";
import { StyleSheet, View, Text, Button, ScrollView } from "react-native";
import CompassHeading from "react-native-compass-heading";

export function RNCompassHeading() {
  const [heading, setHeading] = useState(0);
  const [accuracy, setAccuracy] = useState(0);

  interface Data {
    heading: number;
    accuracy: number;
  }

  useEffect(() => {
    const degree_update_rate = 3;
    CompassHeading.start(degree_update_rate, (data: Data) => {
      setHeading(data.heading);
      setAccuracy(data.accuracy);
    });
    return () => {
      CompassHeading.stop();
    };
  }, []);

  return (
    <ScrollView>
      <View
        style={{
          width: "100%",
          height: "100%",
          backgroundColor: "white",
          flex: 1,
        }}
      >
        <View style={styles.container}>
          <Text>{"heading: " + heading}</Text>
          <Text>{"headings: " + accuracy}</Text>
        </View>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
    height: 400,
  },
});
```

## Use Codegen

Version >= @react-native-ohos/react-native-compass-heading@1.5.1, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-compass-heading@1.5.1 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-compass-heading": "file:../../node_modules/@react-native-ohos/react-native-compass-heading/harmony/compass_heading.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] or details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configure CMakeLists and Import RNCompassHeadingPackage

> If you are using version <= 1.5.0-0.0.2, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/@react-native-ohos/react-native-compass-heading/src/main/cpp" ./compass_heading)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_compass_heading)
# RNOH_BEGIN: manual_package_linking_2
```

> [!Tip] Note: The above definition of NODE_MODULES is the installation path of the source library. Users can define NODE_MODULES based on the installation path of the source library

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNCompassHeadingPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNCompassHeadingPackage>(ctx)
    };
}
```

### 4. Introducing RNCompassHeadingPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {RNCompassHeadingPackage} from '@react-native-ohos/react-native-compass-heading/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNCompassHeadingPackage(ctx)
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

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name  | Description   | Type                                                  | Required | Platform    | HarmonyOS Support |
| ----- | ------------- | ----------------------------------------------------- | -------- | ----------- | ----------------- |
| start | start compass | (degreeUpdateRate: number, callback: CompassCallback) | yes      | Android/iOS | yes               |
| stop  | stop compass  | void                                                  | no       | Android/iOS | yes               |

**start(degree_update_rate,callback)**

| Name               | Description               | Type                                          | Required | Platform    | HarmonyOS Support |
| ------------------ | ------------------------- | --------------------------------------------- | -------- | ----------- | ----------------- |
| degree_update_rate | compass refresh frequency | number                                        | yes      | Android/iOS | yes               |
| callback           | compass callback          | ({heading: number;accuracy: number;}) => void | yes      | Android/iOS | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/firofame/react-native-compass-heading/blob/master/LICENSE).
