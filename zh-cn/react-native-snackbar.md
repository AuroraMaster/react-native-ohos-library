> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-snackbar</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/cooperka/react-native-snackbar">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/cooperka/react-native-snackbar/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-snackbar)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                  | 支持RN版本 |
|--------| ------------------------------------------------------------ | ---------- |
| 2.7.1@deprecated  | [@react-native-oh-tpl/react-native-snackbar Releases(deprecated)](https://github.com/react-native-oh-library/react-native-snackbar/releases) | 0.72       |
| 2.7.2             | [@react-native-ohos/react-native-snackbar Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-snackbar/releases)   | 0.72       |
| 2.9.0             | [@react-native-ohos/react-native-snackbar Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-snackbar/releases)   | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-snackbar
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-snackbar
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { View, StyleSheet, Button, ScrollView } from "react-native";
import Snackbar from "react-native-snackbar";

export const SnackbarTest = () => {
  return (
    <View
      style={{
        width: "100%",
        height: "100%",
        backgroundColor: "white",
        flex: 1,
      }}
    >
      <ScrollView style={styles.container}>
        <View style={styles.buttonContainer}>
          <Button
            title="点击显示组件"
            onPress={() => {
              Snackbar.show({
                text: "Hello harmony",
                marginBottom: 300,
              });
            }}
          />
        </View>
      </ScrollView>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    width: "100%",
    backgroundColor: "#333",
    flex: 1,
  },
  Snackbar: {
    width: "100%",
    backgroundColor: "white",
  },
  buttonContainer: {
    margin: 20,
    padding: 20,
    backgroundColor: "#f5f5f5",
    borderRadius: 8,
  },
});
```

## 使用 Codegen

Version >= @react-native-ohos/react-native-snackbar@2.7.2，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-snackbar@2.7.2，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

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
    "@react-native-ohos/react-native-snackbar": "file:../../node_modules/@react-native-ohos/react-native-snackbar/harmony/snackbar.har"
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

### 3.在 ArkTs 侧引入 RNSnackbarPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {RNSnackbarPackage} from '@react-native-ohos/react-native-snackbar/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNSnackbarPackage(ctx)
  ];
}
```

### 4.配置 CMakeLists 和引入 SnackbarPackage

> [!TIP] V2.7.2 需要配置 CMakeLists 和引入 SnackbarPackage

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-snackbar/src/main/cpp" ./react-native-snackbar)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_snackbar)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "SnackbarPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SnackbarPackage>(ctx)
    };
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

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 5.1.0.150 (API Version 12); IDE: DevEco Studio 5.1.1.830; ROM: 5.1.0.150;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 5.0.0.71(API Version 12 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 5.1.0.150;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Snackbar.show(options)

| Name                               | Description                                                  | Type                       | Required | Platform    | HarmonyOS Support |
| ---------------------------------- | ------------------------------------------------------------ | -------------------------- | -------- | ----------- | ----------------- |
| `text`                             | The message to show.                                         | `string`                   | yes      | Android iOS | yes               |
| `textAlignCenter`<sup>2.9.0+</sup> | If true, text aligns center.                                 | `boolean`                  | no       | Android iOS | yes               |
| `duration`                         | How long to display the Snackbar                             | See below                  | no       | Android iOS | no                |
| `numberOfLines`                    | The max number of text lines to allow before ellipsizing     | `number`                   | no       | Android iOS | no                |
| `marginBottom`                     | Margin from bottom                                           | `number`                   | no       | Android iOS | yes               |
| `textColor`                        | The color of the message text.                               | `string` or `style`        | no       | Android iOS | no                |
| `backgroundColor`                  | The background color for the whole Snackbar                  | `string` or `style`        | no       | Android iOS | no                |
| `fontFamily`                       | [Android only] The basename of a .ttf font from assets/fonts/ | `string`                   | no       | Android     | no                |
| `rtl`                              | [Android only, API 17+] Whether the Snackbar should render right-to-left (requires android:supportsRtl="true"). | `boolean`                  | no       | Android     | no                |
| `action`                           | Optional config for the action button (described below)      | `object` (described below) | no       | Android iOS | no                |

Where `duration` can be one of the following (timing may vary based on device):

- `Snackbar.LENGTH_SHORT` (just over a second)
- `Snackbar.LENGTH_LONG` (about three seconds)
- `Snackbar.LENGTH_INDEFINITE` (stays on screen until dismissed, replaced, or action button is tapped)

The optional `action` object can contain the following options:

| Key         | Type                      | Description                                   | Platform    | HarmonyOS Support |
| ----------- | ------------------------- | --------------------------------------------- | ----------- | ----------------- |
| `text`      | `string` The button text. | The button text.                              | Android iOS | no                |
| `textColor` | `string` or `style`       | The color of the button text.                 | Android iOS | no                |
| `onPress`   | `function`                | A callback for when the user taps the button. | Android iOS | no                |

### Snackbar events

You can have information on snackbar visibility.

```js
  componentDidMount() {
    const SnackbarEventEmitter = new NativeEventEmitter(
      NativeModules.RNSnackbar,
    );
    this.eventListener = SnackbarEventEmitter.addListener('onSnackbarVisibility', (event) => {
      console.log(event.event);
    });
  }

  componentWillUnmount() {
    this.eventListener.remove();
  }
```

Or, with functional components:

```js
useEffect(() => {
  const subscription = new NativeEventEmitter(
    NativeModules.RNSnackbar
  ).addListener("onSnackbarVisibility", (event) => {
    console.log(event.event);
  });
  return () => {
    subscription.remove();
  };
}, []);
```

Where event is one of the following options :

| Key                                  | Type     | Value | Description                                                                | Platform    | HarmonyOS Support |
| ------------------------------------ | -------- | ----- | -------------------------------------------------------------------------- | ----------- | ----------------- |
| `Snackbar.DISMISS_EVENT_SWIPE`       | `number` | 0     | Indicates that the Snackbar was dismissed via a swipe.                     | Android iOS | no                |
| `Snackbar.DISMISS_EVENT_ACTION`      | `number` | 1     | Indicates that the Snackbar was dismissed via an action click.             | Android iOS | no                |
| `Snackbar.DISMISS_EVENT_TIMEOUT`     | `number` | 2     | Indicates that the Snackbar was dismissed via a timeout.                   | Android iOS | no                |
| `Snackbar.DISMISS_EVENT_MANUAL`      | `number` | 3     | Indicates that the Snackbar was dismissed via Snackbar.dismiss() call.     | Android iOS | no                |
| `Snackbar.DISMISS_EVENT_CONSECUTIVE` | `number` | 4     | Indicates that the Snackbar was dismissed from a new Snackbar being shown. | Android iOS | no                |
| `Snackbar.SHOW_EVENT`                | `number` | 5     | Indicates that Snackbar appears                                            | Android iOS | no                |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name    | Description                       | Type     | Required | Platform    | HarmonyOS Support |
| ------- | --------------------------------- | -------- | -------- | ----------- | ----------------- |
| show    | Shows a Snackbar                  | function | yes      | Android iOS | yes               |
| dismiss | Dismisses any existing Snackbars. | function | yes      | Android iOS | no                |

### show()

| Name    | Description | Type   | Required | Platform    | HarmonyOS Support |
| ------- | ----------- | ------ | -------- | ----------- | ----------------- |
| options | options     | object | yes      | Android iOS | partially         |

## 遗留问题

- [ ] 不支持 duration、numberOfLines、textColor、backgroundColor、fontFamily、rtl、action 等参数以及 dismiss()接口: [issue#1](https://github.com/react-native-oh-library/react-native-snackbar/issues/1)
- [ ] 与 Android 和 iOS 的样式有一定的差异: [issue#2](https://github.com/react-native-oh-library/react-native-snackbar/issues/2)
- [ ] 无法实现 Snackbar events：[issue#3](https://github.com/react-native-oh-library/react-native-snackbar/issues/3)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/cooperka/react-native-snackbar/blob/main/LICENSE) ，请自由地享受和参与开源。
