> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-compass-heading</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/firofame/react-native-compass-heading">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/firofame/react-native-compass-heading/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-compass-heading)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.5.0      | [@react-native-oh-tpl/react-native-compass-heading Releases](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Freact-native-oh-library%2Freact-native-compass-heading%2Freleases) | 0.72       |
| 2.0.2      | [@react-native-ohos/react-native-compass-heading Releases]() | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# V1.5.0
npm install @react-native-oh-tpl/react-native-compass-heading

# V2.0.2
npm install @react-native-ohos/react-native-compass-heading
```

#### **yarn**

```bash
# V1.5.0
yarn add @react-native-oh-tpl/react-native-compass-heading

# V2.0.2
yarn add @react-native-ohos/react-native-compass-heading
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from "react";
import { useState, useEffect } from "react";
import { StyleSheet, View, Text, Button, ScrollView } from "react-native";
import CompassHeading from "react-native-compass-heading";

export function RNCompassHeading() {
  const [heading, setHeading] = useState(0);
  const [accuracy, setAccuracy] = useState(0);

  interface Data {
    heading: number;
    accuracy: number;
  }

  useEffect(() => {
    const degree_update_rate = 3;
    CompassHeading.start(degree_update_rate, (data: Data) => {
      setHeading(data.heading);
      setAccuracy(data.accuracy);
    });
    return () => {
      CompassHeading.stop();
    };
  }, []);

  return (
    <ScrollView>
      <View
        style={{
          width: "100%",
          height: "100%",
          backgroundColor: "white",
          flex: 1,
        }}
      >
        <View style={styles.container}>
          <Text>{"heading: " + heading}</Text>
          <Text>{"headings: " + accuracy}</Text>
        </View>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
    height: 400,
  },
});
```

## 使用 Codegen

> [!TIP] V2.0.2 不需要执行 Codegen。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

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

- V1.5.0

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-compass-heading": "file:../../node_modules/@react-native-oh-tpl/react-native-compass-heading/harmony/compass_heading.har"
  }
```

- V2.0.2

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-compass-heading": "file:../../node_modules/@react-native-ohos/react-native-compass-heading/harmony/compass_heading.har"
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

### 3.配置 CMakeLists 和引入 RNCompassHeadingPackage

> V2.0.2 需要配置 CMakeLists 和引入 RNCompassHeadingPackage。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/@react-native-ohos/react-native-compass-heading/src/main/cpp" ./compass_heading)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_compass_heading)
# RNOH_BEGIN: manual_package_linking_2
```

> [!Tip] 注意：上面NODE_MODULES定义，为源库的安装路径，用户可以根据安装源库的路径定义NODE_MODULES

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNCompassHeadingPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNCompassHeadingPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNCompassHeadingPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
// V1.5.0
+ import {RNCompassHeadingPackage} from '@react-native-oh-tpl/react-native-compass-heading/ts';

// V2.0.2
+ import {RNCompassHeadingPackage} from '@react-native-ohos/react-native-compass-heading/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNCompassHeadingPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.5.0      | [@react-native-oh-tpl/react-native-compass-heading Releases](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Freact-native-oh-library%2Freact-native-compass-heading%2Freleases) | 0.72       |
| 2.0.2      | [@react-native-ohos/react-native-compass-heading Releases]() | 0.77       |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name    | Description   | Type                                                  | Required | Platform    | HarmonyOS Support |
| ------- | ------------- | ----------------------------------------------------- | -------- | ----------- | ----------------- |
| `start` | start compass | (degreeUpdateRate: number, callback: CompassCallback) | yes      | Android/iOS | yes               |
| `stop`  | stop compass  | void                                                  | no       | Android/iOS | yes               |

**start(degree_update_rate,callback)**

| Name                 | Description               | Type                                          | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------- | --------------------------------------------- | -------- | ----------- | ----------------- |
| `degree_update_rate` | compass refresh frequency | number                                        | yes      | Android/iOS | yes               |
| `callback`           | compass callback          | ({heading: number;accuracy: number;}) => void | yes      | Android/iOS | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/firofame/react-native-compass-heading/blob/master/LICENSE) ，请自由地享受和参与开源。
