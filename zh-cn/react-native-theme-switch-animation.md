> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-theme-switch-animation</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/WadhahEssam/react-native-theme-switch-animation">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/WadhahEssam/react-native-theme-switch-animation/blob/main/README.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-theme-switch-animation)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本         | 发布信息                                                                                                                                                                     | 支持RN版本 |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| <= 0.6.0-2.1.1@deprecated | [@react-native-oh-tpl/react-native-theme-switch-animation Releases(deprecated)](https://github.com/react-native-oh-library/react-native-theme-switch-animation/releases) | 0.72       |
| 0.6.1            | [@react-native-ohos/react-native-theme-switch-animation Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-theme-switch-animation/releases)                | 0.72       |
| 0.8.1            | [@react-native-ohos/react-native-theme-switch-animation Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-theme-switch-animation/releases)                | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-theme-switch-animation
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-theme-switch-animation
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import { StyleSheet, View, Button, Text } from 'react-native';
import switchTheme from 'react-native-theme-switch-animation';

export function ReactNativeThemeSwitchAnimationDemo() {
  const [theme, setTheme] = React.useState('light');
  
  return (
      <View
        style={{
          ...styles.container,
          backgroundColor: theme === 'light' ? 'white' : 'black',
        }}
      >
        <View
          style={{
            borderWidth: 1,
            borderColor: theme === 'light' ? 'black' : 'white',
            borderRadius: 1.4,
            padding: 50,
          }}
        >
          <Text
            style={{
              color: theme === 'light' ? 'black' : 'white',
            }}
          >
            tests
          </Text>
        </View>

        <View style={{ marginTop: 10 }}>
          <Button
            title="start"
            onPress={() => {
              switchTheme({
                switchThemeFunction: () => {
                  setTheme(theme === 'light' ? 'dark' : 'light');
                },
                animationConfig: {
                  type: 'inverted-circular',
                  duration: 2000,
                  startingPoint: {
                    cxRatio: 0.5,
                    cyRatio: 0.5,
                  },
                },
              });
            }}
          />
        </View>
      </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  box: {
    width: 60,
    height: 60,
    marginVertical: 20,
  },
});

export default ReactNativeThemeSwitchAnimationDemo;
```

## 使用 Codegen

Version >= @react-native-ohos/react-native-theme-switch-animation@0.6.1，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-theme-switch-animation@0.6.1，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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

    "@react-native-ohos/react-native-theme-switch-animation": "file:../../node_modules/@react-native-ohos/react-native-theme-switch-animation/harmony/react_native_theme_switch.har"
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

### 3.配置 CMakeLists 和引入 ThemeSwitchAnimationPackage

> 若使用的是 <= 0.6.0-2.1.1 版本，请跳过本章。


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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-theme-switch-animation/src/main/cpp" ./theme-switch-animation)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_theme_switch_animation)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ThemeSwitchAnimationPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ThemeSwitchAnimationPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 RNThemeSwitchPackage

打开 `entry/src/main/ets/RNPackagesFactory.ets`，添加：

```diff
...
+ import { RNThemeSwitchPackage } from "@react-native-ohos/react-native-theme-switch-animation/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNThemeSwitchPackage(ctx),
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

### 注意事项

本库 HarmonyOS 侧实现依赖@react-native-ohos/react-native-safe-area-context的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入react-native-safe-area-context请参照[@react-native-ohos/react-native-safe-area-context 文档](/zh-cn/react-native-safe-area-context.md)进行引入

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**switchTheme Function Props**

| Prop   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `switchThemeFunction`  |Adds the function you use in your app to switch themes, doesn't matter if you use redux/context/zustand/mobx or any other way |  () => void | no     | All  | yes      |
| `animationConfig`  | Configuration for the animation -> type, duration, starting point | AnimationConfig |  no     | All   | yes      |

**animationConfig options**

| Prop   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `type`  | Specifies animation type | fade circular inverted-circular |  no     | All   | yes      |
| `duration`  | Specifies duration in milliseconds | number |  no     | All   | yes      |
| `startingPoint`  | Configuration for the circular animation, where does the animation start in the screen | 	StartingPointConfig |  no     | All   | yes      |
| `captureType`<sup>0.8.1+</sup> | (iOS only) layer is the default and suitable for most cases, hierarchy is more complex and can cause flickering in (inverted-circular) animation, but it solves issue where some elements are not visible while animation is happening | layer or hierarchy | no | iOS | no |

**startingPoint options**

| Prop   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `cx`  | Specifies starting x point for circular and inverted-circular animation (should not exceed your screen width) |number|  no     | All   | yes      |
| `cy`  | Specifies starting y point for circular and inverted-circular animation (should not exceed your screen height) |number|  no     | All   | yes      |
| `cxRatio`  | Specifies starting percentage of x point for circular and inverted-circular animation (should be number between -1 and 1) |number|  no     | All   | yes      |
| `cyRatio`  | Specifies starting percentage of y point for circular and inverted-circular animation (should be number between -1 and 1) |number|  no     | All   | yes      |

## 遗留问题

- [ ] circular动画效果动画开始前有一个闪屏的问题，后续需要提供在图片上剪裁出一个圆形，透过圆形可以看到下方节点的接口或方法。[issue#6](https://github.com/react-native-oh-library/react-native-theme-switch-animation/issues/6)

## 其他

captureType属性 HarmonyOS 未支持，因该属性旨在处理 iOS 端的在 inverted-circular 倒圆动画进行时某些元素不可见问题，而 HarmonyOS 端无该问题。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/WadhahEssam/react-native-theme-switch-animation/blob/main/LICENSE) ，请自由地享受和参与开源。