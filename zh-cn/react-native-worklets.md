> 模板版本：v0.4.0

<p align="center">
  <h1 align="center"> <code>react-native-worklets</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-reanimated/tree/main/packages/react-native-worklets">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/software-mansion/react-native-reanimated/blob/main/packages/react-native-worklets/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

本项目基于原库 [react-native-worklets@0.7.1](https://github.com/software-mansion/react-native-reanimated/tree/worklets-0.7.1/packages/react-native-worklets) 开发。

该三方库支持直接从 npm 下载,其包名：@react-native-ohos/react-native-worklets

|三方库名称| 三方库版本                 | 发布信息                                      |  支持RN版本                 |Autolink| 编译API版本|社区基线版本|npm地址|
|---------| ------------------------- | ------------------------------------------------- |  -------------------------- | ---| ---|----|----|
|@react-native-ohos/react-native-worklets | ~1.0.0                | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-reanimated/tree/br_rnoh0.82/package/react-native-worklets)  | 0.82.* | 否|API12+|0.7.1|[Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-worklets)|
## 1. 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm intstall react-native-worklets@0.7.1
npm install @react-native-ohos/react-native-worklets
```

#### **yarn**

```bash
yarn add react-native-worklets@0.7.1
yarn add @react-native-ohos/react-native-worklets
```

<!-- tabs:end -->

#### 插件配置

添加react-native-worklets/plugin插件到 `babel.config.js`:

> [!TIP] 为什么需要添加这个？Babel 插件会自动转换特殊的 JavaScript 函数（称为 worklet），以便它们可以被传递并在 UI 线程上运行。

```js
  module.exports = {
    presets: [
      ... // don't add it here :)
    ],
    plugins: [
      ...
      'react-native-worklets/plugin',
    ],
  };
```

清除 Metro 的缓存（推荐）:

<!-- tabs:start -->

#### **npm**

```bash
npm start --reset-cache
```

#### **yarn**

```bash
yarn start --reset-cache
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { runOnUIAsync} from 'react-native-worklets';
  
import React, { useState } from 'react';
import { Platform, StyleSheet, Text, View,Button } from 'react-native';

export default function RunOnUIAsync() {
const [textResult,setTextResult] = useState<string>("")

const result: Promise<string> = runOnUIAsync((): string => {
  return "runOnUIAsync";
});

 return (
    <View style={styles.container}>
        
        <Text>runOnUIAsync:{textResult}</Text>

        <Button
           title="run"
                onPress={async() => {
                  let str =  await result
                  setTextResult(JSON.stringify(str))
                }}
         />
    </View>
  );
}

  const styles = StyleSheet.create({
    container: {
      flex: 1,
      padding: 20,
      backgroundColor:"white"
    },
    text: {
      fontSize: 16,
      marginVertical: 4,
    },
    bold: {
      fontWeight: 'bold',
    },
  });
```

## 2. Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~1.0.0                                |  No              |  0.82     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 2.1. Overrides RN SDK
为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 oh-package.json5 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读官方说明
```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony",
  }
}
```

### 2.2 引入原生端代码

目前有两种方法：

- 通过 har 包引入；
- 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-worklets": "file:../../node_modules/@react-native-ohos/react-native-worklets/harmony/worklets.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 2.3. 配置 CMakeLists 和引入 ReanimatedWorkletPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-worklets/src/main/cpp" ./worklets)

# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_worklets)

# RNOH_BEGIN: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ReanimatedWorkletPackage.h"
using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ReanimatedWorkletPackage>(ctx)
    };
}
```

### 2.4. 在 ArkTs 侧引入 ReanimatedWorkletPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { ReanimatedWorkletPackage } from '@react-native-ohos/react-native-worklets'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ReanimatedWorkletPackage(ctx),
  ];
}
```

</details>

### 2.5. 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1.兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.82.7;  SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1.260; ROM: 6.0.0.130 SP15;

## 4. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                                                                                                                                                                                                                | Type     | Required | Platform | HarmonyOS Support |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |----------| -------- | -------- | ----------------- |
| `createWorkletRuntime`       | lets you create a new JS runtime which can be used to run worklets possibly on different threads than JS or UI thread. | function | No       | All      | yes               |
| `runOnUIAsync`       | lets you asynchronously run workletized functions on the UI thread. | function | No       | All      | yes               |
| `runOnUISync`        | lets you run a workletized function synchronously on the UI Runtime.| function | No       | All      | yes               |
| `scheduleOnRN`       | lets you schedule a function to be executed on the RN Runtime from any Worklet Runtime.| function | No       | All      | yes               |
| `scheduleOnRuntime`   | lets you schedule a worklet to be executed on a Worker Runtime.| function | No       | All      | yes               |
| `scheduleOnUI` | ulets you schedule a function to be executed on the UI Runtime.| function | No       | All      | yes               |
| `createSerializable` | recursively converts JavaScript values into Serializable references that can be passed to different JavaScript Runtimes. | function | No       | All      | yes               |
| `createSynchronizable ` | creates a new Synchronizable holding the provided initial value. Returns the created Synchronizable. | function | No       | All      | yes               |
| `isSerializableRef ` | asserts whether a value is a Serializable reference. | function | No       | All      | yes|
| `isSynchronizable ` | asserts whether a value is a Synchronizable. | function | No       | All      | yes               |
| `registerCustomSerializable  ` | lets you register your own pre-serialization and post-deserialization logic. | function | No       | All      | yes               |
| `getRuntimeKind` | allows you to get the kind of the current runtime.  | function | No       | All      | yes               |
| `isWorkletFunction` |  checks if a function is a worklet function.  | function | No       | All      | yes               |
| `getStaticFeatureFlag` | A function for obtaining static functionality flags (feature flags)                | function  | no       | All      | yes               |

## 5. 其他

## 6. 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/software-mansion/react-native-reanimated/blob/main/packages/react-native-worklets/LICENSE) ，请自由地享受和参与开源。
