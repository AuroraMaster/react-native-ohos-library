> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-touch-id</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/naoufal/react-native-touch-id">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/naoufal/react-native-touch-id?tab=readme-ov-file#license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-touch-id)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                     | Supported RN Version |
|-------| ------------------------------------------------------------ | ---------- |
| <= 4.4.1-0.0.3@deprecated   | [@react-native-oh-tpl/react-native-touch-id Releases(deprecated)](https://github.com/react-native-oh-library/react-native-touch-id/releases) | 0.72                 |
| 4.4.2 | [@react-native-ohos/react-native-touch-id Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-touch-id/releases)                        | 0.72       |
| 4.5.0 | [@react-native-ohos/react-native-touch-id Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-touch-id/releases)                        | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-touch-id
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-touch-id
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component, useState } from 'react';
import { Alert, View, Button, Text } from 'react-native';
import TouchID from 'react-native-touch-id';

const App = () => {
  const [result, setResult] = useState<string>('')
  return (
     <View>
      <Text style={{ height: 40, backgroundColor: 'white', textAlign: 'center' }}>{result}</Text>
      <Button title='check whether you have fingerprint permission'
        onPress={() => {
          TouchID.isSupported({ unifiedErrors: false }).then((res: any) => {
            setResult(res)
          }).catch((err: any) => {
            setResult(err.message)
          })
        }}
      ></Button>
      <Button title='check fingerprint'
        onPress={() => {
          TouchID.authenticate().then((res: boolean) => {
            setResult('Authentication successful')
          }).catch((err: any) => {
            setResult(err.message)
          })
        }}
      ></Button>
    </View>
  )
};

export default App;

```
## Use Codegen

Version >= @react-native-ohos/react-native-touch-id@4.4.2, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-touch-id@4.4.2 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks. Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1.Open `entry/oh-package.json5` file and add the following dependencies:

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
    "@react-native-ohos/react-native-touch-id": "file:../../node_modules/@react-native-ohos/react-native-touch-id/harmony/touch_id.har"
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

### 3. Configuring CMakeLists and Introducing TouchIdPackage

> If you are using version <= 4.4.1-0.0.3, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-touch-id/src/main/cpp" ./touch_id)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_touch_id)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "TouchIdPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<TouchIdPackage>(ctx)
    };
}
```

### 4. Introducing TouchIdPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { TouchIdPackage } from "@react-native-ohos/react-native-touch-id/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new TouchIdPackage(ctx)
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

### Permission Requirements

(Enter the related permission configuration.)

Add the following permissions to their respective files:

In your `module.json5`

```
 "requestPermissions": [
      {
        "name": "ohos.permission.ACCESS_BIOMETRIC"
      }
    ]
```

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| isSupported  | Whether touchid is supported | function  | yes | ios/andriod      | yes |
| authenticate  | Verify touchid | function  | yes | ios/andriod      | yes |
## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### Errors

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Touch ID Error  | Permission verification failed | string  | no | harmonry      | yes |
| Touch ID Error  | Incorrect parameters | string  | no | harmonry      | yes |
| Touch ID Error  | Authentication failed  | string  | no | harmonry  | yes |
| Touch ID Error  | The operation is canceled   | string  | no | harmonry  | yes |
| Touch ID Error  | The operation is time-out | string  | no | harmonry  | yes |
| Touch ID Error  | The authentication type is not supported   | string | no | harmonry  | yes |
| Touch ID Error  | The authentication trust level is not supported | string  | no | harmonry      | yes |
| Touch ID Error  | The authentication task is busy | string  | no | harmonry      | yes |
| Touch ID Error  | The authenticator is locked  | string  | no | harmonry  | yes |
| Touch ID Error  | General operation error   | string  | no | harmonry  | no |
| Touch ID Error  | The authentication type is not supported | string  | no | harmonry  | yes |
| Touch ID Error  | The type of credential has not been enrolled   | string | no | harmonry  | yes |
| Touch ID Error  | The authentication is canceled from widget's navigation button   | string | no | harmonry  | yes |
| Touch ID Error  | Indicates that current authentication failed because of PIN expired   | string | no | harmonry  | yes |
## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/naoufal/react-native-touch-id?tab=readme-ov-file#license).
