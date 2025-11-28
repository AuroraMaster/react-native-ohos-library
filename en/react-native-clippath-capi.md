> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-clippath(CAPI)</code> </h1>
</p>
<p align="center">
 <a href="https://github.com/Only-IceSoul/react-native-clippath">
        <img src="https://img.shields.io/badge/platforms-ios%20%7C%20android%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-clippath/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-clippath/tree/capi)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                                                                                              | Supported RN Version |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| 1.1.8@deprecated            | [@react-native-oh-tpl/react-native-clippathview Releases(deprecated)](https://github.com/react-native-oh-library/react-native-clippath/releases) | 0.72       |
| 1.1.9                       | [@react-native-ohos/react-native-clippathview Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-clippath/releases)                | 0.72       |
| 1.2.0                       | [@react-native-ohos/react-native-clippathview Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-clippath/releases)                | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-clippathview
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-clippathview
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```jsx
import { View, Text, ScrollView } from "react-native";
import React from "react";
import { ClipPathView } from "react-native-clippathview";

export default function index() {
  const viewBox = [0, 0, 400, 400];
  const path = "M 0 0 L 400 0 L 0 400 L 400 400 Z";

  return (
    <ScrollView style={{ width: "100%", height: "100%" }}>
      <ClipPathView d={path} style={{ backgroundColor: "#ff0" }}>
        <Text style={{ height: 800, fontSize: 26 }}>
          MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM
        </Text>
      </ClipPathView>
    </ScrollView>
  );
}
```

## Link

Version >= @react-native-ohos/react-native-clippathview@1.1.9 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks. Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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

- Use the HAR file.
- Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open  `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-clippathview": "file:../../node_modules/@react-native-ohos/react-native-clippathview/harmony/clipPath.har",
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


### 3. Configuring CMakeLists and Introducing ClipPathViewPackage

Open  `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-clippathview/src/main/cpp" ./clippath)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_clip_path )
# RNOH_BEGIN: manual_package_linking_2
```

Open  `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ClipPathViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ClipPathViewPackage>(ctx)
    };
}
```

### 4. Introducing  ClipPathPackage to ArkTS

Open the  `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { ClipPathPackage } from '@react-native-ohos/react-native-clippathview/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ClipPathPackage(ctx),
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

The following combinations have been verified:

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

## Properties 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                                                  | Type              | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ----------------- | -------- | ----------- | ----------------- |
| svgKey               | Unique key.                                                    | string            | No       | Web         | No                |
| d                    | Path shape defined by a series of commands (SVG path data).                       | string            | No       | iOS/Android | Yes               |
| viewBox              | Defines the position and dimensions in user space.                                  | Array<Number>(4)  | No       | iOS/Android | Yes               |
| align                | **align** of the **preserveAspectRatio** property.                            | string            | No       | iOS/Android | Yes               |
| aspect               | **meetOrSlice** of the **preserveAspectRatio** property.                      | meet/slice/none   | No       | iOS/Android | Yes               |
| fillRule             | Path fill rule.                                            | nonzero/evenodd   | No       | iOS/Android | Yes               |
| strokeWidth          | Path stroke width.                                                | number            | No       | iOS/Android | Yes               |
| strokeCap            | Shape of the ends of open paths.                                          | butt/round/square | No       | iOS/Android | Yes               |
| strokeJoin           | Shape used at corners of paths.                                        | bevel/miter/round | No       | iOS/Android | Yes               |
| strokeMiter          | Miter length when **strokeJoin** is **miter**.                         | number            | No       | iOS/Android | Yes               |
| strokeStart          | Percentage of the starting point of the **CAShapeLayer** stroke to the total path on iOS. The default value is **0**.| number            | No       | iOS/Android | Yes               |
| strokeEnd            | Percentage of the ending point of the **CAShapeLayer** stroke to the total path on iOS. The default value is **1**. If the value is less than or equal to that of **strokeStart**, no content is drawn.| number            | No       | iOS/Android | Yes               |
| translateZ           | Sets the positioning layer depth (similar to index).                                  | number            | No       | iOS/Android | Yes               |
| transX               | Horizontal translation in a 2D plane.                                | number            | No       | iOS/Android | Yes               |
| transY               | Vertical translation in a 2D plane.                                | number            | No       | iOS/Android | Yes               |
| transPercentageValue | Whether **transX** and **transY** use percentage values.                                   | boolean           | No       | iOS/Android | Yes               |
| rot                  | Rotation of an element around a specific point.                                        | number            | No       | iOS/Android | Yes               |
| rotOx                | Horizontal position of the rotation origin.                                          | number            | No       | iOS/Android | Yes               |
| rotOy                | Vertical position of the rotation origin.                                          | number            | No       | iOS/Android | Yes               |
| rotPercentageValue   | Whether **rotOx** and **rotOy** use percentage values.                                     | boolean           | No       | iOS/Android | Yes               |
| sc                   | Uniform scaling of an element.                                              | number            | No       | iOS/Android | Yes               |
| scX                  | X-axis scaling.                                                    | number            | No       | iOS/Android | Yes               |
| scY                  | Y-axis scaling.                                                    | number            | No       | iOS/Android | Yes               |
| scO                  | Scaling origin point.                                              | number            | No       | iOS/Android | Yes               |
| scOx                 | Horizontal position of the scaling origin.                                          | number            | No       | iOS/Android | Yes               |
| scOy                 | Vertical position of the scaling origin.                                          | number            | No       | iOS/Android | Yes               |
| scPercentageValue    | Whether **scO**, **scOx**, and **scOy** use percentage values.                                  | boolean           | No       | iOS/Android | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/Only-IceSoul/react-native-clippath/blob/main/LICENSE).