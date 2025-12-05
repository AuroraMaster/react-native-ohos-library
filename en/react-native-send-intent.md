> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-send-intent</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lucasferreira/react-native-send-intent">
        <img src="https://img.shields.io/badge/platforms-android%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/lucasferreira/react-native-send-intent?tab=readme-ov-file#license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-send-intent)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.3.0@deprecated  | [@react-native-oh-tpl/react-native-send-intent Releases(deprecated)](https://github.com/react-native-oh-library/react-native-send-intent/releases) | 0.72       |
| 1.3.1             | [@react-native-ohos/react-native-send-intent Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-send-intent/releases)   | 0.72       |
| 1.4.0             | [@react-native-ohos/react-native-send-intent Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-send-intent/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/react-native-send-intent
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-send-intent
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useState, useEffect } from "react";
import { Button, Text } from "react-native";
import NativeSendIntent from "react-native-send-intent";

function SendIntent() {
  return (
    <>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.sendPhoneDial</Text>
        <Button
          onPress={() => {
            NativeSendIntent.sendPhoneDial("10086", false);
          }}
          title=""
          color="#841584"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.sendSms</Text>
        <Button
          onPress={() => {
            NativeSendIntent.sendSms("100010", "text SMS");
          }}
          title=""
          color="#DC143C"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.openCalendar</Text>
        <Button
          onPress={() => {
            NativeSendIntent.openCalendar();
          }}
          title=""
          color="#D2691E"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.sendMail</Text>
        <Button
          onPress={() => {
            NativeSendIntent.sendMail(
              "mailto:someone@example.com",
              "This%20is%20the%20subject",
              "This%20is%20the%20body"
            );
          }}
          title=""
          color="#B8860B"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.openMaps</Text>
        <Button
          onPress={() => {
            NativeSendIntent.openMaps("Wuchang Railway Station");
          }}
          title=""
          color="#FF0000"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.openCamera</Text>
        <Button
          onPress={() => {
            NativeSendIntent.openCamera();
          }}
          title=""
          color="#FF1493"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.openSettings</Text>
        <Button
          onPress={() => {
            NativeSendIntent.openSettings("bluetooth_entry");
          }}
          title=""
          color="#8B4513"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.gotoHomeScreen</Text>
        <Button
          onPress={() => {
            NativeSendIntent.gotoHomeScreen();
          }}
          title=""
          color="#006400"
        />
      </>
    </>
  );
}
export default SendIntent;
```

## Use Codegen

Version >= @react-native-ohos/react-native-send-intent@1.3.1, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >=@react-native-ohos/react-native-send-intent@1.3.1 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
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
    "@react-native-ohos/react-native-send-intent": "file:../../node_modules/@react-native-ohos/react-native-send-intent/harmony/send_intent.har"
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

### 3.Configure CMakeLists and introduce SendIntentPackage

> V1.3.1 requires configuring CMakeLists and importing SendIntentPackage.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-send-intent/src/main/cpp" ./send_intent)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_send_intent)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SendIntentPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<SendIntentPackage>(ctx),
    };
}
```

### 4. Introducing RNSendIntentPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {RNSendIntentPackage} from '@react-native-ohos/react-native-send-intent/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+    new RNSendIntentPackage(ctx)
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

To use this library, you need to use the correct React-Native and RNOH versions. Additionally, you need to use the matching DevEco Studio and phone ROM.

Verified successfully in the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 5.1.0.150 (API Version 12); IDE: DevEco Studio 5.1.1.830; ROM: 5.1.0.150;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 5.0.0.71(API Version 12 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 5.1.0.150;

## API

| Name                                   | Description                                            | Type     | Required | Platform | HarmonyOS Support |
| -------------------------------------- | ------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| sendText                               | Usage of Text (Share)                                  | Function | no       | Android  | yes               |
| sendMail                               | Usage of Send Mail (text/plain only)                   | Function | no       | Android  | yes               |
| sendSms                                | Usage of SMS                                           | Function | no       | Android  | yes               |
| sendPhoneCall                          | Usage of Phone Dial Screen                             | Function | no       | Android  | yes               |
| sendPhoneDial                          | sage of Phone Dial Screen                              | Function | no       | Android  | yes               |
| addCalendarEvent                       | Create Calendar Event                                  | Function | no       | Android  | no                |
| isAppInstalled                         | Check if an application is installed                   | Function | no       | Android  | no                |
| installRemoteApp                       | Install a remote APK                                   | Function | no       | Android  | no                |
| openApp                                | Open App                                               | Function | no       | Android  | yes               |
| openAppWithData                        | Open App with Data                                     | Function | no       | Android  | no                |
| openChromeIntent                       | browser opened                                         | Function | no       | Android  | yes               |
| openCalendar                           | Open Camera Intent                                     | Function | no       | Android  | yes               |
| openCamera                             | Open Camera                                            | Function | no       | Android  | yes               |
| openEmailApp                           | Open Email Application                                 | Function | no       | Android  | yes               |
| openAllEmailApp                        | Will open all the Email app's that available in device | Function | no       | Android  | yes               |
| openDownloadManager                    | Open Download Manager                                  | Function | no       | Android  | yes               |
| openChooserWithOptions                 | Open Share With dialog                                 | Function | no       | Android  | yes               |
| openChooserWithMultipleOptions         | Open Multiple Files Share With dialog                  | Function | no       | Android  | yes               |
| openMaps                               | Open Maps                                              | Function | no       | Android  | yes               |
| openMapsWithRoute                      | Open Maps With Route                                   | Function | no       | Android  | yes               |
| shareTextToLine                        | Share text to line                                     | Function | no       | Android  | no                |
| shareImageToInstagram                  | Share Image to Instagram                               | Function | no       | Android  | no                |
| openSettings                           | Open Settings                                          | Function | no       | Android  | yes               |
| getVoiceMailNumber                     | Get voiceMail number                                   | Function | no       | Android  | no                |
| openFileChooser                        | Open File Chooser                                      | Function | no       | Android  | yes               |
| openFilePicker                         | Opens Android own file selector callback path from     | Function | no       | Android  | yes               |
| getPhoneNumber                         | Get phone number                                       | Function | no       | Android  | no                |
| requestIgnoreBatteryOptimizations      | Request 'ignore battery optimizations'                 | Function | no       | Android  | no                |
| showIgnoreBatteryOptimizationsSettings | Show battery optimizations settings                    | Function | no       | Android  | no                |
| gotoHomeScreen                         | Jump to main screen                                    | Function | no       | Android  | yes               |
| openAppWithUri                         | Open the app and go to the app store                   | Function | no       | Android  | yes               |

## Known Issues

- [ ] react-native-send-intent 部分方法未实现 HarmonyOS 化 [issue#2](https://github.com/react-native-oh-library/react-native-send-intent/issues/2)

## Others

- installRemoteApp(); 不支持通过一个链接下载一个包，进行安装，只能通过应用市场
- shareTextToLine(); 共享的应用 android 源码为海外应用,无法打开
- shareImageToInstagram(); Instagram 为海外应用,无法打开
- getVoiceMailNumber(); ICCID 和号码信息为敏感数据，不开放(https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-sim-V5)
- getPhoneNumber(); ICCID 和号码信息为敏感数据，不开放(https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-sim-V5)

## License

This project is licensed under [The MIT License (MIT)](https://github.com/lucasferreira/react-native-send-intent?tab=readme-ov-file#license).
