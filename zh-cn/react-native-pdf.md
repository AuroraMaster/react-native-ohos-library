> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-pdf</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wonday/react-native-pdf">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/wonday/react-native-pdf/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-pdf)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本         | 发布信息                                                                                                                             | 支持RN版本 |
|------------------|------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| <= 6.7.4-0.3.6@deprecated | [@react-native-oh-tpl/react-native-pdf Releases(deprecated)](https://github.com/react-native-oh-library/react-native-pdf/releases) | 0.72       |
| 6.7.5            | [@react-native-ohos/react-native-pdf Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-pdf/releases)                | 0.72       |
| 6.8.0            | [@react-native-ohos/react-native-pdf Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-pdf/releases)                | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-pdf
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-pdf
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { View, Dimensions, StyleSheet } from "react-native";
import Pdf from "react-native-pdf";

export function PdfExample() {
  // const source = { uri: 'https://www-file.huawei.com/minisite/media/annual_report/annual_report_2022_cn.pdf', cache: true };
  const source = require("../assets/test.pdf");

  return (
    <View style={styles.sectionContainer}>
      <Pdf
        source={source}
        onLoadComplete={(numberOfPages, filePath) => {
          console.log(`Number of pages: ${numberOfPages}`);
        }}
        onPageChanged={(page, numberOfPages) => {
          console.log(`Current page: ${page}`);
        }}
        onError={(error) => {
          console.log(error);
        }}
        onPressLink={(uri) => {
          console.log(`Link pressed: ${uri}`);
        }}
        style={styles.pdf}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  sectionContainer: {
    flex: 1,
    justifyContent: "flex-start",
    alignItems: "center",
  },
  pdf: {
    flex: 1,
    width: Dimensions.get("window").width,
    height: Dimensions.get("window").height,
  },
});
```

## 使用 Codegen

Version >= @react-native-ohos/react-native-pdf@6.7.5，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-pdf@6.7.5，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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
    "@react-native-ohos/react-native-pdf": "file:../../node_modules/@react-native-ohos/react-native-pdf/harmony/pdfview.har"
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

### 3.配置 CMakeLists 和引入 PdfViewPackage

> 若使用的是 <= 6.7.4-0.3.6 版本，请跳过本章。

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-pdf/src/main/cpp" ./pdfview)
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
#include "SamplePackage.h"
+ #include "PdfViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<PdfViewPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RTNPdfView 组件

找到 **function buildCustomRNComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RTNPdfView, PDF_VIEW_TYPE } from '@react-native-ohos/react-native-pdf';

  @Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+  if (ctx.componentName === PDF_VIEW_TYPE) {
+     RTNPdfView({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag,
+     })
+   }
    ...
  }
  ...

```

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ PDF_VIEW_TYPE
  ];
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

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                    | Description                                                  | Type                                                         | Required | Platform      | HarmonyOS Support |
| --------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ------------- | ----------------- |
| source                                  | PDF 数据源配置，如 {uri:xxx, cache:false}，详情见下文说明 | object                                                       | YES      | iOS / Android | yes               |
| page                                    | 初始页码索引                                           | number                                                       | NO       | iOS / Android | yes               |
| scale                                   | 显示缩放比例，需满足 minScale<=scale<=maxScale                             | number                                                       | NO       | iOS / Android | yes               |
| minScale                                | 最小缩放值                                                    | number                                                       | NO       | iOS / Android | yes               |
| maxScale                                | 最大缩放值                                                    | number                                                       | NO       | iOS / Android | yes               |
| horizontal                              | 页面横向滚动，若需监听方向变化可配合 [[react-native-orientation-locker\]](https://github.com/react-native-oh-library/react-native-orientation-locker) | bool                                                         | NO       | iOS / Android | no                |
| showsHorizontalScrollIndicator          | 控制 iOS 上横向滚动条指示器的显示与隐藏    | bool                                                         | NO       | iOS           | no                |
| showsVerticalScrollIndicator            | 控制 iOS 上纵向滚动条指示器的显示与隐藏      | bool                                                         | NO       | iOS           | no                |
| fitWidth                                | 为 true 时内容自适应宽度，且不可与 scale 同时使用 | bool                                                         | NO       | iOS / Android | no                |
| fitPolicy                               | 0 表示按宽度适配，1 表示按高度，2 表示同时适配（默认）               | number                                                       | NO       | iOS / Android | yes               |
| spacing                                 | 各页之间的间距                               | number                                                       | NO       | iOS / Android | yes               |
| password                                | PDF 密码，错误时会触发 onError 并提示 “Password required or incorrect password.” | string                                                       | NO       | iOS / Android | yes               |
| style                                   | 常规 View 样式，可用于设置边框、间距颜色等 | object                                                       | NO       | iOS / Android | yes               |
| renderActivityIndicator                 | 加载过程中显示的自定义指示器组件 | (progress) => Component                                      | NO       | iOS / Android | no                |
| enableAntialiasing                      | 在低分辨率屏幕上提升渲染质量（Android 4.4 可能出现问题） | bool                                                         | NO       | iOS / Android | no                |
| enablePaging                            | 仅在屏幕上显示一页                                 | bool                                                         | NO       | iOS / Android | no                |
| enableRTL                               | 以 “page3, page2, page1” 方式反向滚动                         | bool                                                         | NO       | iOS / Android | no                |
| enableAnnotationRendering               | 启用批注渲染，注意 iOS 仅支持初始设置，不支持实时切换 | bool                                                         | NO       | iOS           | no                |
| enableDoubleTapZoom                     | 启用双击缩放手势                            | bool                                                         | NO       | iOS / Android | no                |
| trustAllCerts                           | 允许连接使用自签名证书的服务器  | bool                                                         | NO       | iOS / Android | no                |
| singlePage                              | 仅展示第一页，适用于缩略图场景             | bool                                                         | NO       | iOS / Android | no                |
| onLoadProgress                          | 加载进度回调，返回 0-1 的进度值         | function(percent)                                            | NO       | iOS / Android | yes               |
| onLoadComplete                          | PDF 加载完成回调，返回总页数、本地/缓存路径、尺寸以及目录 | function(numberOfPages, path, {width, height}, tableContents) | NO       | iOS / Android | partially         |
| onPageChanged                           | 翻页回调，返回当前页及总页数 | function(page,numberOfPages)                                 | NO       | iOS / Android | yes               |
| onError                                 | 发生错误时的回调                                 | function(error)                                              | NO       | iOS / Android | yes               |
| onPageSingleTap                         | 页面被单击时的回调                         | function(page)                                               | NO       | iOS / Android | no                |
| onScaleChanged                          | 缩放变化时的回调                                     | function(scale)                                              | NO       | iOS / Android | yes               |
| onPressLink                             | 点击 PDF 内链接时的回调                                    | function(uri)                                                | NO       | iOS / Android | yes               |
| scrollEnabled<sup>6.7.7+</sup>          | 启用或禁用滚动                                     | bool                                                         | NO       | iOS           | yes               |
| progressContainerStyle<sup>6.7.7+</sup> | 进度容器的样式，可设置边框或间距颜色 | object                                                       | NO       | iOS / Android | no                |

#### Source

| Name          | Description                                   | Type   | Required | Platform      | HarmonyOS Support |
| ------------- | --------------------------------------------- | ------ | -------- | ------------- | ----------------- |
| uri           | 详细说明见下文                 | object | YES      | iOS / Android | yes               |
| cache         | 是否使用缓存                              | bool   | NO       | iOS / Android | no                |
| cacheFileName | 缓存 PDF 使用的文件名        | string | NO       | iOS / Android | no                |
| expiration    | 缓存文件过期秒数（0 表示不过期） | number | NO       | iOS / Android | no                |
| method        | 当 uri 为 URL 时的请求方法              | string | NO       | iOS / Android | no                |
| headers       | 当 uri 为 URL 时的请求头             | object | NO       | iOS / Android | no                |

#### Uri

| Name                                                               | Description                                                                             | Type          | Required | Platform      | HarmonyOS Support |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------- | ------------- | -------- | ------------- | ----------------- |
| {uri:"http://xxx/xxx.pdf"}                                         | 从 URL 加载 PDF                                                                     | object        | NO       | iOS / Android | yes               |
| {require("./test.pdf")}                                            | 加载与 JS 文件关联的本地资源（无需在 Xcode 中额外添加）                                   | require(path) | NO       | iOS           | yes               |
| {uri:"bundle-assets://path/to/xxx.pdf"}                            | 从 Android 项目 assets 目录加载 PDF | object        | NO       | iOS           | no                |
| {uri:"data:application/pdf;base64,JVBERi0xLjcKJc..."}              | 通过 Base64 字符串加载 PDF                                                             | object        | NO       | iOS / Android | no                |
| {uri:"file:///absolute/path/to/xxx.pdf"}                           | 从本地文件系统加载 PDF                                                         | object        | NO       | iOS / Android | no                |
| {uri:"ms-appx:///xxx.pdf"}                                         | 从 UWP 应用内置资源加载 PDF                                                           | object        | NO       | Windows       | no                |
| {uri:"content://com.example.blobs/xxxxxxxx-...?offset=0&size=xxx"} | 通过 content URI 加载 PDF                                                               | object        | NO       | iOS           | no                |
| {uri:"blob:xxxxxxxx-...?offset=0&size=xxx"}                        | 从 blob URL 加载 PDF                                                                  | object        | NO       | Android       | no                |

## 静态方法

| Name    | Description                                                                                                                              | Type                 | Required | Platform      | HarmonyOS Support |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------- | -------------------- | -------- | ------------- | ----------------- |
| setPage | 设置 PDF 组件当前页。pageNumber 为正整数，若大于总页数则保持原页码不变。 | function(pageNumber) | NO       | iOS / Android | yes                |

## 遗留问题

- [ ] onLoadComplete 回调函数参数返回目前仅支持 numberOfPages, path参数：[issue#47](https://github.com/react-native-oh-library/react-native-pdf/issues/47)
- [ ] 原库部分接口在 HarmonyOS 中没有对应属性及接口处理相关逻辑: [issue#48](https://github.com/react-native-oh-library/react-native-pdf/issues/48)
- [ ] V0.77 部分属性未实现 HarmonyOS 化:  [issue#1](https://gitcode.com/openharmony-sig/rntpc_react-native-pdf/issues/1)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wonday/react-native-pdf/blob/master/LICENSE) ，请自由地享受和参与开源。