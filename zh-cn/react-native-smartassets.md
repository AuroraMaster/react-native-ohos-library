> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-smartassets</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/smallnew/react-native-smartassets">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/smallnew/react-native-smartassets/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/smallnew/react-native-smartassets)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-smartassets Releases](https://github.com/smallnew/react-native-smartassets/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-smartassets
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-smartassets
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { View, Image } from 'react-native';
import { SmartAssets } from 'react-native-smartassets';

export default function App() {
  // 在应用启动时初始化 SmartAssets
  SmartAssets.initSmartAssets();

  return (
    <View>
      {/* 正常使用 Image 组件，SmartAssets 会自动处理资源加载 */}
      <Image 
        source={require('./assets/images/demo.png')} 
        style={{ width: 100, height: 100 }}
      />
    </View>
  );
}
```

## Link

目前HarmonyOS暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的HarmonyOS工程 `harmony`

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
    "@react-native-oh-tpl/react-native-smartassets": "file:../../node_modules/@react-native-oh-tpl/react-native-smartassets/harmony/smartassets.har"
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

### 3.配置 CMakeLists 和引入 SmartAssetsPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-smartassets/src/main/cpp" ./smartassets)
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
+ target_link_libraries(rnoh_app PUBLIC smartassets)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SmartAssetsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<SmartAssetsPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 SmartAssetsPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { SmartAssetsPackage } from '@react-native-oh-tpl/react-native-smartassets';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SmartAssetsPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-smartassets Releases](https://github.com/smallnew/react-native-smartassets/releases)

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.32; SDK: HarmonyOS-Next-DB6 5.0.0.61; IDE: DevEco Studio 5.0.3.706; ROM: 3.0.0.61;

<!-- ### 使用限制

- 仅支持通过 `require()` 方式引用的本地图片资源
- 不支持网络图片（http/https URL）
- 图片文件必须具有有效的图片扩展名（.png、.jpg、.jpeg、.gif、.webp、.svg、.bmp、.tiff） -->

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

SmartAssets 是一个 React Native 图片资源智能加载库。它通过 hook `AssetSourceResolver.defaultAsset` 方法改变了 React Native 的图片加载逻辑，让应用能够智能地从应用包（Android APK、iOS IPA、HarmonyOS HAP）和文件系统沙箱路径中加载图片资源。

**Name** | **Description** | **Type** | **Required** | **Platform** | **HarmonyOS Support**
-- | -- | -- | -- | -- | --
initSmartAssets | 初始化 SmartAssets，设置图片加载 hook | function | yes | All | yes
findAssetInBundles | 在应用包和沙箱路径中查找指定名称的图片资源 | function | no | 	Harmony | yes
## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/smallnew/react-native-smartassets/blob/master/LICENSE) ，请自由地享受和参与开源。
