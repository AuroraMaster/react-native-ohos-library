> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-immersive</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mockingbot/react-native-immersive">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20hormony-blue
" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mockingbot/react-native-immersive/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-immersive)

请到三方库的 Releases 发布地址查看配套的版本信息：

| version | Package name                              | Releases info                                                | Support RN version |
| ------- | ----------------------------------------- | ------------------------------------------------------------ | ------------------ |
| 2.1.0   | @react-native-ohos/react-native-immersive | [@react-native-ohos/react-native-immersive Releases](https://github.com/react-native-oh-library/react-native-immersive/releases) | 0.72/0.77          |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-immersive
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-immersive
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from 'react'
import { AppRegistry, StyleSheet, Text, View, Button, TextInput, Alert, Modal } from 'react-native'
import { Immersive } from 'react-native-immersive'

class testReactNative extends Component {
  constructor (props) {
    super(props)
    
    Immersive.getImmersive().then((immersiveState) => {
        console.log('init [getImmersiveState]', immersiveState)
        this.setState({ immersiveState,isImmersive: immersiveState.isImmersiveOn })
        if(immersiveState.isImmersiveOn){
          Immersive.on()
        }
      }).catch((err) => {
        console.error('[getImmersiveState] error', err)
   })

    this.setImmersiveOn = () => {
      let startTime = Date.now();
      Immersive.on()
      let endTime = Date.now();
      console.log("react-native-immersive on time:", endTime - startTime, "ms");
      this.setState({ isImmersive: true })
    }
    this.setImmersiveOff = () => {
      let startTime = Date.now();
      Immersive.off()
      let endTime = Date.now();
      console.log("react-native-immersive off time:", endTime - startTime, "ms");
      this.setState({ isImmersive: false })
    }
    this.setImmersiveTrue = () => {
      let startTime = Date.now();
      Immersive.setImmersive(true)
      let endTime = Date.now();
      console.log("react-native-immersive setImmersive time:", endTime - startTime, "ms");
      this.setState({ isImmersive: true })
    }
    this.setImmersiveFalse = () => {
      Immersive.setImmersive(false)
      this.setState({ isImmersive: false })
    }
    this.addImmersiveListener = () => {
      if(!this.state.isAddListener){
        console.log("Immersive---------> addImmersiveListener",this.restoreImmersive);
        let startTime = Date.now();
        Immersive.addImmersiveListener(this.restoreImmersive)
        let endTime = Date.now();
        console.log("react-native-immersive addImmersiveListener time:", endTime - startTime, "ms");
        this.setState({ isAddListener: true })
      }
    }
    this.removeImmersiveListener = () => {
      if(this.state.isAddListener){
        console.log("Immersive---------> removeImmersiveListener",this.restoreImmersive);
        let startTime = Date.now();
        Immersive.removeImmersiveListener(this.restoreImmersive)
        let endTime = Date.now();
        console.log("react-native-immersive removeImmersiveListener time:", endTime - startTime, "ms");
        this.setState({ isAddListener: false })
      }
    }

  
    this.getImmersiveState = () => {
      let startTime = Date.now();
      Immersive.getImmersive().then((immersiveState) => {
        let endTime = Date.now();
        console.log("react-native-immersive getImmersive time:", endTime - startTime, "ms");
        console.log('[getImmersiveState]', immersiveState)
        this.setState({ immersiveState })
      }).catch((err) => {
        console.error('[getImmersiveState] error', err)
      })
    }

    this.restoreImmersive = () => {
      Alert.alert("Callback","The registered listener callback has been invoked")
    }

    this.state = {
      isAddListener: false,
      isImmersive: false,
      isRestoreImmersive: true,
      immersiveState: null
    }
  }

  render () {
    const { isImmersive, immersiveState } = this.state
    return (
      <View style={{margin: 16}}>
            <Button onPress={this.addImmersiveListener} title="addImmersiveListener" />
            <View style={{ marginTop: 10, marginBottom: 10 }}>
                <Button style={{marginTop: 10, marginBottom: 10}} onPress={this.removeImmersiveListener} title="removeImmersiveListener" />
            </View>
            <Button onPress={isImmersive ? this.setImmersiveOff : this.setImmersiveOn} title="on/off" />
            <Text style={styles.text}>isImmersive: {JSON.stringify(isImmersive)}</Text>
            <View style={{ marginTop: 10, marginBottom: 10 }}>
              <Button onPress={isImmersive ? this.setImmersiveFalse : this.setImmersiveTrue} title="setImmersive" />
            <Text style={styles.text}>isImmersive: {JSON.stringify(isImmersive)}</Text>
            </View>
            <Button onPress={this.getImmersiveState} title="getImmersive" />
            <Text style={styles.text}>immersiveState: {JSON.stringify(immersiveState)}</Text>
      </View>
    )
  }
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 24 },
  containerTest: { alignItems: 'stretch', justifyContent: 'center', flex: 1 },
  text: { textAlign: 'center', fontSize: 14 }
})

export default testReactNative;
AppRegistry.registerComponent('testReactNative', () => testReactNative)
```

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

```json
"dependencies": {
   ...
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-immersive": "file:../../node_modules/@react-native-ohos/react-native-immersive/harmony/immersive.har",
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

### 3.配置 CMakeLists 和引入 RNCVideoPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-immersive/src/main/cpp" ./rnoh_immersive)

# RNOH_BEGIN: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_immersive)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNImmersivePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNImmersivePackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNCVideoPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNImmersivePackage } from '@react-native-ohos/react-native-immersive/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNImmersivePackage(ctx)
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

## 6.约束与限制

兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过。

1. RNOH: 0.72.79; SDK: HarmonyOS 5.1.1 Release SDK; IDE: DevEco Studio 5.1.1 Release; ROM: 5.0.1.120;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;


## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 Android 的效果。

| Name                      | Description  | Type     | Required | Platform | HarmonyOS Support |
| ------------------------- | ------------ | -------- | -------- | -------- | ----------------- |
| `on()`                    | 设置全屏     | function | No       | Android  | yes               |
| `off()`                   | 关闭全屏     | function | No       | Android  | yes               |
| `setImmersive()`          | 设置全屏状态 | function | No       | Android  | yes               |
| `getImmersive()`          | 获取全屏状态 | function | No       | Android  | yes               |
| `addImmersiveListener()`  | 添加监听     | function | No       | Android  | yes               |
| removeImmersiveListener() | 取消监听     | function | No       | Android  | yes               |

## 遗留问题

不涉及

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mockingbot/react-native-immersive/blob/master/LICENSE) ，请自由地享受和参与开源。