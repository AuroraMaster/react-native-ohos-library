> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-keep-awake</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/corbt/react-native-keep-awake">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/corbt/react-native-keep-awake/blob/master/LICENCE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-keep-awake)

## Installation and Usage

Find the matching version information in the release address of a third-party library: 

| ---------- | ------------------------------------------------------------ | ---------- |
| <= 4.0.0-0.0.1@deprecated     | [@react-native-oh-tpl/react-native-keep-awake Releases(deprecated)](https://github.com/react-native-oh-library/react-native-keep-awake/releases) | 0.72       |
| 4.0.1      | [@react-native-ohos/react-native-keep-awake Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-keep-awake/releases) | 0.72       |
| 4.1.0      | [@react-native-ohos/react-native-keep-awake Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-keep-awake/releases) | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-keep-awake
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-keep-awake
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useEffect } from "react";
import { Text, Button } from "react-native";

import KeepAwake, {
  activateKeepAwake,
  deactivateKeepAwake,
  useKeepAwake,
} from "react-native-keep-awake";

export function KeepAwakeExample() {
  useKeepAwake();

  const handleClick = (buttonId: number) => {
    switch (buttonId) {
      case 1:
        deactivateKeepAwake();
        break;
      case 2:
        activateKeepAwake();
        break;
      case 3:
        deactivateKeepAwake();
        break;
      case 4:
        KeepAwake.activate();
        break;
      case 5:
        KeepAwake.deactivate();
        break;
      default:
        break;
    }
  };

  return (
    <>
      <Text style={{ color: "blue" }}>
        Button 1: Hook default method enabled (always
        on),----useKeepAwake(),Click button 1 to turn off the constant light
      </Text>
      <Button title="Button 1" onPress={() => handleClick(1)}></Button>

      <Text style={{ color: "blue" }}>
        Button 2: Enable functions method----activateKeepAwake()
      </Text>
      <Button title="Button 2" onPress={() => handleClick(2)}></Button>

      <Text style={{ color: "blue" }}>
        Button 3: Close the function method----deactivateKeepAwake()
      </Text>
      <Button title="Button 3" onPress={() => handleClick(3)}></Button>

      <Text style={{ color: "blue" }}>
        Button 4: Old interface method----KeepAwake.activate()
      </Text>
      <Button title="Button 4" onPress={() => handleClick(4)}></Button>

      <Text style={{ color: "blue" }}>
        Button 5: Old interface method----KeepAwake.deactivate()
      </Text>
      <Button title="Button 5" onPress={() => handleClick(5)}></Button>
    </>
  );
}
```

## 使用 Codegen

Version >= @react-native-ohos/react-native-keep-awake@4.0.1, now supports Codegen to generate bridging code.

This repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-keep-awake@4.0.1, now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

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
    "@react-native-ohos/react-native-keep-awake": "file:../../node_modules/@react-native-ohos/react-native-keep-awake/harmony/keep_awake.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] The source code is stored in the `harmony` folder in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-keep-awake": "file:../../node_modules/@react-native-ohos/react-native-keep-awake/harmony/keep_awake"
  }
```

run the following instruction on the terminal:

```bash
cd entry
ohpm install --no-link
```

### 3.Configuring CMakeLists and Introducing RNThemeControlPackage

> If you are using version <= 4.0.0-0.0.1, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt`， and add:

```cmake
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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-keep-awake/src/main/cpp" ./keep-awake)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_keep_awake)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```c++
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "KeepAwakePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<KeepAwakePackage>(ctx)
    };
}
```

### 4. Introducing RNKeepAwakePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNKeepAwakePackage } from "@react-native-ohos/react-native-keep-awake/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNKeepAwakePackage(ctx)
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

## Usage

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] Both old and new APIs can be used in the form of functions.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                   | Description                                    | Required | Platform | HarmonyOS Support |
| ---------------------- | ---------------------------------------------- | -------- | -------- | ----------------- |
| `<KeepAwake/>`         | Component that activates the current screen-on mode.            | No       | All      | yes               |
| KeepAwake.activate()   | Function that deactivates the current screen-on mode (old API).| No       | All      | yes               |
| KeepAwake.deactivate() | Function that deactivates the current screen-on mode (old API).| No       | All      | yes               |
| useKeepAwake()         | Hook.                                | No       | All      | yes               |
| activateKeepAwake()    | Function that activates the current screen-on mode (new API).| No       | All      | yes               |
| deactivateKeepAwake()  | Function that deactivates the current screen-on mode (new API).| No       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/corbt/react-native-keep-awake/blob/master/LICENCE).
