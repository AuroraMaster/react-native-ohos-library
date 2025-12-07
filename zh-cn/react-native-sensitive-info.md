模板版本：v0.2.2

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


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-sensitive-info)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                  | 支持RN版本 |
|--------| ------------------------------------------------------------ | ---------- |
| <= 6.0.0-alpha.9-0.0.3@deprecated | [@react-native-oh-tpl/react-native-sensitive-info Releases(deprecated)](https://github.com/react-native-oh-library/react-native-sensitive-info/releases) | 0.72         |
| 6.0.1             | [@react-native-ohos/react-native-sensitive-info Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-sensitive-info/releases)   | 0.72       |
| 6.1.0             | [@react-native-ohos/react-native-sensitive-info Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-sensitive-info/releases)   | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useCallback, useState } from 'react';
import { Alert, Button, SafeAreaView, Text } from 'react-native';
import SInfo from 'react-native-sensitive-info';

const SensitiveInfoDemo = () => {
  const handleAddUsingSetItemOnPress = useCallback(() => {
    SInfo.setItem('key1', 'value1', {
      sharedPreferencesName: 'exampleApp',
      keychainService: 'exampleApp',
    }).catch((err) => {
      Alert.alert('Error', err);
    });
  }, []);

  const handleReadingDataWithoutFingerprint = useCallback(async () => {
    try {
      const data = await SInfo.getItem('key1', {
        sharedPreferencesName: 'exampleApp',
        keychainService: 'exampleApp',
      });
      Alert.alert('Data stored:', data);
    } catch (err) {
      Alert.alert('Error', String(err));
    }
  }, []);


  const [logText, setLogText] = useState('');
  async function runTest() {
    const options = {
      sharedPreferencesName: 'exampleAppTest',
      keychainService: 'exampleAppTest',
    };
    let dbgText = '';
    dbgText += `setItem(key1, value1): ${await SInfo.setItem(
      'key1',
      'value1',
      options,
    )}\n`;
    dbgText += `setItem(key2, value2): ${await SInfo.setItem(
      'key2',
      'value2',
      options,
    )}\n`;
    dbgText += `setItem(key3, value3): ${await SInfo.setItem(
      'key3',
      'value3',
      options,
    )}\n`;
    dbgText += `getItem(key2): ${await SInfo.getItem('key2', options)}\n`;
    dbgText += `delItem(key2): ${await SInfo.deleteItem('key2', options)}\n`;
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

## 使用 Codegen

Version >= @react-native-ohos/react-native-sensitive-info@6.0.1，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-sensitive-info@6.0.1，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-sensitive-info": "file:../../node_modules/@react-native-ohos/react-native-sensitive-info/harmony/react_native_sensitive_info.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码


> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.配置 CMakeLists 和引入 RNSensitiveInfoPackage

> 若使用的是 <= 6.0.0-alpha.9-0.0.3 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

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

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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

### 4.在 ArkTs 侧引入 RNSensitiveInfoPackage

打开 entry/src/main/ets/组件RNPackagesFactory.ts，添加：

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

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。



## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### 权限要求
在  YourProject/entry/src/main/module.json5补上配置
```js
"requestPermissions": [ { "name": "ohos.permission.ACCESS_BIOMETRIC" }, ]
```

## API
[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name        |    Description              | Type     | Required | Platform     | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | -------- | -------- | ------------ | ----------------- |
| isSensorAvailable()    |  Indicates the overall availability of fingerprint sensor. It will resolve to true or false   |  function | no      | Android、iOS | yes               |
| cancelFingerprintAuth ()                   | Canceling fingerprint authentication  | function | no      | Android、iOS | yes               |
| hasEnrolledFingerprints ()         | It will return true if detected otherwise returns false  | function | no      | Android、iOS | yes               |
| setItem() | Insert new data into the storage. |  function | yes      | Android、iOS | yes               |
| getItem() | Get an item from storage |  function | yes      | Android、iOS | yes               |
| getAllItems() | Get all items from storage. |  function | yes      | Android、iOS | yes               |
| deleteItem() | Delete an item from storage |  function | yes      | Android、iOS | yes               |
| setInvalidatedByBiometricEnrollment() | Set invalid enrollment by biometrics |  function | yes      | Android | yes               |


#### **Options**
[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
| Name        |    Description              | Type     | Required | Platform     | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | -------- | -------- | ------------ | ----------------- |
| kSecAccessControl | A secure storage area provided for storing sensitive information such as passwords, keys, etc |  object    | no      | iOS | no               |
| kSecAttrAccessible | Used to enhance data security |  object    | no      | iOS | no               |
| kSecAttrSynchronizable | Set when adding or querying Keychain data items |  boolean | no      |    iOS | no               |
| keychainService | A tool provided for securely storing sensitive information |  string | no      | iOS | no               |
| sharedPreferencesName |The name parameter used to specify the file name |  string | no      | Android | yes               |
| touchID | Unlock devices, verify identities, and make secure payments |  boolean | no      | Android、iOS | no               |
| showModal | display a dialog box |  boolean | no      | iOS | no               |
| kSecUseOperationPrompt | Use constants related to authentication |  string | no      | iOS | no               |
| kLocalizedFallbackTitle | Handling biometric authentication attributes such as Touch ID and Face ID |  string | no      | iOS | no               |
| strings | Android stores information |  object            | no      | Android | no               |


## 遗留问题


## 其他
由于iOS用的Keychain系统，kSecAccessControl、 kSecAttrAccessible、 kSecAttrSynchronizable、keychainService、showModal、kSecUseOperationPrompt、kLocalizedFallbackTitle 这些属性是该系统独有，strings里面的header、description、hint、success、notRecognized、cancel、cancelled、这些是Android的Keystore系统所需要的，所以这里的属性HarmonyOS不能统一支持

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mCodex/react-native-sensitive-info) ，请自由地享受和参与开源。

