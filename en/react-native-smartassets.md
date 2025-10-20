> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-smartassets</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/smallnew/react-native-smartassets">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/smallnew/react-native-smartassets/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/smallnew/react-native-smartassets)

## Installation and Usage

Please go to the release address of the third-party library to view the matching version information: [@react-native-oh-tpl/react-native-smartassets Releases](https://github.com/smallnew/react-native-smartassets/releases). For older versions not published to npm, please refer to the [Installation Guide](/en/tgz-usage.md) to install the tgz package.

Navigate to the project directory and enter the following command:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-smartassets
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-smartassets
```

<!-- tabs:end -->

The code below demonstrates the basic usage scenario of this library:

> [!WARNING] The library name remains unchanged when importing.

```js
import React from 'react';
import { View, Image } from 'react-native';
import { SmartAssets } from 'react-native-smartassets';

export default function App() {
  // Initialize SmartAssets when the app starts
  SmartAssets.initSmartAssets();

  return (
    <View>
      {/* Use Image component normally, SmartAssets will handle asset loading automatically */}
      <Image 
        source={require('./assets/images/demo.png')} 
        style={{ width: 100, height: 100 }}
      />
    </View>
  );
}
```

## Link

Currently, HarmonyOS does not support AutoLink, so the Link steps need to be configured manually.

First, use DevEco Studio to open the HarmonyOS project `harmony`

### 1. Add overrides field in `oh-package.json5` at the project root directory

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introduce Native Code

There are two methods currently:

1. Via har package (this method will be deprecated after IDE improves related features, currently preferred);
2. Direct linking to source code.

Method 1: Via har package (Recommended)

> [!TIP] The har package is located in the `harmony` folder of the third-party library installation path.

Open `entry/oh-package.json5` and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-smartassets": "file:../../node_modules/@react-native-oh-tpl/react-native-smartassets/harmony/smartassets.har"
  }
```

Click the `sync` button in the upper right corner

Or execute in the terminal:

```bash
cd entry
ohpm install
```

Method 2: Direct linking to source code

> [!TIP] For direct linking to source code, please refer to [Direct Source Code Linking Guide](/en/link-source-code.md)

### 3. Configure CMakeLists and Introduce SmartAssetsPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-smartassets/src/main/cpp" ./smartassets)
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
+ target_link_libraries(rnoh_app PUBLIC smartassets)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SmartAssetsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<SmartAssetsPackage>(ctx)
    };
}
```

### 4. Introduce SmartAssetsPackage on ArkTs Side

Open `entry/src/main/ets/RNPackagesFactory.ts` and add:

```diff
  ...
+ import { SmartAssetsPackage } from '@react-native-oh-tpl/react-native-smartassets';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SmartAssetsPackage(ctx)
  ];
}
```

### 5. Run

Click the `sync` button in the upper right corner

Or execute in the terminal:

```bash
cd entry
ohpm install
```

Then compile and run.

## Constraints and Limitations

### Compatibility

To use this library, the correct React-Native and RNOH versions are required. Additionally, you need to use the matching DevEco Studio and phone ROM.

Please go to the corresponding Releases page of the third-party library to view the matching version information: [@react-native-oh-tpl/react-native-smartassets Releases](https://github.com/smallnew/react-native-smartassets/releases)

This document is verified based on the following versions:

1. RNOH: 0.72.32; SDK: HarmonyOS-Next-DB6 5.0.0.61; IDE: DevEco Studio 5.0.3.706; ROM: 3.0.0.61;

<!-- ### Usage Limitations

- Only supports local image assets referenced via `require()`
- Does not support network images (http/https URLs)
- Image files must have valid image extensions (.png, .jpg, .jpeg, .gif, .webp, .svg, .bmp, .tiff) -->

## Static Methods

> [!TIP] The "Platform" column indicates the platform supported by the attribute in the original third-party library.

> [!TIP] If "HarmonyOS Support" is "yes", it means HarmonyOS platform supports this property; "no" means not supported; "partially" means partially supported. The usage method is cross-platform consistent, and the effect is aligned with iOS or Android.

SmartAssets is a React Native image asset intelligent loading library. It changes the React Native image loading logic by hooking the `AssetSourceResolver.defaultAsset` method, allowing applications to intelligently load image resources from application packages (Android APK, iOS IPA, HarmonyOS HAP) and file system sandbox paths.

**Name** | **Description** | **Type** | **Required** | **Platform** | **HarmonyOS Support**
-- | -- | -- | -- | -- | --
initSmartAssets | Initialize SmartAssets and set up image loading hook | function | yes | All | yes
findAssetInBundles | Find image resource with specified name in application package and sandbox paths | function | no | Harmony | yes

## Known Issues

## Others

## License

This project is based on [The MIT License (MIT)](https://github.com/smallnew/react-native-smartassets/blob/master/LICENSE), please enjoy and participate in open source freely.
