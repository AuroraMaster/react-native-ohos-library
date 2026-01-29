> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-screen-capture</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/recepkocur/react-native-screen-capture">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/recepkocur/react-native-screen-capture?tab=readme-ov-file#license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/recepkocur/react-native-screen-capture)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本                     | 发布信息                                     |Supported RN Version  |
|---------------------------|--------------------------------------------| -------------------- |
| 0.2.4 | [@react-native-ohos/react-native-screen-capture](https://gitcode.com/OpenHarmony-RN/rntpc_react-native-screen-capture/releases) | 0.72/0.77    

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-screen-capture
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-screen-capture
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { View, Button, Text, StyleSheet } from 'react-native';
import { disallowScreenshot, keepAwake } from 'react-native-screen-capture';

class AppDemo extends React.Component {
  state = {
    isVisible: false,
    screenOn: false, // false 表示允许截屏，true 表示禁止截屏
  };

  handleDisallowScreenshot = () => {
    // 切换状态：如果当前是 false（允许截屏），点击后变为 true（禁止截屏）
    const newState = !this.state.screenOn;
    this.setState({ screenOn: newState });
    disallowScreenshot(newState);
  };

  handleKeepAwake = () => {
    const newState = !this.state.isVisible;
    this.setState({ isVisible: newState });
    keepAwake(newState);
  };

  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.status}>
          防截屏状态: {this.state.screenOn ? '已禁止' : '已允许'}
        </Text>
        <Button
          title={this.state.screenOn ? "允许截屏" : "禁止截屏"}
          onPress={this.handleDisallowScreenshot}
        />
        <Text style={styles.status}>
          屏幕常亮状态: {this.state.isVisible ? '已开启' : '已关闭'}
        </Text>
        <Button
          title={this.state.isVisible ? "关闭屏幕常亮" : "开启屏幕常亮"}
          onPress={this.handleKeepAwake}
        />
      </View>
    )
  };
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    flexDirection: 'column',
    alignItems: 'center'
  },
  label: {
    fontSize: 30
  },
  status: {
    fontSize: 18,
    marginVertical: 10,
    color: '#333'
  }
})

export default AppDemo;

```
## Link

  <summary>此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 1. Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)：

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
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
  "@react-native-ohos/react-native-screen-capture": "file:../../node_modules/@react-native-ohos/react-native-screen-capture/harmony/screen_capture.har"
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


### 3.配置 CMakeLists 和引入 ScreenCapturePackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-screen-capture/src/main/cpp" ./screen-capture)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_screen_capture)
# RNOH_END: manual_package_linking_2

```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ScreenCapturePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ScreenCapturePackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 ScreenCapturePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { ScreenCapturePackage } from '@react-native-ohos/react-native-screen-capture/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+    new ScreenCapturePackage(ctx)
  ];
}
```

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
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### 权限要求

（填入相关权限配置）

在entry目录下的module.json5文件中添加权限配置：

打开 `entry/src/main/module.json5` 文件，添加权限配置：

```
 "requestPermissions": [
    {
      "name": "ohos.permission.PRIVACY_WINDOW"
    }
  ]
```

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| disallowScreenshot  | 启动或禁用防截屏 | function  | yes | ios/andriod      | yes |
| keepAwake  | 启动或禁用屏幕常亮 | function  | yes | ios/andriod      | yes |

## API 参数介绍

### disallowScreenshot(state: boolean);
* **state**: boolean类型，启动或禁用防截屏，false表示允许截屏，true表示禁止截屏。

### keepAwake(state: boolean);
* **state**: boolean类型，启动或禁用屏幕常亮，false表示允许屏幕休眠，true表示保持屏幕常亮。

## 遗留问题


## 其他


## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/recepkocur/react-native-screen-capture/blob/0.2.3/LICENSE) ，请自由地享受和参与开源。
