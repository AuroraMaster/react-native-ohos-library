> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-get-random-values</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/LinusU/react-native-get-random-values">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/LinusU/react-native-get-random-values/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-get-random-values)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 1.11.0-0.0.1@deprecated      | [@react-native-oh-tpl/react-native-get-random-values Releases(deprecated)](https://github.com/react-native-oh-library/react-native-get-random-values/releases) | 0.72       |
| 1.11.1      | [@react-native-ohos/react-native-get-random-values Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-get-random-values/releases)                        | 0.72       |
| 1.12.0      | [@react-native-ohos/react-native-get-random-values Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-get-random-values/releases)                        | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-get-random-values
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-get-random-values
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { View, Text, StyleSheet, Button } from "react-native";
import "react-native-get-random-values";

export const GetRandomValues = () => {
  const [randomValue, setRandomValue] = useState < any > [];
  const styles = StyleSheet.create({
    container: {
      flex: 1,
      justifyContent: "center",
      alignItems: "center",
      backgroundColor: "#F5FCFF",
    },
  });

  const clickBtn = () => {
    const getRandomValues = global?.crypto?.getRandomValues(new Uint8Array(4));
    console.log(JSON.stringify(getRandomValues), "click");

    const array = Object.values(getRandomValues);
    console.log(array, "click");

    setRandomValue(array);
  };
  return (
    <View style={styles.container}>
      <Text style={{ fontSize: 20 }}> 点击获取随机数 </Text>
      <Button onPress={clickBtn} title="click" />
      {randomValue?.map((item: any, index: number) => {
        return <Text key={index}>{item}</Text>;
      })}
    </View>
  );
};
```

## Link

Version >= @react-native-ohos/react-native-get-random-values@1.11.1，已支持 Autolink，无需手动配置，目前只支持72框架。
Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-get-random-values": "file:../../node_modules/@react-native-ohos/react-native-get-random-values/harmony/get_random_values.har"
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

### 3.配置 CMakeLists 和引入 GetRandomValuesPackage

> 若使用的是 <= 1.11.0-0.0.1 版本，请跳过本章。

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-get-random-values/src/main/cpp" ./get_random_values)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_get_random_values)
# RNOH_END: manual_package_linking_2
```
打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "GetRandomValuesPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<GetRandomValuesPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNGetRandomValuesPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNGetRandomValuesPackage } from "@react-native-ohos/react-native-get-random-values/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNGetRandomValuesPackage(ctx)
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

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。
>
> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>
> | Name                          | Description                                          | Type    | Required | Platform    | HarmonyOS Support |
> | ----------------------------- | ---------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
> | global.crypto.getRandomValues | 允许你获取具有加密强度的随机值。 | funtion | no       | IOS/Android | yes               |

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/LinusU/react-native-get-random-values/blob/master/LICENSE) ，请自由地享受和参与开源。
