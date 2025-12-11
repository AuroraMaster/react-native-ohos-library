> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-haptic-feedback</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/mkuczera/react-native-haptic-feedback">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mkuczera/react-native-haptic-feedback/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-haptic-feedback)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <=2.2.1@deprecated  | [@react-native-oh-tpl/react-native-haptic-feedback Releases(deprecated)](https://github.com/react-native-oh-library/react-native-haptic-feedback/releases) | 0.72       |
| 2.2.2      | [@react-native-ohos/react-native-haptic-feedback Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-haptic-feedback/releases)    | 0.72       |
| 2.3.4      | [@react-native-ohos/react-native-haptic-feedback Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-haptic-feedback/releases)    | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install @react-native-ohos/react-native-haptic-feedback
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-haptic-feedback
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react"
import { SafeAreaView, ScrollView, Button } from "react-native"
import ReactNativeHapticFeedback from "react-native-haptic-feedback"
const options = {
  enableVibrateFallback: false,
  ignoreAndroidSystemSettings: false,
}

const methods: Array<
  | "impactLight"
  | "impactMedium"
  | "impactHeavy"
  | "notificationSuccess"
  | "notificationWarning"
  | "notificationError"
  | "rigid"
  | "soft"
  | "selection"
  | "clockTick"
  | "contextClick"
  | "keyboardPress"
  | "keyboardRelease"
  | "keyboardTap"
  | "longPress"
  | "textHandleMove"
  | "virtualKey"
  | "virtualKeyRelease"
  | "effectClick"
  | "effectDoubleClick"
  | "effectHeavyClick"
  | "effectTick"
> = [
  "impactLight",
  "impactMedium",
  "impactHeavy",
  "notificationSuccess",
  "notificationWarning",
  "notificationError",
  "rigid",
  "soft",
  "selection",
  "clockTick",
  "contextClick",
  "keyboardPress",
  "keyboardRelease",
  "keyboardTap",
  "longPress",
  "textHandleMove",
  "virtualKey",
  "virtualKeyRelease",
  "effectClick",
  "effectDoubleClick",
  "effectHeavyClick",
  "effectTick",
]

export const HapticFeedbackExample = () => {
  return (
    <SafeAreaView>
      <ScrollView>
        {methods.map((item) => {
          return (
            <Button
              title={item}
              onPress={() => ReactNativeHapticFeedback.trigger(item, options)}
              key={item}
            ></Button>
          )
        })}
      </ScrollView>
    </SafeAreaView>
  )
}

export default HapticFeedbackExample;
```

## 使用 Codegen

Version >= @react-native-ohos/react-native-haptic-feedback@2.2.2，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-haptic-feedback@2.2.2，已支持 Autolink，无需手动配置，目前只支持72框架。
Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
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
    "@react-native-ohos/react-native-haptic-feedback": "file:../../node_modules/@react-native-ohos/react-native-haptic-feedback/harmony/haptic_feedback.har"
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

### 3.配置 CMakeLists 和引入 RNHapticFeedbackPackage

> 若使用的是 <= 2.2.1 版本，请跳过本章。

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-haptic-feedback/src/main/cpp" ./haptic-feedback)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_haptic_feedback)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNHapticFeedbackPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<RNHapticFeedbackPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 RNHapticFeedbackPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+  import { RNHapticFeedbackPackage } from '@react-native-ohos/react-native-haptic-feedback/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNHapticFeedbackPackage(ctx)
  ]
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

#### 在 entry 目录下的module.json5中添加权限

在 entry/src/main/module.json5补上配置
```js
"requestPermissions": [ { "name": "ohos.permission.VIBRATE" }, ]
```

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该方法；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Available Methods

`trigger(method, options)`
Use this method to trigger haptic feedback

| Name                                  | Description                                                  | Type                             | Required | Platform    | HarmonyOS Support |
| ------------------------------------- | ------------------------------------------------------------ | -------------------------------- | -------- | ----------- | ----------------- |
| `method`                              | Specifies the type of haptic feedback. See the list of available methods below. | keyof typeof HapticFeedbackTypes | yes      | iOS/Android | yes               |
| `options.enableVibrateFallback`       | iOS only. If haptic feedback is unavailable (iOS < 10 OR Device < iPhone6s), vibrate with default method (heavy 1s) (default: false). | boolean                          | no       | iOS         | no                |
| `options.ignoreAndroidSystemSettings` | Ignoreing phone mute mode setting and triggering haptic feedback. (default: false). | boolean                          | no       | Android     | yes               |

### method Overview

Here's an overview of the available methods and their compatibility

##### HapticFeedbackTypes

| Name | Description | Type |Required|Platform|HarmonyOS Support|
| ---- | :-----: | :----: |:---: |:----: |:------: |
| `impactLight` | impactLight feedback | string |no|iOS/Android|yes|
| `impactMedium` | impactMedium feedback | string |no|iOS/Android|yes|
| `impactHeavy` | impactHeavy feedback | string |no|iOS/Android|yes|
| `rigid` | rigid feedback | string |no|iOS/Android|yes|
| `soft` | soft feedback | string |no|iOS/Android|yes|
| `notificationSuccess` | notificationSuccess feedback | string |no|iOS/Android|yes|
| `notificationWarning` | notificationWarning feedback | string |no|iOS/Android|yes|
| `notificationError` | notificationError feedback | string |no|iOS/Android|yes|
| `selection` | selection feedback | string |no|iOS|yes|
| `clockTick` | clockTick feedback | string |no|Android|yes|
| `contextClick` | contextClick feedback | string |no|Android|yes|
| `keyboardPress` | keyboardPress feedback | string |no|Android|yes|
| `keyboardRelease` | keyboardRelease feedback | string |no|Android|yes|
| `keyboardTap` | keyboardTap feedback | string |no|Android|yes|
| `longPress` | longPress feedback | string |no|Android|yes|
| `textHandleMove` | textHandleMove feedback | string |no|Android|yes|
| `virtualKey` | virtualKey feedback | string |no|Android|yes|
| `virtualKeyRelease` | virtualKeyRelease feedback | string |no|Android|yes|
| `effectClick` | effectClick feedback | string |no|Android|yes|
| `effectDoubleClick` | effectDoubleClick feedback | string |no|Android|yes|
| `effectHeavyClick` | effectHeavyClick feedback | string |no|Android|yes|
| `effectTick` | effectTick feedback | string |no|Android|yes|

## 遗留问题

- [ ] 自定义振动文件配置问题: [issue#6](https://github.com/react-native-oh-library/react-native-haptic-feedback/issues/6)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mkuczera/react-native-haptic-feedback/blob/master/LICENSE) ，请自由地享受和参与开源。
