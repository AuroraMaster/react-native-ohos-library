> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-safe-area-context</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/th3rdwave/react-native-safe-area-context">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20web%20%7C%20macos%20%7C%20windows%20%7C%20harmony-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/th3rdwave/react-native-safe-area-context/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-safe-area-context)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 社区版本                                                                                                                                     | 发布信息                                                                                                                                            | 支持RN版本 |
|-------|-------------------------------------------------------------------------------------------------------------------------------------------------| ---------- | ---------- |
| 5.6.3                     | 5.6.2                     | [@react-native-ohos/react-native-safe-area-context Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-safe-area-context/releases) | 0.82       |
| 5.1.1                     | 5.1.0                     | [@react-native-ohos/react-native-safe-area-context Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-safe-area-context/releases) | 0.77       |
| 4.7.5                     | 4.7.4                     | [@react-native-ohos/react-native-safe-area-context Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-safe-area-context/releases) | 0.72       |
| <= 4.7.4-0.2.1@deprecated | 4.7.4 | [@react-native-oh-tpl/react-native-safe-area-context Releases(deprecated)](https://github.com/react-native-oh-library/react-native-safe-area-context/releases) | 0.72 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-safe-area-context
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-safe-area-context
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { Text, View } from "react-native";
import {
  SafeAreaProvider,
  SafeAreaView,
  initialWindowMetrics,
} from "react-native-safe-area-context";

const App = () => {
  return (
    <SafeAreaProvider initialMetrics={initialWindowMetrics}>
      <SafeAreaView style={{ flex: 1, backgroundColor: "red" }}>
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
          <Text>hello</Text>
        </View>
      </SafeAreaView>
    </SafeAreaProvider>
  );
};

export default App;
```

## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~5.6.3 | No | 0.82 |
| ~5.1.1                               |  No              |  0.77     |
| ~4.7.5                              |  Yes             |  0.72     |
| <= 4.7.4-0.2.1@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

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

    "@react-native-ohos/react-native-safe-area-context": "file:../../node_modules/@react-native-ohos/react-native-safe-area-context/harmony/safe_area.har"
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

### 3.配置 CMakeLists 和引入 SafeAreaViewPackage

> 若使用的是 <= 4.7.4-0.2.1 版本，请跳过本章

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

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-safe-area-context/src/main/cpp" ./safe-area)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_safe_area)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SafeAreaViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<SafeAreaViewPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 SafeAreaViewPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {SafeAreaViewPackage} from '@react-native-ohos/react-native-safe-area-context/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SafeAreaViewPackage(ctx)
  ];
}
```

</details>

## 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

> [!TIP] version>=4.7.4-0.2.1的版本需要在DevEco Studio 5.0.2(API14) 及以上版本编译

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
4. RNOH: 0.82.1; SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1 Release; ROM:6.0.0.120 SP7



## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**组件 SafeAreaProvider**

您应该在应用的根组件中添加 `SafeAreaProvider`。在使用 react-native-screens 时，您可能还需要在其他地方添加它，例如模态框和路由的根部。

请注意，Provider 不应放在使用 Animated 动画的 View 内或 ScrollView 内，因为这可能导致非常频繁的更新。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | -------- |
| `Props` | 接受所有 View 属性。默认样式为 {flex: 1}。 | object | no | All | yes |
| `initialMetrics` | 可用于提供 frame 和 insets 的初始值，这允许立即渲染。有关如何使用此属性的更多信息，请参阅优化部分。 | object | no | All | yes |

**组件 SafeAreaView**

`SafeAreaView` 是一个常规的 View 组件，并将安全区域插入（insets）应用为 padding 或 margin。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | -------- |
| `Props` | 接受所有 View 属性。默认样式为 {flex: 1}。 | object | no | All | yes |
| `edges` | 设置要应用安全区域插入的边。默认为全部。 | array | no | All | yes |
| `mode` | 可选，padding（默认）或 margin。将安全区域应用到 padding 或 margin。 | string | no | All | yes |

# API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ------------------ |
| useSafeAreaInsets | 返回最近 Provider 的安全区域插入（insets）。 | object | no | All | yes |
| useSafeAreaFrame | 返回最近 Provider 的 frame。这可以替代 Dimensions 模块使用。 | object | no | All | yes |
| SafeAreaInsetsContext | 提供安全区域插入（insets）值的 React Context。 | object | no | All | yes |
| withSafeAreaInsets<sup>5.1.1+</sup> | 高阶组件，将安全区域插入（insets）作为 insets 属性提供。 | function | no | All | yes |
| SafeAreaFrameContext | 提供安全区域 frame 值的 React Context。 | object | no | All | yes |
| initialWindowMetrics | 初始渲染时窗口的插入（insets）和 frame。这可以与 SafeAreaProvider 的 initialMetrics 一起使用。 | object | no | All | yes |
| SafeAreaListener<sup>5.6.3+</sup>  | 监听渲染位置的安全区域变化 | object | no | All | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/th3rdwave/react-native-safe-area-context/blob/main/LICENSE) ，请自由地享受和参与开源。
