> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-shake</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Doko-Demo-Doa/react-native-shake">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Doko-Demo-Doa/react-native-shake/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-shake)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本    | 发布信息                                                     | 支持RN版本 |
| ------------- | ------------------------------------------------------------ | ---------- |
| <= 5.6.2-0.0.1@deprecated  | [@react-native-oh-tpl/react-native-shake Releases(deprecated)](https://github.com/react-native-oh-library/react-native-shake/releases) | 0.72       |
| 5.6.3             | [@react-native-ohos/react-native-shake Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-shake/releases)           | 0.72       |
| 6.0.2             | [@react-native-ohos/react-native-shake Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-shake/releases)           | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。


进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-shake
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-shake
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from 'react';
import { Text, View, StyleSheet } from 'react-native'
import RNShake from 'react-native-shake';

export function ShakeExample() {
    const [result, setResult] = useState<string>('')
    myComponent(setResult)
    return (
      <View style={styles.container}>
      <Text style={styles.title}>shake（摇晃手机）</Text>
      <Text style={styles.resultText}>{result}</Text>
  </View>
    )
}

export const myComponent = (setResult: React.Dispatch<React.SetStateAction<string>>) => {
    React.useEffect(() => {
        const subscription = RNShake.addListener(() => {
            setResult('shake listen success')
        })
        return () => {
            subscription.remove()
        }
    }, [])
}

const styles = StyleSheet.create({
  container: {
      flex: 1,
      backgroundColor: 'white',
      width: '100%',
      justifyContent: 'center',
      alignItems: 'center',
      padding: 20
  },
  title: {
      fontSize: 18,
      fontWeight: 'bold',
      marginBottom: 15,
      textAlign: 'center'
  },
  resultText: {
      fontSize: 16,
      color: '#2196F3',
      textAlign: 'center',
      marginTop: 10
  }
});
```


## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~6.0.2                               |  No              |  0.77     |
| ~5.6.3                               |  Yes             |  0.72     |
| <= 5.6.2-0.0.1@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

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

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-shake": "file:../../node_modules/@react-native-ohos/react-native-shake/harmony/shake_package.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)。


### 3.在 ArkTs 侧引入 ShakePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { ShakePackage } from "@react-native-ohos/react-native-shake/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ShakePackage(ctx)
  ];
}
```

### 4.配置 CMakeLists 和引入 ShakePackge

> 若使用的是 <= 5.6.2-0.0.1 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-shake/src/main/cpp" ./shake_package)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_shake)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ShakePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ShakePackage>(ctx)
    };
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

### 权限要求

此库接口需要normal权限：ohos.permission.ACCESS_BLUETOOTH，权限需配置在entry/src/main目录下module.json5文件中

```
 "requestPermissions": [
      {
        "name": "ohos.permission.ACCELEROMETER"
      }
    ]
```

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `addListener` | 添加摇一摇事件监听 | function | yes | ios/andriod | yes |
| `removeAllListeners` | 移除事件监听 | function | yes | ios/andriod | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/Doko-Demo-Doa/react-native-shake/blob/main/LICENSE) ，请自由地享受和参与开源。