> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-rotate</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/dgladkov/react-native-image-rotate">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/dgladkov/react-native-image-rotate/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-image-rotate)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
|-------| ------------------------------------------------------------ | ---------- |
| <= 2.1.0-0.0.1@deprecated | [@react-native-oh-tpl/react-native-image-rotate Releases(deprecated)](https://github.com/react-native-oh-library/react-native-image-rotate/releases) | 0.72       |
| 2.1.1 | [@react-native-ohos/react-native-image-rotate Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-rotate/releases)                        | 0.72       |
| 2.2.0 | [@react-native-ohos/react-native-image-rotate Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-rotate/releases)                        | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

<!-- tabs:start -->

进入到工程目录并输入以下命令：

#### npm

```bash
npm install @react-native-ohos/react-native-image-rotate
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-image-rotate
```

快速使用：

```js
import React, { Component } from 'react';
import {
  Image,
  StyleSheet,
  Text,
  TouchableHighlight,
  View
} from 'react-native';

import ImageRotate from 'react-native-image-rotate';

const SOURCE_IMAGE = 'https://upload.wikimedia.org/wikipedia/en/5/56/Warcraft_Teaser_Poster.jpg';

export default class App extends Component {

  constructor() {
    super();
    this.state = {
      image: SOURCE_IMAGE,
      currentAngle: 0,
      width: 150,
      height: 240,
    };

    this.rotate = this.rotate.bind(this);
  }

  rotate(angle) {
    const nextAngle = this.state.currentAngle + angle;
    ImageRotate.rotateImage(
      SOURCE_IMAGE,
      nextAngle,
      (uri) => {
        this.setState({
          image: uri,
          currentAngle: nextAngle,
          width: this.state.height,
          height: this.state.width,
        });
      },
      (error) => {
        console.error(error);
      }
    );
  }

  render() {
    return (
      <View style={styles.container}>
        <View style={styles.imageContainer}>
          <Image style={{width: this.state.width, height: this.state.height}} source={{uri: this.state.image}} />
        </View>
        <TouchableHighlight
          onPress={() => this.rotate(90)}
          style={styles.button}
        >
          <Text style={styles.text}>ROTATE CW</Text>
        </TouchableHighlight>

        <TouchableHighlight
          onPress={() => this.rotate(-90)}
          style={styles.button}
        >
          <Text style={styles.text}>ROTATE CCW</Text>
        </TouchableHighlight>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  button: {
    backgroundColor: 'red',
    padding: 5,
    margin: 5,
  },
  imageContainer: {
    height: 240,
    justifyContent: 'center',
  },
  text: {
    color: 'white',
  },
});

```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

|                           | 是否支持autolink | RN框架版本 |
|---------------------------|-----------------|------------|
| ~2.2.0                    |  No              |  0.77     |
| ~2.1.1                    |  Yes             |  0.72     |
| <= 2.1.0-0.0.1@deprecated |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

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
    "@react-native-ohos/react-native-image-rotate": "file:../../node_modules/@react-native-ohos/react-native-image-rotate/harmony/imageRotate.har"
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

### 3.配置 CMakeLists 和引入 ImageRotatePackage

> 若使用的是 <=  2.1.0-0.0.1 版本，请跳过本章。

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-image-rotate/src/main/cpp" ./imageRotate)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_image_rotate)
# RNOH_END: manual_package_linking_2
```
打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ImageRotatePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ImageRotatePackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNImageRotatePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
  
+  import { RNImageRotatePackage } from '@react-native-ohos/react-native-image-rotate/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNImageRotatePackage(ctx)
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

## 静态方法

> [!TIP]"Platform"列表示该属性在原三方库上支持的平台。

> [!TIP]"HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

Name | Description | Type | Required | Platform | HarmonyOS   Support
-- | -- | -- | -- | -- | --
rotateImage | 旋转图片 | Function | no | iOS/Android | yes

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/dgladkov/react-native-image-rotate/blob/master/LICENSE) ，请自由地享受和参与开源。
