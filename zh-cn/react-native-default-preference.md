> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-default-preference</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/kevinresol/react-native-default-preference">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/kevinresol/react-native-default-preference/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-default-preference)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 1.4.4-0.0.1@deprecated      | [@react-native-oh-tpl/react-native-default-preference Releases](https://github.com/react-native-oh-library/react-native-default-preference/releases) | 0.72       |
| 1.4.5      | [@react-native-ohos/react-native-default-preference Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-default-preference/releases)     | 0.72       |
| 1.5.0      | [@react-native-ohos/react-native-default-preference Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-default-preference/releases) | 0.77       |


对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash

npm install @react-native-ohos/react-native-default-preference
```

#### **yarn**

```bash

yarn add @react-native-ohos/react-native-default-preference
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { Text, View } from "react-native";
import DefaultPreference from 'react-native-default-preference';

const App = () => {
    const handleSetItem = useCallback((key: string, value:  string) => {
        RNDefaultPreference.set(key, value)
    }, []);

    const handleGetItem = useCallback((key: string) => {
        RNDefaultPreference?.get(key).then(res => {
            console.log(res)
        });
    }, []);
  return (
      <View>
        <Button onPress={async () => { handleSetItem('key1', 'value1') }} title={'Add item using setItem'}></Button>
        <Button onPress={async () => { handleGetItem('key1') }} title={'Add item using setItem'}></Button>
     </View>
  );
};

export default App;
```

## 使用 Codegen



本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|------------------|-----------|
| ~1.5.0                               |  No              |  0.77     |
| ~1.4.5                               |  Yes             |  0.72     |
| <= 1.4.4-0.0.1@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md。

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

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
    "@react-native-ohos/react-native-default-preference": "file:../../node_modules/@react-native-ohos/react-native-default-preference/harmony/react_native_default_preference.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/link-source-code.md)

### 3.配置 CMakeLists 和引入 DefaultPreferencePackage

> 若使用的是 <= 1.4.4-0.0.1 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```
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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-default-preference/src/main/cpp" ./default_preference)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_default_preference)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "DefaultPreferencePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<DefaultPreferencePackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 RNDefaultPreferencePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...

+ import { RNDefaultPreferencePackage } from '@react-native-ohos/react-native-default-preference/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNDefaultPreferencePackage(ctx)
  ];
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

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name          | Description                   | Type     | Required | Platform     | HarmonyOS Support |
| ------------- | ----------------------------- | -------- | -------- | ------------ | ----------------- |
| get           | 取出键值对                    | function | yes      | Android、iOS | yes               |
| set           | 设置键值对                    | function | yes      | Android、iOS | yes               |
| clear         | 清除键值对                    | function | yes      | Android、iOS | yes               |
| getMultiple   | 取出多个键值对                | function | yes      | Android、iOS | yes               |
| setMultiple   | 设置多个键值对                | function | yes      | Android、iOS | yes               |
| clearMultiple | 清除多个键值对                | function | yes      | Android、iOS | yes               |
| getAll        | 取出所有键值对                | function | no       | Android、iOS | yes               |
| clearAll      | 清除所有键值对                | function | no       | Android、iOS | yes               |
| getName       | 获取 Preferences 实例的名称。 | function | no       | Android、iOS | yes               |
| setName       | 设置 Preferences 实例的名称。 | function | yes      | Android、iOS | yes               |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/kevinresol/react-native-default-preference/blob/master/LICENSE) ，请自由地享受和参与开源。
