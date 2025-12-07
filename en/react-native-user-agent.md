> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-user-agent</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/bebnev/react-native-user-agent">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bebnev/react-native-user-agent/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-user-agent)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <=2.3.1-0.0.1@deprecated | [@react-native-oh-tpl/react-native-user-agent Releases(deprecated)](https://github.com/react-native-oh-library/react-native-user-agent/releases) | 0.72       |
| 2.3.2             | [@react-native-ohos/react-native-user-agent Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-user-agent/releases)   | 0.72       |
| 2.4.0             | [@react-native-ohos/react-native-user-agent Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-user-agent/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-user-agent
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-user-agent
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useEffect } from 'react';
import { View, Text } from 'react-native';
import UserAgent from 'react-native-user-agent';

// sync method:
let userAgent: string = UserAgent.getUserAgent();

export default function UserAgentExample() {
  const [webViewUserAgent, setWebViewUserAgent] = useState<string | null>(null);
  useEffect(() => {
    // async method:
    UserAgent.getWebViewUserAgent()
      .then(webViewUserAgent => {
        setWebViewUserAgent(webViewUserAgent);
        console.log(webViewUserAgent);
      })
      .catch(e => {
        console.error('Error getting WebView User Agent:', e);
      });
  }, []);
  return (
    <View>
      <Text>Sync method:</Text>
      <Text>{userAgent}</Text>

      <Text>Async method</Text>
      <Text>{webViewUserAgent}</Text>

      <Text>Property: </Text>
      <Text>systemName: {UserAgent.systemName}</Text>
      <Text>systemVersion: {UserAgent.systemVersion}</Text>
      <Text>applicationName: {UserAgent.applicationName}</Text>
      <Text>applicationVersion: {UserAgent.applicationVersion}</Text>
      <Text>buildNumber: {UserAgent.buildNumber}</Text>
    </View>
  );
};

```

## Use Codegen

Version >= @react-native-ohos/react-native-user-agent@2.3.2, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to Codegen, generate the bridge code of the third-party library by using the Codegen. For details, see[ Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-user-agent@2.3.2 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

Open the harmony directory of the HarmonyOS project in DevEco Studio.

### 1.Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony": "./react_native_openharmony"
  }
}
```

### 2.Introducing Native Code

Currently, two methods are available:

1.  (recommended): Use the HAR file.
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-user-agent": "file:../../node_modules/@react-native-ohos/react-native-user-agent/harmony/user_agent.har"
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

### 3.Configuring CMakeLists and introducing UserAgent

> If you are using version <=2.3.1-0.0.1, please skip this chapter.

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
+ set(USER_AGENT_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules/@react-native-ohos/react-native-user-agent/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

# (VM) Define a variable and assign it to the current module's cpp directory
set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})

# Add the Header File directory, including cpp, cpp/include, and tell cmake to find the Header Files introduced by the code here
include_directories(${NATIVERENDER_ROOT_PATH}
                    ${NATIVERENDER_ROOT_PATH}/include)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)
+ add_subdirectory("${USER_AGENT_CPP_DIR}" ./user_agent)


add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)
+ target_link_libraries(rnoh_app PUBLIC user_agent)
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```diff
#include "RNOH/PackageProvider.h"
+#include "generated/UserAgentPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx)
{
    return {
+        std::make_shared<UserAgentPackage>(ctx),        
    };
}
```

### 4.Introducing RNUserAgentPackage to ArkTs

Open `entry/src/main/ets/RNPackagesFactory.ts` and add:

```diff
  ...
  
+  import { RNUserAgentPackage } from '@react-native-ohos/react-native-user-agent/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new RNUserAgentPackage(ctx)
  ];
}
```

### 5.Running

Click the sync button in the upper right corner.

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

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## Properties

> [!tip] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description         | Type   | Required | Platform | HarmonyOS Support |
| ------------------ | ------------------- | ------ | -------- | -------- | ----------------- |
| systemName         | System Name         | string | no       | All      | yes               |
| systemVersion      | System Version      | string | no       | All      | yes               |
| applicationName    | Application Name    | string | no       | All      | yes               |
| applicationVersion | Application Version | string | no       | All      | yes               |
| buildNumber        | Build Number        | string | no       | All      | yes               |
| darwinVersion      | Darwin Version      | string | no       | iOS      | no                |
| cfnetworkVersion   | Cfnetwork Version   | string | no       | iOS      | no                |
| modelName          | Model Name          | string | no       | iOS      | no                |
| deviceName         | Device Name         | string | no       | iOS      | no                |

## API

> [!tip] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                | Description                   | Type    | Required | Platform | HarmonyOS Support |
| ------------------- | ----------------------------- | ------- | -------- | -------- | ----------------- |
| getUserAgent        | Get user agent synchronously  | string  | no       | All      | yes               |
| getWebViewUserAgent | Get user agent asynchronously | Promise | no       | All      | yes               |

## Known Issues

## Others

Depending on HarmonyOS NEXT Developer Beta3 version default UserAgent definition, word ArkWeb VersionCode (ArkWeb version number) has no receive method currently, waiting for completion afterwards.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/bebnev/react-native-user-agent/blob/master/LICENSE).
