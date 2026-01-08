> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-nitro-modules</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mrousavy/nitro/tree/main/packages/react-native-nitro-modules">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mrousavy/nitro/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Gitcode 地址](https://gitcode.com/OpenHarmony-RN/rntpc_react-native-nitro-modules/tree/dev-0.31.10)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息 | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.31.11     | [@react-native-ohos/react-native-nitro-modules Releases](https://gitcode.com/OpenHarmony-RN/rntpc_react-native-nitro-modules/tree/dev-0.31.10) | 0.77     |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-nitro-modules
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-nitro-modules
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```ts
import React from 'react';
import { View, Text, Pressable, StyleSheet } from 'react-native';
import type {TurboModule} from 'react-native/Libraries/TurboModule/RCTExport';
import {TurboModuleRegistry} from 'react-native';
import { type HybridObject, NitroModules } from 'react-native-nitro-modules'

interface Math extends HybridObject<{}> {
    add(a: number, b: number): number
}

export interface Spec extends TurboModule {
    install(): void;
}

const PlatformConstants	= TurboModuleRegistry.get<Spec>('NitroModules');
if(PlatformConstants) {
    PlatformConstants.install()
}

const App = () => {
  const handleButtonClick = () => {
    const math = NitroModules.createHybridObject<Math>("Math")
    const result = math.add(15, 7) // --> 22
    console.info("result:", result) 
  };

  return (
    <View style={styles.container}>
      <Text style={styles.text}>Hello React Native TSX!</Text>
      <View style={styles.buttonWrapper}>
        <Pressable
          onPress={handleButtonClick}
          style={styles.button}
          android_ripple={{ color: '#ccc' }}
        >
          <Text style={styles.buttonText}>add</Text>
        </Pressable>
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f5f5f5',
  },
  text: {
    fontSize: 18,
    color: '#333',
    marginBottom: 20,
  },
  buttonWrapper: {
    paddingVertical: 20,
    paddingHorizontal: 20,
  },
  button: {
    paddingVertical: 8,
    paddingHorizontal: 16,
    backgroundColor: '#007AFF',
    borderRadius: 4,
  },
  buttonText: {
    fontSize: 16,
    color: '#fff',
    textAlign: 'center',
  },
});

export default App;
```
## Link

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json` 添加 overrides字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
  ...
}
```

### 2.引入原生端代码

当前有两种方式：

- 通过 HAR 包导入（IDE 功能完善后将废弃，目前推荐使用此方式）；
- 直接链接源码。

方式一：通过 HAR 包导入（推荐）
> [!TIP] HAR 包位于三方库安装目录的 harmony 子文件夹中。

打开 entry/oh-package.json5 文件并追加以下依赖项：

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-nitro-modules": "file:../../node_modules/@react-native-ohos/react-native-nitro-modules/harmony/nitro_modules.har"
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

### 3.CPP侧配置 CMakeLists、引入 NitroModulesPackage、注册HybridObject、新增HybridMath.hpp和HybridMath.cpp文件

open entry/src/main/cpp/CMakeLists.txt，add：

```diff
include(FetchContent)
# BOOST
set(BOOST_ENABLE_CMAKE On)
FetchContent_Declare(
 Boost
 URL /7277/boost-1.82.0.tar.xz
 OVERRIDE_FIND_PACKAGE)
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)


add_subdirectory("${RNOH_CPP_DIR}" ./rn)

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-nitro-modules/src/main/cpp" ./nitro_modules)

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
+    "./HybridMath.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

+ target_link_libraries(rnoh_app PUBLIC rnoh_nitro_modules)
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
+ #include "NitroModulesPackage.h"
+ #include "HybridObjectRegistry.hpp"
+ #include "HybridMath.hpp"

using namespace rnoh;
+ using namespace margelo::nitro;
+ using namespace margelo::nitro::test;
std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
+    HybridObjectRegistry::registerHybridObjectConstructor(
+        "Math", []() -> std::shared_ptr<HybridObject> { return std::make_shared<HybridMath>(); });
    return {
+       std::make_shared<NitroModulesPackage>(ctx),
    };
}
```
打开`entry/src/main/cpp/HybridMath.hpp`，添加：
```diff
+ #include "HybridObject.hpp"
+ namespace margelo::nitro::test {
+ class HybridMath: public HybridObject {
+ public:
+   HybridMath(): HybridObject(NAME) { }

+ public:
+   double add(double a, double b);

+ protected:
+   void loadHybridMethods() override;

+ private:
+   static constexpr auto NAME = "Math";
+ };
+ }
```
打开`entry/src/main/cpp/HybridMath.cpp`，添加：
```diff
+ #include "HybridMath.hpp"
+ namespace margelo::nitro::test {
+ double HybridMath::add(double a, double b) {
+   return a + b;
+ }
+
+ void HybridMath::loadHybridMethods() {
+   // register base methods (toString, ...)
+   HybridObject::loadHybridMethods();
+   // register custom methods (add)
+   registerHybrids(this, [](Prototype& proto) {
+     proto.registerHybridMethod(
+       "add",
+       &HybridMath::add
+     );
+   });
+ }
+ }
```
### 4.在 ArkTs 侧引入 NitroModulesPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { NitroModulesPackage } from '@react-native-ohos/react-native-nitro-modules/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new NitroModulesPackage(ctx)
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

要使用此库，需要使用正确的 React-Native 和 RNOH 版本

本文档内容基于以下版本验证通过：
1. RNOH：0.77.33; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## API
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                    | Description                                  | Type     | Required | Platform    | HarmonyOS Support |
| ----------------------- | -------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| buildType     | 获取在 `NITRO_DEBUG` 中定义的当前构建类型配置          | property | No      | iOS/Android | yes               |
| hasHybridObject    | 返回指定@linkcode name的HybridObject是否已注册       | function | No      | iOS/Android | yes               |
| isHybridObject | 返回给定的@linkcode object是否为@linkcode HybridObject                | function | No      | iOS/Android | yes               |
| getAllHybridObjectNames | 获取所有已注册混合对象的列表                | function | No      | iOS/Android | yes               |
| version | 获取此应用所构建使用的原生Nitro Modules核心运行时版本                | property | No      | iOS/Android | yes               |
| box | 将给定的@linkcode hybridObject装箱为@linkcode BoxedHybridObject，之后可以在单独的运行时中将其拆箱                | function | No      | iOS/Android | yes               |
| unbox | 表示一个装箱的@linkcode HybridObject，之后可以再次拆箱                | function | No      | iOS/Android | yes               |
| hasNativeState | 返回给定的@linkcode object是否具有NativeState                | function | No      | iOS/Android | yes               |
| updateMemorySize | 重新计算给定@linkcode HybridObject的`memorySize`，并通知JS虚拟机更新后的内存占用情况                | function | No      | iOS/Android | yes               |
| AnyHybridObject | 表示基础 `HybridObject` 类型的值，所有其他 HybridObjects 均继承自它                | interface | No      | iOS/Android | yes               |
| getHybridObjectConstructor | 获取给定 `HybridObject` @linkcode T 的构造函数               | function | No      | iOS/Android | yes               |
| toString | 返回给定`HybridObject`的字符串表示形式                | function | No      | iOS/Android | yes               |
| name | 混合对象的名称               | property | No      | iOS/Android | yes               |
| equals | 返回此 `HybridObject` 是否与 @linkcode other 是同一个对象                | function | No      | iOS/Android | yes               |
| dispose | 释放此@linkcode HybridObject可能持有的任何原生资源，并释放此@linkcode HybridObject的`NativeState`                | function | No      | iOS/Android | yes               |
| CustomType | 表示一种自定义的、手动编写的本地类型                | type | No      | iOS/Android | yes               |
| Sync | 将给定函数标记为同步函数，使其能够在同一线程上同步调用                | type | No      | iOS/Android | yes               |
| createHybridObject | 创建 `HybridObject` @linkcode T 的新实例                | function | No      | iOS/Android | yes               |
| HybridView | 表示Nitro混合视图               | type | No      | iOS/Android | no               |
| getHostComponent | 通过给定的@linkcode name查找并返回原生视图（即“HostComponent”）              | function | No      | iOS/Android | no               |

## 遗留问题
## 其他

- react-native-nitro-modules库没有依赖react-native 0.72的版本，HybridView和getHostComponent用于构建Hybrid Views，至少需要react-native 0.78的版本

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mrousavy/nitro/blob/main/LICENSE) ，请自由地享受和参与开源。

