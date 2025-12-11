> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-MJRefresh</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-studio/react-native-MJRefresh">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-studio/react-native-MJRefresh/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-MJRefresh)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                | 支持RN版本 |
|-------| ------------------------------------------------------------ | ---------- |
| <= 0.7.0-0.2.2@deprecated | [@react-native-oh-tpl/react-native-MJRefresh Releases(deprecated)](https://github.com/react-native-oh-library/react-native-MJRefresh/releases) | 0.72       |
| 0.7.1 | [@react-native-ohos/react-native-MJRefresh Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-mjrefresh/releases)                        | 0.72       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/react-native-mjrefresh
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-mjrefresh
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, { Component } from "react";
import { Text, View } from "react-native";
import MJRefresh, { ScrollView } from "react-native-mjrefresh";

interface State {
  text: string,
  refreshing: Boolean,
}

export default class MjRefreshDemo extends Component<{}, State> {
  constructor(props: any) {
    super(props);
  }

  state = {
    text: "下拉刷新",
    refreshing: false
  }
  _mjrefresh: any = null;
  _hw = {
    finishRefresh: () => {}
  }

  _onRefresh = () => {
    setTimeout(() => {
      this._hw && this._hw.finishRefresh();
    }, 1000);
  }
  render() {
    return (
      <ScrollView
        refreshControl={
          <MJRefresh
            ref={(ref: any) => this._mjrefresh = ref}
            onRefresh={
              () => {
                this.setState({
                  text: '正在刷新'
                })
                console.log('onRefresh')
                setTimeout(() => {
                  this._mjrefresh && this._mjrefresh.finishRefresh();
                }, 1000)
              }
            }
            onRefreshIdle={() => console.log('onRefreshIdle')}
            onReleaseToRefresh={() => {
              this.setState({
                text: '释放刷新'
              })
            }}
            onPulling={(e: any) => {
              console.log('cbdtest onPulling:' + e.nativeEvent.percent)
              if (e.nativeEvent.percent < 0.1) {
                this.setState({
                  text: '下拉刷新'
                })
              }
            }}
          >
            <View style={{
              height: 100, backgroundColor: 'red',
              justifyContent: 'center',
              alignItems: 'center', flexDirection: 'row'
            }}>
              <Text>{this.state.text}</Text>
            </View>
          </MJRefresh>
        }
      >
        <Text>{"mjRefresh TEST mjRefresh TEST mjRefresh TEST mjRefresh TEST mjRefresh TEST"}</Text>
      </ScrollView>
    )
  };
};
```

## Link

Version >= @react-native-ohos/react-native-mjrefresh@0.7.1，已支持 Autolink，无需手动配置，目前只支持72框架。
Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides字段

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

    "@react-native-ohos/react-native-mjrefresh": "file:../../node_modules/@react-native-ohos/react-native-mjrefresh/harmony/mjrefresh.har"
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

### 3.配置 CMakeLists 和引入 MJRefreshPackge

> 若使用的是 <= 0.7.0-0.2.2 版本，请跳过本章。

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-mjrefresh/src/main/cpp" ./mjrefresh)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_mjrefresh)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "MJRefreshPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<MJRefreshPackage>(ctx),
    };
}
```

### 4.运行

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

详情请见[react-native-MJRefresh](https://github.com/react-native-studio/react-native-MJRefresh)

| Name               | Description | Type     | Required | Platform | HarmonyOS Support (ArkTS) |HarmonyOS Support (CAPI) |
| :----------------- | ----------- | -------- | -------- | -------- | ----------------- |----------------- |
| onRefresh          | 刷新时触发 | function | No       | IOS      | yes               |yes               |
| onRefreshIdle      | 刷新闲置时触发 | function | No       | IOS      | yes               |yes               |
| onReleaseToRefresh | 可释放刷新时触发 | function | No       | IOS      | yes               |yes               |
| onPulling          | header下拉过程中触发 | function | No       | IOS      | yes               |yes               |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-MJRefresh](https://github.com/react-native-studio/react-native-MJRefresh)

| Name          | Description | Type     | Required | Platform | HarmonyOS Support (ArkTS) | HarmonyOS Support (CAPI) |
| :------------ | ----------- | -------- | -------- | -------- | ----------------- |----------------- |
| beginRefresh  | 开始刷新 | function | No       | IOS      | yes               |yes               |
| finishRefresh | 结束刷新 | function | No       | IOS      | yes               |yes               |

## 其他

## 开源协议

本项目基于 [Apache License (Apache)](https://github.com/react-native-studio/react-native-MJRefresh/blob/master/LICENSE) ，请自由地享受和参与开源。
