> 模板版本：v0.4.0

<p align="center">
  <h1 align="center"> <code>react-native-orientation-locker</code> </h1>
</p>

本项目基于 [react-native-orientation-locker](https://github.com/wonday/react-native-orientation-locker) 开发。

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-orientation-locker` 版本所属关系如下：
| 三方库名称    | 三方库版本    | 发布信息     | 支持RN版本    | Autolink     | 编译API版本     | 社区基线版本    | npm地址                |
| ------------ | ------------ | ------------------------------ | ------------- | ------------- |------------------------ | ------------- | ------------- |
| @react-native-ohos/react-native-orientation-locker |  1.8.0   | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-orientation-locker/releases) | 0.77 | 否 | API12+ | 1.7.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-orientation-locker) |
| @react-native-ohos/react-native-orientation-locker | 1.7.1   | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-orientation-locker/releases) | 0.72 | 是 | API12+ | 1.7.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-orientation-locker) | 
| @react-native-oh-tpl/react-native-orientation-locker | <= 1.7.0-0.0.7@deprecated    | [Github Releases](https://github.com/react-native-oh-library/react-native-orientation-locker/releases) | 0.72 | 否 | API12+ | 1.7.0 | [Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/react-native-orientation-locker) | 

    
## 1. 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/react-native-orientation-locker
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-orientation-locker
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx

import {
  Alert,
  Button,
  StyleSheet,
  Text,
  TouchableOpacity,
  View,
} from 'react-native';
import {useCallback, useEffect, useState} from 'react';
import Orientation, {
  OrientationLocker,
  PORTRAIT,
  LANDSCAPE,
  useOrientationChange,
  useDeviceOrientationChange,
  useLockListener,
} from 'react-native-orientation-locker';
import React from 'react';

export function OrientationLockerExample() {
  const [showVideo, setShowVideo] = useState(true);
  const [orientation, setOrientation] = useState<string>();
  const [isLock, setIsLock] = useState<boolean>(false);
  const updateOrientation = (orientation: string) => {
    console.info('---orientation-----22222', orientation);
    setOrientation(orientation);
  };

  const updateDeviceOrientation = (orientation: string) => {
    console.info('---updateDeviceOrientation-----1111111', orientation);
    setOrientation(orientation);
  };

  const updateLock = (orientation: string) => {
    console.info('---updateLock-----', orientation);
  };

  useEffect(() => {
    // 开启方向变化的监听
    getOrientationInt();
  }, []);


  //获取方向
  const getOrientationInt = () => {
    Orientation.getOrientation((orientation: string) => {
      updateOrientation(orientation);
      if (orientation) {
        Alert.alert(`当前屏幕方向为${orientation}`);
      } else {
        Alert.alert('获取当前屏幕方向失败');
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

  // 锁定上下的方向
  const lockToPortraitUpsideDown = () => {
    Orientation.lockToPortraitUpsideDown();
  };

  // 锁定除了上下的所有方向
  const lockToAllOrientationsButUpsideDown = () => {
    Orientation.lockToAllOrientationsButUpsideDown();
  };
  // 添加监听a
  const addTisten = () => {
    Orientation.addDeviceOrientationListener(updateDeviceOrientation);
  };
  // 取消监听
  const cancelAddTisten = () => {
    Orientation.removeDeviceOrientationListener(updateDeviceOrientation);
  };

  return (
    <View style={styles.container}>
      <Text>{`Current Orientation----: ${orientation}`}</Text>
      <TouchableOpacity
        onPress={lockToPortraitUpsideDown}
        style={styles.button}>
        <Text style={styles.instructions}>锁定上下的方向</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={lockToAllOrientationsButUpsideDown}
        style={styles.button}>
        <Text style={styles.instructions}>锁定除了上下的所有方向</Text>
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
      <TouchableOpacity onPress={addTisten} style={styles.button}>
        <Text style={styles.instructions}>添加监听</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={cancelAddTisten} style={styles.button}>
        <Text style={styles.instructions}>取消监听</Text>
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

## 2. Link

|                           | 是否支持autolink | RN框架版本 |
|---------------------------|--------------|--------|
| ~1.8.0                     | No           | 0.77   |
| ~1.7.1                     | Yes          | 0.72   |
| <= 1.7.0-0.0.7@deprecated | No           | 0.72   |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1. Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony"
  }
}
```

### 2.2. 引入原生端代码

目前有两种方法：

- 通过 har 包引入；
- 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-orientation-locker":"file:../../node_modules/@react-native-ohos/react-native-orientation-locker/harmony/orientation_locker.har"
}
```

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 2.3. 配置 CMakeLists 和引入 OrientationLockerPackage

> 若使用的是  <= 1.7.0-0.0.7 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-orientation-locker/src/main/cpp" ./orientation_locker)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_orientation_locker)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "OrientationLockerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<OrientationLockerPackage>(ctx),
    };
}
```

### 2.4. 在 ArkTs 侧引入 RNOrientationLockerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+  import { RNOrientationLockerPackage } from '@react-native-ohos/react-native-orientation-locker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new RNOrientationLockerPackage(ctx)
  ];
}
```
</details>

### 2.5. 运行

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1. 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### 3.2. 权限要求

由于此库获取加速度传感器的数据，使用时需要配置对应的权限，权限需配置在entry/src/main目录下module.json5 中添加如下权限:

```diff
...
"requestPermissions": [
...
+      {
+        "name": "ohos.permission.ACCELEROMETER"
+       }
    ]
```

## 4. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| -------------- | ---------------------------------------- | ------ | ------------------------  | ---------------- | ----------------- |
| lockToPortrait   |   Lock the orientation of the application to portrait (portrait)         |  function  | No       | IOS/Android | yes               |
| lockToLandscape  |    Lock the orientation of the application to landscape (landscape)         | function | No       | IOS/Android | yes               |
| lockToLandscapeLeft  | Lock the orientation of the app to landscape and rotated to the left         | function | No       | IOS/Android | yes               |
| lockToLandscapeRight  | Lock the orientation of the app to landscape and rotated to the right         | function | No       | IOS/Android | yes               |
| unlockAllOrientations  | Unlocks the orientation of the app, allowing the device to rotate freely          | function | No       | IOS/Android | yes               |
| getOrientation  | Get the direction of the current device        | callback | No       | IOS/Android | yes               |
| getDeviceOrientation  | Obtains the direction of the current device        | callback | No       | IOS/Android | yes               |

## 5. Events

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name   | Description                              | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | ---------------------------------------- | ------ | -------- | ----------- | ----------------- |
| addOrientationListener  | When UI orientation changed, callback function will be called. But if lockToXXX is called , callback function will be not called untill unlockAllOrientations. It can return either PORTRAIT LANDSCAPE-LEFT LANDSCAPE-RIGHT PORTRAIT-UPSIDEDOWN UNKNOWN When lockToXXX/unlockAllOrientations, it will force resend UI orientation changed event.| callback | No       | IOS/Android | yes               |
| addDeviceOrientationListener  | When device orientation changed, callback function will be called. When lockToXXX is called, callback function also can be called. It can return either PORTRAIT LANDSCAPE-LEFT LANDSCAPE-RIGHT PORTRAIT-UPSIDEDOWN UNKNOWN | callback | No       | IOS/Android | yes               |
| removeOrientationListener  | Remove a previously added screen orientation change listener   | callback | No       | IOS/Android | yes               |
| removeDeviceOrientationListener  |   Remove the event that monitors physical directional changes of the device      | callback | No       | IOS/Android | yes               |
| addLockListener  | When call lockToXXX/unlockAllOrientations, callback function will be called. It can return either PORTRAIT LANDSCAPE-LEFT LANDSCAPE-RIGHT UNKNOWN UNKNOWN means not be locked. | callback | No       | IOS/Android | yes               |
| removeLockListener  |  Remove the event that monitors changes in screen orientation lock status   | callback | No       | IOS/Android | yes              |
| removeAllListeners  |  Remove all listening events     | callback | No       | IOS/Android | yes              |


## 6. 遗留问题

## 7. 其他

## 8. 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wonday/react-native-orientation-locker/blob/master/LICENSE) ，请自由地享受和参与开源。
