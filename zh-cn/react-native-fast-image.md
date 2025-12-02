> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-fast-image</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/DylanVann/react-native-fast-image">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-fast-image/blob/harmony/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-fast-image)

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：@react-native-ohos/react-native-fast-image，具体版本所属关系如下：


| 三方库版本 | 包名                                                    | 仓库地址 | 发布(Release) | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |  ---------- |  ---------- |
| 8.6.3 | @react-native-oh-tpl/react-native-fast-image | [Github](https://github.com/react-native-oh-library/react-native-fast-image)|[Github Releases](https://github.com/react-native-oh-library/react-native-fast-image/releases)|0.72       |
| 8.7.0 | @react-native-ohos/react-native-fast-image          | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-fast-image/tree/br_rnoh0.77) |[Gitcode Releases]() | 0.77       |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-fast-image

# 0.77
npm install @react-native-ohos/react-native-fast-image
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-fast-image

# 0.77
yarn add @react-native-ohos/react-native-fast-image
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { StyleSheet, View, ScrollView } from "react-native";
import FastImage, {
  ResizeMode,
  OnLoadEvent,
  OnProgressEvent,
} from "react-native-fast-image";

export const FastImageDemo = () => {
  return (
    <ScrollView>
      <View>
        <FastImage
          style={styles.image}
          source={{
            uri: "https://res8.vmallres.com/pimages/uomcdn/CN/pms/202205/gbom/6941487259298/428_428_D7BFF22D4678EB68440F914B352214C4mp_tds.png",
          }}
          resizeMode={FastImage.resizeMode.contain}
          onLoadStart={() => {
            console.log("onLoadStart: success");
          }}
          onProgress={(e: OnProgressEvent) => {
            console.log(
              "onProgress: success loaded=" +
                e.nativeEvent.loaded +
                " total=" +
                e.nativeEvent.total
            );
          }}
          onLoad={(e: OnLoadEvent) => {
            console.log(
              "onLoad: success width=" +
                e.nativeEvent.width +
                " height=" +
                e.nativeEvent.height
            );
          }}
          onError={() => {
            console.log("onError: success");
          }}
          onLoadEnd={() => {
            console.log("onLoadEnd: success");
          }}
        />
      </View>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  image: {
    width: 200,
    height: 200,
    margin: 20,
  },
});
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

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
     // 0.72
    "@react-native-oh-tpl/react-native-fast-image": "file:../../node_modules/@react-native-oh-tpl/react-native-fast-image/harmony/fast_image.har"

     // 0.77
    "@react-native-ohos/react-native-fast-image": "file:../../node_modules/@react-native-ohos/react-native-fast-image/harmony/fast_image.har"
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

### 3.配置 CMakeLists 和引入 FastImagePackage

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
# 0.72
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-fast-image/src/main/cpp" ./fast-image)

# 0.77
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-fast-image/src/main/cpp" ./fast-image)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_fast_image)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "FastImagePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<FastImagePackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 FastImagePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ // 0.72 
+ import {FastImagePackage} from '@react-native-oh-tpl/react-native-fast-image/ts';

+ // 0.77
+ import {FastImagePackage} from '@react-native-ohos/react-native-fast-image/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new FastImagePackage(ctx)
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

本文档内容基于以下版本验证通过：

1、RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); IDE: DevEco Studio 5.1.1.830; ROM: 6.0.0.112 SP12;  
2、RNOH: 0.77.18; SDK: HarmonyOS-5.1.1.208(API19); IDE: DevEco Studio 5.1.1.830; ROM: 6.0.0.112 SP12;


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                           | Description                                                                               | Type             | Required | Platform | HarmonyOS Support |
| ------------------------------ | ----------------------------------------------------------------------------------------- | ---------------- | -------- | -------- | ----------------- |
| `source.uri`                   | Source for the remote image to load.                                                      | string           | yes      | All      | yes               |
| `source.headers?`              | Headers to load the image with. e.g. { Authorization: 'someAuthToken' }.                  | object           | yes      | All      | yes               |
| `source.priority?`             | loading url priority                                                                      | enum             | no       | All      | no                |
| `source.cache?`                | setting loading url cache mode                                                            | enum             | no       | All      | no                |
| `defaultSource?`               | An asset loaded with require(...).                                                        | number           | yes      | All      | yes               |
| `resizeMode?`                  | loading image for scale mode                                                              | enum             | yes      | All      | yes               |
| `onLoadStart`                  | Called when the image starts to load.                                                     | function         | yes      | All      | yes               |
| `onProgress`                   | Called when the image is loading.                                                         | function         | yes      | All      | yes               |
| `onLoad`                       | Called on a successful image fetch. Called with the width and height of the loaded image. | function         | yes      | All      | yes               |
| `onError`                      | Called on an image fetching error.                                                        | function         | yes      | All      | yes               |
| `onLoadEnd`                    | Called when the image finishes loading, whether it was successful or an error.            | function         | yes      | All      | yes               |
| `tintColor?`                   | If supplied, changes the color of all the non-transparent pixels to the given color.      | number \| string | yes      | All      | yes               |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                              | Description                                | Type     | Required | Platform | HarmonyOS Support |
| ------------------------------------------------- | ------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `FastImage.preload`          | Preload images to display later. e.g.      | function | no       | All      | yes                |
| `FastImage.clearMemoryCache` | Clear all images from memory cache.        | function | no       | All      | yes                |
| `FastImage.clearDiskCache`   | Clear all images from disk cache. priority | function | no       | All      | yes                |

## 遗留问题

- [ ] 不支持属性 source.cache.  [issue#57](https://github.com/react-native-oh-library/react-native-fast-image/issues/57)
- [ ] 不支持属性 source.priority.  [issue#56](https://github.com/react-native-oh-library/react-native-fast-image/issues/56)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/DylanVann/react-native-fast-image/blob/main/LICENSE) ，请自由地享受和参与开源。

