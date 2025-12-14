Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-sensitive-info</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/mCodex/react-native-sensitive-info">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mCodex/react-native-sensitive-info/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-sensitive-info)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 6.0.0-alpha.9-0.0.3@deprecated | [@react-native-oh-tpl/react-native-sensitive-info Releases(deprecated)](https://github.com/react-native-oh-library/react-native-sensitive-info/releases) | 0.72                 |
| 6.0.1             | [@react-native-ohos/react-native-sensitive-info Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-sensitive-info/releases)   | 0.72       |
| 6.1.0             | [@react-native-ohos/react-native-sensitive-info Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-sensitive-info/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-sensitive-info
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-sensitive-info
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useCallback, useState } from "react";
import { Alert, Button, SafeAreaView, Text } from "react-native";
import SInfo from "react-native-sensitive-info";

const SensitiveInfoDemo = () => {
  const handleAddUsingSetItemOnPress = useCallback(() => {
    SInfo.setItem("key1", "value1", {
      sharedPreferencesName: "exampleApp",
      keychainService: "exampleApp",
    }).catch((err) => {
      Alert.alert("Error", err);
    });
  }, []);

  const handleReadingDataWithoutFingerprint = useCallback(async () => {
    try {
      const data = await SInfo.getItem("key1", {
        sharedPreferencesName: "exampleApp",
        keychainService: "exampleApp",
      });
      Alert.alert("Data stored:", data);
    } catch (err) {
      Alert.alert("Error", String(err));
    }
  }, []);

  const [logText, setLogText] = useState("");
  async function runTest() {
    const options = {
      sharedPreferencesName: "exampleAppTest",
      keychainService: "exampleAppTest",
    };
    let dbgText = "";
    dbgText += `setItem(key1, value1): ${await SInfo.setItem(
      "key1",
      "value1",
      options
    )}\n`;
    dbgText += `setItem(key2, value2): ${await SInfo.setItem(
      "key2",
      "value2",
      options
    )}\n`;
    dbgText += `setItem(key3, value3): ${await SInfo.setItem(
      "key3",
      "value3",
      options
    )}\n`;
    dbgText += `getItem(key2): ${await SInfo.getItem("key2", options)}\n`;
    dbgText += `delItem(key2): ${await SInfo.deleteItem("key2", options)}\n`;
    dbgText += `getAllItems():\n`;
    const allItems = await SInfo.getAllItems(options);
    for (const key in allItems) {
      dbgText += ` - ${key} : ${allItems[key]}\n`;
    }
    setLogText(dbgText);
  }
  runTest();

  return (
    <SafeAreaView style={{ margin: 10 }}>
      <Button
        title="Add item using setItem"
        onPress={handleAddUsingSetItemOnPress}
      />
      <Button
        title="Read data without fingerprint"
        onPress={handleReadingDataWithoutFingerprint}
      />
      <Text>{logText}</Text>
    </SafeAreaView>
  );
};
export default SensitiveInfoDemo;
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~6.1.0                               |  No                   |  0.77                |
| ~6.0.1                               |  Yes                  |  0.72                |
| <= 6.0.0-alpha.9-0.0.3@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md.

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

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
    "@react-native-ohos/react-native-sensitive-info": "file:../../node_modules/@react-native-ohos/react-native-sensitive-info/harmony/react_native_sensitive_info.har"
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

### 3. Configuring CMakeLists and Introducing RNSensitiveInfoPackage

> If you are using version <= 6.0.0-alpha.9-0.0.3, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-sensitive-info/src/main/cpp" ./react_native_sensitive_info)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_sensitive_info)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNSensitiveInfoPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNSensitiveInfoPackage>(ctx)
    };
}
```

### 4. Introducing RNSensitiveInfoPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...

+ import { RNSensitiveInfoPackage } from '@react-native-ohos/react-native-sensitive-info/ts';

@Builder
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNSensitiveInfoPackage(ctx)
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

在 YourProject/entry/src/main/module.json5 补上配置

```js
"requestPermissions": [ { "name": "ohos.permission.ACCESS_BIOMETRIC" }, ]
```

## API

[!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

[!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                  | Description                                                                                | Type     | Required | Platform     | HarmonyOS Support |
| ------------------------------------- | ------------------------------------------------------------------------------------------ | -------- | -------- | ------------ | ----------------- |
| isSensorAvailable()                   | Indicates the overall availability of fingerprint sensor. It will resolve to true or false | function | no       | Android、iOS | yes               |
| cancelFingerprintAuth ()              | Canceling fingerprint authentication                                                       | function | no       | Android、iOS | yes               |
| hasEnrolledFingerprints ()            | It will return true if detected otherwise returns false                                    | function | no       | Android、iOS | yes               |
| setItem()                             | Insert new data into the storage.                                                          | function | yes      | Android、iOS | yes               |
| getItem()                             | Get an item from storage                                                                   | function | yes      | Android、iOS | yes               |
| getAllItems()                         | Get all items from storage.                                                                | function | yes      | Android、iOS | yes               |
| deleteItem()                          | Delete an item from storage                                                                | function | yes      | Android、iOS | yes               |
| setInvalidatedByBiometricEnrollment() | Set invalid enrollment by biometrics                                                       | function | yes      | Android      | yes               |

#### **Options**

[!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

[!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | -------- | -------- | ------------ | ----------------- |
| kSecAccessControl | A secure storage area provided for storing sensitive information such as passwords, keys, etc | object | no | iOS | no |
| kSecAttrAccessible | Used to enhance data security | object | no | iOS | no |
| kSecAttrSynchronizable | Set when adding or querying Keychain data items | boolean | no | iOS | no |
| keychainService | A tool provided for securely storing sensitive information | string | no | iOS | no |
| sharedPreferencesName |The name parameter used to specify the file name | string | no | Android | yes |
| touchID | Unlock devices, verify identities, and make secure payments | boolean | no | Android、iOS | no |
| showModal | display a dialog box | boolean | no | iOS | no |
| kSecUseOperationPrompt | Use constants related to authentication | string | no | iOS | no |
| kLocalizedFallbackTitle | Handling biometric authentication attributes such as Touch ID and Face ID | string | no | iOS | no |
| strings | Android stores information | object | no | Android | no |

## Known Issues

## Others

由于 iOS 用的 Keychain 系统，kSecAccessControl、 kSecAttrAccessible、 kSecAttrSynchronizable、keychainService、showModal、kSecUseOperationPrompt、kLocalizedFallbackTitle 这些 Properties 是该系统独有，strings 里面的 header、description、hint、success、notRecognized、cancel、cancelled、这些是 Android 的 Keystore 系统所需要的，所以这里的 PropertiesHarmonyOS 不能统一支持

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mCodex/react-native-sensitive-info).
