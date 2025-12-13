> Template Version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-safe-area-context</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/th3rdwave/react-native-safe-area-context">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20web%20%7C%20macos%20%7C%20windows%20%7C%20harmony-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/th3rdwave/react-native-safe-area-context/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github Address](https://github.com/react-native-oh-library/react-native-safe-area-context)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
|-----------------------------| ------------------------------------------------------------ | ---------- |
| <= 4.7.4-0.2.1@deprecated | [@react-native-oh-tpl/react-native-safe-area-context Releases(deprecated)](https://github.com/react-native-oh-library/react-native-safe-area-context/releases) | 0.72       |
| 4.7.5 | [@react-native-ohos/react-native-safe-area-context Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-safe-area-context/releases)               | 0.72       |
| 5.1.1 | [@react-native-ohos/react-native-safe-area-context Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-safe-area-context/releases)               | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-safe-area-context
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-safe-area-context
```

<!-- tabs:end -->

The following code demonstrates a basic usage scenario of this library:

> [!WARNING] The import library name remains unchanged during use.

```js
import React from "react";
import { Text, View } from "react-native";
import {
  SafeAreaProvider,
  SafeAreaView,
  initialWindowMetrics,
} from "react-native-safe-area-context";

const App = () => {
  return (
    <SafeAreaProvider initialMetrics={initialWindowMetrics}>
      <SafeAreaView style={{ flex: 1, backgroundColor: "red" }}>
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
          <Text>hello</Text>
        </View>
      </SafeAreaView>
    </SafeAreaProvider>
  );
};

export default App;
```

## Link

|                                      | Is supported autolink  | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~5.1.1                               |  No                   |  0.77                |
| ~4.7.5                              |  Yes                  |  0.72                |
| <= 4.7.4-0.2.1@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

### 1. Add the overrides field to the root `oh-package.json5` of the project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Import Native Side Code

There are currently two methods:

1.  Import via har package (This method will be deprecated after IDE features are improved; currently the preferred method).
2.  Link source code directly.

Method 1: Import via har package

> [!TIP] The har package is located in the `harmony` folder of the third-party library's installation path.

Open `entry/oh-package.json5` and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-ohos/react-native-safe-area-context": "file:../../node_modules/@react-native-ohos/react-native-safe-area-context/harmony/safe_area.har"
  }
```

Click the `sync` button in the top right corner.

Or execute in the terminal:

```bash
cd entry
ohpm install
```

Method 2: Link Source Code Directly

> [!TIP] If you need to link source code directly, please refer to the [Direct Link Source Code Instructions](/en/link-source-code.md)

### 3. Configure CMakeLists and Import SafeAreaViewPackage

> If you are using version <= 4.7.4-0.2.1, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add:

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

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-safe-area-context/src/main/cpp" ./safe-area)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_safe_area)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SafeAreaViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<SafeAreaViewPackage>(ctx),
    };
}
```

### 4. Import SafeAreaViewPackage on the ArkTs Side

Open `entry/src/main/ets/RNPackagesFactory.ts` and add:

```diff
...
+ import {SafeAreaViewPackage} from '@react-native-ohos/react-native-safe-area-context/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SafeAreaViewPackage(ctx)
  ];
}
```

</details>

## Running

Click the `sync` button in the top right corner.

Or execute in the terminal:

```bash
cd entry
ohpm install
```

Then compile and run.

## Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified successfully in the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## Props

> [!TIP] The "Platform" column indicates the platforms supported by the original third-party library for that prop.

> [!TIP] A value of "yes" in the "HarmonyOS Support" column indicates the prop is supported on the HarmonyOS platform; "no" indicates it is not supported; "partially" indicates partial support. The usage method is consistent across platforms, and the effect aligns with that on iOS or Android.

**Component SafeAreaProvider**

You should add `SafeAreaProvider` in your app root component. You may need to add it in other places like the root of modals and routes when using `react-native-screens`.

Note that providers should not be inside a View that is animated with `Animated` or inside a `ScrollView` since it can cause very frequent updates.

| Name               | Description                                                                                                                                                            | Type   | Required | Platform | HarmonyOS Support |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | ----------------- |
| `Props`            | Accepts all View props. Has a default style of `{flex: 1}`.                                                                                                            | object | no       | All      | yes               |
| `initialMetrics`   | Can be used to provide the initial value for frame and insets, this allows rendering immediately. See optimization for more information on how to use this prop.       | object | no       | All      | yes               |

**Component SafeAreaView**

`SafeAreaView` is a regular View component with the safe area insets applied as padding or margin.

| Name     | Description                                                                          | Type   | Required | Platform | HarmonyOS Support |
| -------- | ------------------------------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `Props`  | Accepts all View props. Has a default style of `{flex: 1}`.                          | object | no       | All      | yes               |
| `edges`  | Sets the edges to apply the safe area insets to. Defaults to all.                    | array  | no       | All      | yes               |
| `mode`   | Optional, `padding` (default) or `margin`. Apply the safe area to either the padding or the margin. | string | no       | All      | yes               |

## API

> [!TIP] The "Platform" column indicates the platforms supported by the original third-party library for that API.

> [!TIP] A value of "yes" in the "HarmonyOS Support" column indicates the API is supported on the HarmonyOS platform; "no" indicates it is not supported; "partially" indicates partial support. The usage method is consistent across platforms, and the effect aligns with that on iOS or Android.

| Name                      | Description                                                                          | Type     | Required | Platform | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `useSafeAreaInsets`       | Returns the safe area insets of the nearest provider.                                | object   | no       | All      | yes               |
| `useSafeAreaFrame`        | Returns the frame of the nearest provider. This can be used as an alternative to the Dimensions module. | object   | no       | All      | yes               |
| `SafeAreaInsetsContext`   | React Context with the value of the safe area insets.                                | object   | no       | All      | yes               |
| `withSafeAreaInsets`<sup>5.1.1+</sup> | Higher order component that provides safe area insets as the `insets` prop.          | function | no       | All      | yes               |
| `SafeAreaFrameContext`    | React Context with the value of the safe area frame.                                 | object   | no       | All      | yes               |
| `initialWindowMetrics`    | Insets and frame of the window on initial render. This can be used with the `initialMetrics` from `SafeAreaProvider`. | object   | no       | All      | yes               |

## Known Issues

## Others

## License

This project is based on [The MIT License (MIT)](https://github.com/th3rdwave/react-native-safe-area-context/blob/main/LICENSE). Feel free to enjoy and participate in open source.