> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-capinsets-next</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mayconmesquita/react-native-image-capinsets-next">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-image-capinsets-next)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information:

| Third-party Library Version | Release Information                                                                                                                                                  | Supported RN Version |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| 0.6.1@deprecated            | [@react-native-oh-tpl/react-native-image-capinsets-next Releases(deprecated)](https://github.com/react-native-oh-library/react-native-image-capinsets-next/releases) | 0.72       |
| 0.6.2                       | [@react-native-ohos/react-native-image-capinsets-next Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-capinsets-next/releases)                | 0.72       |
| 0.7.0                       | [@react-native-ohos/react-native-image-capinsets-next Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-capinsets-next/releases)                | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-image-capinsets-next
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-image-capinsets-next
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import ImageCapInset from "react-native-image-capinsets-next";
import React, { useState } from "react";
import { View, StyleSheet, Text, Switch } from "react-native";

const YourImage = () => {
  const img1 = require("./capinset_bg.png");
  const img2 = require("./capinset_bg2.png");
  const initInset = JSON.stringify({ top: 4, right: 3, bottom: 4, left: 12 });
  const initInset2 = JSON.stringify({ top: 1, right: 1, bottom: 1, left: 5 });
  const [currentImg, setCurrentImg] = useState(img1);
  const [currentCapInset, setCurrentCapInset] = useState(JSON.parse(initInset));

  const onChangeUrl = () => {
    const url = currentImg === img1 ? img2 : img1;
    setCurrentImg(url);
  };

  const onChangeInset = () => {
    const inset =
      JSON.stringify(currentCapInset) === initInset ? initInset2 : initInset;
    setCurrentCapInset(JSON.parse(inset));
  };

  return (
    <View style={styles.container}>
      <ImageCapInset
        style={styles.imgStyle}
        source={currentImg}
        capInsets={currentCapInset}>
        <Text>image content 2</Text>
      </ImageCapInset>
      <View style={styles.switchItem}>
        <Text>switch image: </Text>
        <Switch
          trackColor={{ false: "#767577", true: "#81b0ff" }}
          thumbColor={currentImg === img1 ? "#f5dd4b" : "#f4f3f4"}
          ios_backgroundColor="#3e3e3e"
          onValueChange={onChangeUrl}
          value={currentImg === img1 ? true : false}
        />
      </View>
      <View style={styles.switchItem}>
        <Text>switch Inset: </Text>
        <Switch
          thumbColor={currentCapInset === initInset ? "#f5dd4b" : "#f4f3f4"}
          onValueChange={onChangeInset}
          value={JSON.stringify(currentCapInset) === initInset ? true : false}
        />
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    paddingTop: 50,
    justifyContent: "center",
    alignItems: "center",
  },
  imgStyle: {
    width: 200,
    height: 40,
    display: "flex",
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "lightblue",
  },
  switchItem: {
    display: "flex",
    flexDirection: "row",
    alignItems: "center",
  },
});

export default YourImage;
```

## Use Codegen

Version >= @react-native-ohos/react-native-image-capinsets-next@0.6.2, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-image-capinsets-next@0.6.2 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks. Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-image-capinsets-next": "file:../../node_modules/@react-native-ohos/react-native-image-capinsets-next/harmony/rn_image_capinsets.har"
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

### 3.Configure CMakeLists and introduce ImageCapinsetsNextPackage

> [!TIP] If using version 0.6.2, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add：

```
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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-image-capinsets-next/src/main/cpp" ./rn-image-capinsets)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_rn_image_capinsets)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add：

```
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ImageCapinsetsNextPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ImageCapinsetsNextPackage>(ctx),
    };
}
```

### 4. Introducing RNCImageCapInsets Component to ArkTS

(If the code of the repository is written through CAPI, delete this section.)<br>Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { IMAGE_CAP_INSETS, RNCImageCapInsets } from "@react-native-ohos/react-native-image-capinsets-next"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === IMAGE_CAP_INSETS) {
+   RNCImageCapInsets({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag,
+   })
+ }
...
}
...
```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ IMAGE_CAP_INSETS
  ];
```

### 5. Introducing RNCImageCapInsetsPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNCImageCapInsetsPackage } from '@react-native-ohos/react-native-image-capinsets-next/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNCImageCapInsetsPackage(ctx)
  ];
}
```

### 6. Running

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

| Name      | Description                                                                                                                                                                                                                                     | Type                                                              | Required | Platform | HarmonyOS Support |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- | -------- | -------- | ----------------- |
| source    | Image source data                                                                                                                                                                                                                               | [ImageSource](https://reactnative.cn/docs/next/image#imagesource) | yes      | All      | yes               |
| capInsets | When the image is scaled, the size of the corners specified by the capInsets is fixed without scaling, while the rest of the middle and sides are stretched. This is useful for making variable-size rounded button shadows and other resources | [Rect](https://reactnative.cn/docs/next/rect)                     | no       | All      | yes               |

## Others

## License

This project is licensed under [The MIT License (MIT)](https://www.mit-license.org).

