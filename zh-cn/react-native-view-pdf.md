> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-view-pdf</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/rumax/react-native-PDFView">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/rumax/react-native-PDFView/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-PDFView)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <=0.14.0-0.0.2@deprecated | [@react-native-oh-tpl/react-native-view-pdf Releases(deprecated)](https://github.com/react-native-oh-library/react-native-PDFView/releases) | 0.72       |
| 0.14.1      | [@react-native-ohos/react-native-view-pdf Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-pdfview/releases) | 0.72       |
| 0.15.0      | [@react-native-ohos/react-native-view-pdf Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-pdfview/releases) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-view-pdf
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-view-pdf
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { View } from "react-native";
import PDFView from "react-native-view-pdf";

export function PdfViewExample() {
  <View style={{ flex: 1 }}>
    <PDFView
      style={{ flex: 1 }}
      resource="https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf"
      resourceType="url"
      onLoad={() => {}}
      onError={(error: any) => {}}
    ></PDFView>
  </View>;
}
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~0.15.0                              |  No              |  0.77     |
| ~0.14.1                              |  Yes             |  0.72     |
| <=0.14.0-0.0.2@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 1.在工程根目录的 `oh-package.json` 添加 overrides 字段

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
    "@react-native-ohos/react-native-view-pdf": "file:../../node_modules/@react-native-ohos/react-native-view-pdf/harmony/pdf_view.har"
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

### 3.在 ArkTs 侧引入 RNPDFView 组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RNPDFView } from '@react-native-ohos/react-native-view-pdf'

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === RNPDFView.NAME) {
+   RNPDFView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。（如使用混合方案）

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ RNPDFView.NAME
  ];
```

### 4.配置 CMakeLists 和引入 ViewPdfPackage

> [!TIP] 若使用的是 <=0.14.0-0.0.2 版本，请跳过本章。 

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-view-pdf/src/main/cpp" ./pdf_view)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_pdf_view)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ViewPdfPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ViewPdfPackage>(ctx),
    };
}
```

### 5.在 ArkTs 侧引入 PDFViewPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { PDFViewPackage } from '@react-native-ohos/react-native-view-pdf/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new PDFViewPackage(ctx)
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

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name              | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| resource          | 待渲染的资源。支持从文件、URL（需编码）或 Base64 格式渲染 PDF | string   | yes      | all      | yes               |
| resourceType      | 需与 resource 对应，可选值：file（文件）、url（链接）或 base64（Base64 编码） | string   | no       | all      | yes               |
| fileFrom          | iOS：当 resourceType 设为 file 时，指定在 iOS 文件系统中的搜索路径。目前支持 documentsDirectory（文档目录）、libraryDirectory（库目录）、cachesDirectory（缓存目录）、tempDirectory（临时目录）和 bundle（应用包）。<br>HarmonyOS：支持 files（文件目录）、cache（缓存目录）、temp（临时目录） | string   | no       | iOS      | yes               |
| onLoad            | 加载完成时触发的回调函数                                     | function | no       | all      | yes               |
| onError           | 加载失败时触发的回调函数，错误信息通过参数返回（原文 Type 列修正为 function） | style    | no       | all      | yes               |
| style             | CSS 样式                       | string   | no       | all      | yes               |
| fadeInDuration    | 加载完成后 PDF 视图淡入显示的时长（单位：毫秒，默认 0.0）    | number   | no       | all      | yes               |
| enableAnnotations | 仅 Android 支持：是否启用 Android 视图注释功能（默认 false） | boolean  | no       | Android  | no                |
| urlProps          | URL 类型的扩展属性，支持指定 HTTP 方法、请求头和请求体       | map      | no       | all      | no                |
| onPageChanged     | 页面切换时触发的回调函数，返回当前页和总页数信息             | function | no       | Android  | no                |
| onScrolled        | PDF 滚动时触发的回调函数，返回滚动偏移量（范围 0-1，目前仅支持 0 和 1） | function | no       | all      | no                |

### 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ------ | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| reload | 允许重新加载 PDF 文档。这在网络问题、文档过期等情况下非常有用。 要重新加载文档，你需要获取该组件的 `ref` 引用: | function | yes      | all      | yes               |

## 遗留问题

- [ ] urlProps 属性不支持, HarmonyOS 原生组件 webview 不支持 urlProps。[issue: #5](https://github.com/react-native-oh-library/react-native-PDFView/issues/5)
- [ ] onScrolled 属性不支持, HarmonyOS 原生组件 webview 加载 pdf 文件时 onScrolled 回调函数不执行。 [issue: #6](https://github.com/react-native-oh-library/react-native-PDFView/issues/6)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/rumax/react-native-PDFView/blob/master/LICENSE) ，请自由地享受和参与开源。
