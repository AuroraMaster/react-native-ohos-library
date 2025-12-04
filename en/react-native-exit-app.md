> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-exit-app</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wumke/react-native-exit-app">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/wumke/react-native-exit-app/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-exit-app)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                                                                                              | Supported RN Version |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| 2.0.0@deprecated  | [@react-native-oh-tpl/react-native-exit-app Releases(deprecated)](https://github.com/react-native-oh-library/react-native-exit-app/releases) | 0.72       |
| 2.0.1             | [@react-native-ohos/react-native-exit-app Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-exit-app/releases) | 0.72       |
| 2.1.0             | [@react-native-ohos/react-native-exit-app Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-exit-app/releases) | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install @react-native-ohos/react-native-exit-app
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-exit-app
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  useColorScheme,
  View,
  Button,
} from "react-native";
import RNExitApp from "react-native-exit-app";
import { Colors } from "react-native/Libraries/NewAppScreen";
function App(): React.JSX.Element {
  const isDarkMode = useColorScheme() === "dark";
  const backgroundStyle = {
    backgroundColor: isDarkMode ? Colors.darker : Colors.lighter,
  };
  return (
    <SafeAreaView>
      <StatusBar barStyle={"dark-content"} />
      <Button
        title="exitApp"
        onPress={() => {
          RNExitApp.exitApp();
        }}
      />
    </SafeAreaView>
  );
}

export default App;
```

## Use Codegen

Version >= @react-native-ohos/react-native-exit-app@2.0.1, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-exit-app@2.0.1 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks. Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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
    "@react-native-ohos/react-native-exit-app": "file:../../node_modules/@react-native-ohos/react-native-exit-app/harmony/exit_app.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly Link Source Code

> [!TIP] If you need to directly link the source code, please refer to the [Direct Source Code Linking Guide](/en/link-source-code.md).

### 3. Configure CMakeLists and import ExitAppPackage

> V2.0.1 requires configuring CMakeLists and importing ExitAppPackage.

Open the `entry/src/main/cpp/CMakeLists.txt` file and add the following code:

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-exit-app/src/main/cpp" ./exit_app)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_exit_app)
# RNOH_END: manual_package_linking_2
```

Open the `entry/src/main/cpp/PackageProvider.cpp` file and add the following code:

```
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ExitAppPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ExitAppPackage>(ctx),
    };
}
```

### 4. Introducing ExitAppPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+  import { ExitAppPackage } from '@react-native-ohos/react-native-exit-app/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ExitAppPackage(ctx)
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

1. RNOH: 0.72.96; SDK: HarmonyOS 5.1.0.150 (API Version 12); IDE: DevEco Studio 5.1.1.830; ROM: 5.1.0.150;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 5.0.0.71(API Version 12 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 5.1.0.150;

## Static Methods

> [!TIP]The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP]If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name    | Description   | Type     | Required | Platform    | HarmonyOS Support |
| ------- | ------------- | -------- | -------- | ----------- | ----------------- |
| exitApp | close/exit APP | Function | no       | iOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/wumke/react-native-exit-app/blob/master/LICENSE).
