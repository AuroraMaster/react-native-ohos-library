> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-screenshot-prevent</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/killserver/react-native-screenshot-prevent">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/killserver/react-native-screenshot-prevent/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-screenshot-prevent)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 1.2.1-0.0.2@deprecated | [@react-native-oh-tpl/react-native-screenshot-prevent Releases(deprecated)](https://github.com/react-native-oh-library/react-native-screenshot-prevent/releases) | 0.72         |
| 1.2.2      | [@react-native-ohos/react-native-screenshot-prevent Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-screenshot-prevent/releases)                        | 0.72       |
| 1.3.0      | [@react-native-ohos/react-native-screenshot-prevent Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-screenshot-prevent/releases)                        | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-screenshot-prevent
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-screenshot-prevent
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useEffect } from "react";
import { Alert } from "react-native";
import RNScreenshotPrevent, {
  addListener,
} from "react-native-screenshot-prevent";

RNScreenshotPrevent.enabled(true);

RNScreenshotPrevent.enabled(false);

useEffect(() => {
  const subscription = RNScreenshotPrevent.addListener(() => {
    Alert.alert(
      "You have taken a screenshot of the app.This is prohibited due to security reasons."
    );
  });

  return () => {
    subscription.remove();
  };
}, []);
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~1.3.0                               |  No              |  0.77     |
| ~1.2.2                              |  Yes             |  0.72     |
| <= 1.2.1-0.0.2@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

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
    "@react-native-ohos/react-native-screenshot-prevent": "file:../../node_modules/@react-native-ohos/react-native-screenshot-prevent/harmony/react_native_screenshot_prevent.har"
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

### 3.配置 CMakeLists 和引入 RNScreenShotPreventPackage

> 若使用的是 <= 1.2.1-0.0.2 版本，请跳过本章。

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-screenshot-prevent/src/main/cpp" ./react_native_screenshot_prevent)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_screenshot_prevent)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNScreenShotPreventPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNScreenShotPreventPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNScreenShotPreventPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNScreenShotPreventPackage } from "@react-native-ohos/react-native-screenshot-prevent/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNScreenShotPreventPackage(ctx)
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

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### 权限要求

- 由于此库涉及开启窗口隐私模式，调用对应接口时则需要配置对应的权限，权限需配置在 entry/src/main 目录下 module.json5 文件中。需要打开 `entry/src/main/ets/module.json5`，添加：

```diff
  ...
 "requestPermissions": [
      {
        "name": "ohos.permission.INTERNET"
      },
      {
        "name": "ohos.permission.ACCELEROMETER"
      },
+     {
+        "name": "ohos.permission.PRIVACY_WINDOW"
+     }
    ]
```

## RNScreenshotPrevent

默认导出 RNScreenshotPrevent 对象

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### RNScreenshotPrevent 方法

| Name              | Description                                                                                                                                                                        | Type     | Required | Platform    | HarmonyOS Support |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| enabled           | Whether to enable the function of disabling screenshot/screen recording                                                                                                            | function | no       | iOS/Android | yes               |
| addListener       | notifies when user has taken screenshot (yes, after taking) - you can show alert or do some actions                                                                                | function | no       | iOS         | yes               |
| enableSecureView  | creates a hidden secureTextField which prevents Application UI capture on screenshots and allow uses imgUri as the source of the background image (can be both https://, file:///) | function | no       | iOS         | no                |
| disableSecureView | remove a hidden secureTextField which prevents Application UI capture on screenshots                                                                                               | function | no       | iOS         | no                |

## 遗留问题

- [ ] iOS 支持创建隐藏的安全文本字段，防止应用程序 UI 捕获屏幕截图 [issue#3](https://github.com/react-native-oh-library/react-native-screenshot-prevent/issues/3)
- [ ] iOS 支持创建一个隐藏的安全文本字段，防止应用程序 UI 捕获屏幕截图，并使用 imgUri 作为背景图像的来源（可以是 https://, file:///） [issue#2](https://github.com/react-native-oh-library/react-native-screenshot-prevent/issues/2)
- [ ] iOS 支持移除隐藏的安全文本字段，允许应用程序 UI 捕获屏幕截图 [issue#1](https://github.com/react-native-oh-library/react-native-screenshot-prevent/issues/1)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/killserver/react-native-screenshot-prevent/blob/main/LICENSE) ，请自由地享受和参与开源。
