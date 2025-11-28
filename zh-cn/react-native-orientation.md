> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-orientation</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/yamill/react-native-orientation">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-orientation/blob/sig/LICENSE.md">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-orientation)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                  | 支持RN版本 |
|--------| ------------------------------------------------------------ | ---------- |
| 3.1.3@deprecated  | [@react-native-oh-tpl/react-native-orientation Releases(deprecated)](https://github.com/react-native-oh-library/react-native-orientation/releases) | 0.72       |
| 3.1.4             | [@react-native-ohos/react-native-orientation Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-orientation/releases)   | 0.72       |
| 3.2.0             | [@react-native-ohos/react-native-orientation Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-orientation/releases)   | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：


<!-- tabs:start -->

####  npm

```bash
npm install @react-native-ohos/react-native-orientation
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-orientation
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx

import Orientation from 'react-native-orientation';
import {Alert, StyleSheet, Text, TouchableOpacity, View} from 'react-native';
import {useEffect, useState} from 'react';

export default function OrientationDemo() {
  const [orientation, setOrientation] = useState<string>();
  const [SpecificOrientation, setSpecificOrientation] = useState<string>();
  const updateOrientation = (orientation: string) => {
    console.info('orientation', orientation);
    setOrientation(orientation);
  };
  const UpdateSpecificOrientation = (SpecificOrientation: string) => {
    console.info('SpecificOrientation', SpecificOrientation);
    setSpecificOrientation(SpecificOrientation);
  };
  useEffect(() => {
    // 开启方向变化的监听
    Orientation.addOrientationListener(updateOrientation);
    Orientation.addSpecificOrientationListener(UpdateSpecificOrientation);
    return () => {
     // 移除方向变化的监听
      Orientation.removeOrientationListener(updateOrientation);
      Orientation.removeSpecificOrientationListener(UpdateSpecificOrientation);
    };
  }, []);
  // 获取方向
  const getOrientationInt = () => {
    Orientation.getOrientation((err: string, orientation: string) => {
      if (orientation) {
        Alert.alert(`当前屏幕方向为${orientation}`);
      } else {
        Alert.alert(err);
      }
    });
  };
  // 获取具体方向
  const getSpecificOrientationInt = () => {
    Orientation.getSpecificOrientation((err: string, orientation: string) => {
      if (orientation) {
        Alert.alert(`当前屏幕方向为${orientation}`);
      } else {
        Alert.alert(err);
      }
    });
  };
  // 锁定方向为纵向（竖屏）
  const setLockToPortrait = () => {
    Orientation.lockToPortrait();
  };
  // 锁定方向为横向（横屏）
  const setLockToLandscape = () => {
    Orientation.lockToLandscape();
  };
  // 锁定方向为横向，并且是向左旋转的方向
  const setLockToLandscapeLeft = () => {
    Orientation.lockToLandscapeLeft();
  };
  // 锁定方向为横向，并且是向右旋转的方向
  const setLockToLandscapeRight = () => {
    Orientation.lockToLandscapeRight();
  };
  // 解除方向的锁定，允许自由旋转
  const unlockAllOrientations = () => {
    Orientation.unlockAllOrientations();
  };
  return (
    <View style={styles.container}>
      <Text>{`Current Orientation: ${orientation}`}</Text>
      <Text>{`Current SpecificOrientation: ${SpecificOrientation}`}</Text>
      <TouchableOpacity onPress={getOrientationInt} style={styles.button}>
        <Text style={styles.instructions}>获取当前屏幕的方向</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={getSpecificOrientationInt}
        style={styles.button}>
        <Text style={styles.instructions}>获取当前屏幕具体的方向</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToPortrait} style={styles.button}>
        <Text style={styles.instructions}>锁定当前屏幕为竖屏</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToLandscape} style={styles.button}>
        <Text style={styles.instructions}>锁定当前屏幕为横屏</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToLandscapeLeft} style={styles.button}>
        <Text style={styles.instructions}>锁定当前屏幕为横屏,左旋转</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToLandscapeRight} style={styles.button}>
        <Text style={styles.instructions}>锁定当前屏幕为横屏,右旋转</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={unlockAllOrientations} style={styles.button}>
        <Text style={styles.instructions}>解锁当前屏幕旋转锁定</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'flex-start',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
    marginTop: 20,
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#eeeeee',
    marginBottom: 0,
  },
  buttonContainer: {
    flex: 0,
    flexDirection: 'row',
    justifyContent: 'space-around',
  },
  button: {
    padding: 5,
    margin: 5,
    borderWidth: 1,
    borderColor: 'white',
    borderRadius: 3,
    backgroundColor: 'grey',
  },
});


```
## 使用 Codegen 

Version >= @react-native-ohos/react-native-orientation@3.1.4，已适配codegen-lib生成桥接代码。

本库已经适配了 Codegen ，在使用前需要主动执行生成三方库桥接代码，详细请参考 [Codegen 文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-orientation@3.1.4，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides字段

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

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）;
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-orientation": "file:../../node_modules/@react-native-ohos/react-native-orientation/harmony/rn_orientation.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 3.配置 CMakeLists 和引入 RNOrientationPackage

> [!TIP] 版本 `3.2.0` 及以上需要

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-orientation/src/main/cpp" ./rn_orientation)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_orientation)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNOritentionPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNOritentionPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 RNOrientationPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNOrientationPackage } from '@react-native-ohos/react-native-orientation/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNOrientationPackage(ctx)
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

在以下版本验证通过：

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-orientation](https://github.com/yamill/react-native-orientation?tab=readme-ov-file#api)

| Name           | Description                              | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | ---------------------------------------- | ------ | -------- | ----------- | ----------------- |
| lockToPortrait  | 锁定应用程序的方向为纵向（portrait）         | function | no       | IOS/Android | yes               |
| lockToLandscape  | 锁定应用程序的方向为横向（landscape）         | function | no       | IOS/Android | yes               |
| lockToLandscapeLeft  | 锁定应用程序的方向为横向并向左旋转         | function | no       | IOS/Android | yes               |
| lockToLandscapeRight  | 锁定应用程序的方向为横向并向右旋转         | function | no       | IOS/Android | yes               |
| unlockAllOrientations  | 解锁应用程序的方向，允许设备自由旋转         | function | no       | IOS/Android | yes               |
| getOrientation  | 获取当前设备的方向        | callback | no       | IOS/Android | yes               |
| getSpecificOrientation  | 获取当前设备的具体方向        | callback | no       | IOS/Android | yes               | 

## Events

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-orientation](https://github.com/yamill/react-native-orientation?tab=readme-ov-file#orientation-events)

| Name           | Description                              | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | ---------------------------------------- | ------ | -------- | ----------- | ----------------- |
| addOrientationListener  | 启用监听屏幕方向变化事件         | callback | no       | IOS/Android | yes               |
| addSpecificOrientationListener  | 开始监听屏幕具体方向变化事件 | callback | no       | IOS/Android | yes               |
| removeOrientationListener  | 移除监听屏幕方向变化事件    | callback | no       | IOS/Android | yes               |
| removeSpecificOrientationListener  | 移除监听屏幕具体方向变化事件        | callback | no       | IOS/Android | yes               |
## 其他

## 开源协议

本项目基于 [ISC License](https://github.com/yamill/react-native-orientation/blob/master/LICENSE.md) ，请自由地享受和参与开源。