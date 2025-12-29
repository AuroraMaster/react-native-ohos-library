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

| Version                           | Release Information                        |Supported RN Version  |
|-----------------------------------|--------------------------------------------| -------------------- |
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
If an error occurs during compilation indicating that the source library needs to be imported, you can run the following command

```bash
npm install --force
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
      <Button title='check whether you have FaceID permission'
        onPress={() => {
          TouchID.isSupported({ unifiedErrors: false, useFaceID: true }).then((res: any) => {
            setResult(res);
          }).catch((err: any) => {
            setResult(err.message);
          });
        }}
      ></Button>
      <Button title='check FaceID'
        onPress={() => {
          TouchID.authenticate(undefined, { useFaceID: true }).then(() => {
            setResult('Authentication successful')
          }).catch((err: any) => {
            setResult(err.message);
          });
        }}
      ></Button>
    </View>
  )
};

export default App;

```
## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | is supporte autolink  | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~4.5.0                               |  No                   |  0.77                |
| ~4.4.2                               |  Yes                  |  0.72                |
| <= 4.4.1-0.0.3@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

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
</details>

## Running

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
## API Parameters Introduction
### authenticate(reason?: string, config?: AuthenticateConfig);
* **reason**: A string providing a clear reason for requesting authentication
* **config**: A configuration object for more detailed dialog settings
  * **AuthenticateConfig**:
	| Name | Description | Type | Required | Platform | HarmonyOS Support  |
	| ---- | ----------- | ---- | -------- | -------- | ------------------ |
	| title  | **Android only** - Title of the confirmation dialog | string  | no | ios/android      | yes |
	| imageColor  | **Android only** - Color of the fingerprint image | string  | no | ios/android      | no |
	| imageErrorColor  | **Android only** - Color of the fingerprint image after a failed attempt | string  | no | ios/android      | no |
	| sensorDescription  | **Android only** - Text displayed next to the fingerprint image | string  | no | ios/android      | no |
	| sensorErrorDescription  | **Android only** - Text displayed next to the fingerprint image after a failed attempt | string  | no | ios/android      | no |
	| cancelText  | **Android only** - Cancel button text | string  | no | ios/android      | yes |
	| fallbackLabel  | **iOS only** - By default shows "Show Password" label. If set to empty string, the label will be invisible | string  | no | ios/android      | no |
	| passcodeFallback  | **iOS only** - Defaults to false. If set to true, will allow fallback to passcode | boolean  | no | ios/android      | no |
    | unifiedErrors| Returns unified error messages | boolean | no | ios/android      | yes |
    | useFaceID | Whether to use faceID. Default is false, fingerprint will be used. If set to true, faceID will be used. | boolean | no | no      | yes |
### isSupported(config?: IsSupportedConfig): `Promise<BiometryType>`;
* **config** - Returns a `Promise` that rejects if TouchID is not supported. On iOS, resolves to a `biometryType` string with value `FaceID` or `TouchID`
 * **IsSupportedConfig**:
 	| Name | Description | Type | Required | Platform | HarmonyOS Support  |
	| ---- | ----------- | ---- | -------- | -------- | ------------------ |
    | unifiedErrors| Returns unified error messages | boolean | no | ios/android      | yes |
    | useFaceID | Whether to use faceID. Default is false, fingerprint will be used. If set to true, faceID will be used. | boolean | no | no      | yes |
## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### Errors

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| 201  | Permission verification failed | string  | no | harmonry      | yes |
| 401  | Incorrect parameters | string  | no | harmonry      | no |
| 12500001  | Authentication failed  | string  | no | harmonry  | yes |
| 12500002  | General operation error   | string  | no | harmonry  | no |
| 12500003  | The operation is canceled   | string  | no | harmonry  | yes |
| 12500004  | The operation is time-out | string  | no | harmonry  | no |
| 12500005  | The authentication type is not supported   | string | no | harmonry  | no |
| 12500006  | The authentication trust level is not supported | string  | no | harmonry      | no |
| 12500007  | The authentication task is busy | string  | no | harmonry      | no |
| 12500009  | The authenticator is locked  | string  | no | harmonry  | yes |
| 12500010  | The type of credential has not been enrolled   | string | no | harmonry  | yes |
| 12500011  | The authentication is canceled from widget's navigation button   | string | no | harmonry  | yes |
| 12500013  | Indicates that current authentication failed because of PIN expired   | string | no | harmonry  | no |

## Known Issues

- [ ] The config parameter is partially supported.[issue#13](https://github.com/react-native-oh-library/react-native-touch-id/issues/13)
- [ ] Error is partially supported.[issue#12](https://gitcode.com/openharmony-sig/rntpc_react-native-touch-id/issues/12)

## Others

- ios/android does not support the `useFaceID` parameter, which is only applicable to the HarmonyOS platform and is used to control whether the facial recognition feature is enabled.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/naoufal/react-native-touch-id?tab=readme-ov-file#license).
