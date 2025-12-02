<!--{%raw%}-->
> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>@remobile/react-native-toast</code> </h1>
</p>

本项目基于 [react-native-toast@1.0.7](https://github.com/remobile/react-native-toast) 开发。

请到三方库的 Releases发布地址查看配套的版本信息：

| Version                        | Package Name                                  | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
|1.0.7@deprecated  | @react-native-oh-tpl/react-native-toast | [Github](https://github.com/react-native-oh-library/react-native-toast) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-toast/releases) | 0.72 |
|  1.0.8           | @react-native-ohos/react-native-toast   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-toast) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-toast/releases) | 0.72 |
|  1.1.0           | @react-native-ohos/react-native-toast   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-toast) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-toast/releases) | 0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-toast
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-toast
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, {Component} from 'react';
import {Text, View, Button} from 'react-native';
import Toast from '@remobile/react-native-toast';

function ToastMasterDemo() {
    return (
        <View style={{flex: 2, justifyContent: 'center', alignItems: 'center'}}>
            <Text>Tosat !</Text>
            <Button
                title={'show toast'}
                onPress={() => {
                    Toast.show('This is a toast.');
                }}
            />
            <Button
                title={'short top toast'}
                onPress={() => {
                    Toast.showShortTop('This is a top toast.');
                }}
            />
            <Button
                title={'short center toast'}
                onPress={() => {
                    Toast.showShortCenter('This is a center toast.');
                }}
            />
            <Button
                title={'short bottom toast'}
                onPress={() => {
                    Toast.showShortBottom('This is a bottom toast.');
                }}
            />
            <Button
                title={'long top toast'}
                onPress={() => {
                    Toast.showLongTop('This is a long top toast.');
                }}
            />
            <Button
                title={'long center toast'}
                onPress={() => {
                    Toast.showLongCenter('This is a long center toast.');
                }}
            />
            <Button
                title={'long bottom toast'}
                onPress={() => {
                    Toast.showLongBottom('This is a long bottom toast.');
                }}
            />
        </View>
    );
}

export default ToastMasterDemo;

```

## 使用 Codegen

> [!TIP] V1.0.8 不需要执行 Codegen。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-toast@1.0.8，已支持 Autolink，无需手动配置，目前只支持72框架。
Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的HarmonyOS工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony": "./react_native_openharmony"
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
"@react-native-ohos/react-native-toast": "file:../../node_modules/@react-native-ohos/react-native-toast/harmony/rn_toast.har"
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

### 3.在 ArkTs 侧引入 ToastPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {ToastPackage} from '@react-native-ohos/react-native-toast/ts';
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ToastPackage(ctx)
  ];
}
```

### 4.配置 CMakeLists 和引入 ToastPackage

> [!TIP] 若使用的是V 1.0.7 版本，请跳过本章

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-toast/src/main/cpp" ./toast)

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
+ target_link_libraries(rnoh_app PUBLIC rn_toast)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ToastPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ToastPackage>(ctx),
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

本文档内容基于以下环境验证通过：

1. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- |---------| -------- | ------------------ |
| show()  | 显示Toast的位置、持续时间和消息内容 | function  | no     | android      | yes |
| showShortTop()  | 短时间显示顶部Toast | function  | no     | android      | yes |
| showShortCenter()  | 短时间显示居中Toast | function  | no     | android      | yes |
| showShortBottom()  | 短时间显示底部Toast | function  | no     | android      | yes |
| showLongTop()  | 长时间显示顶部Toast | function  | no     | android      | yes |
| showLongCenter()  | 长时间显示居中Toast | function  | no     | android      | yes |
| showLongBottom()  | 长时间显示底部Toast | function  | no     | android      | yes |
| hide()  | 隐藏正在显示的Toast         | function  | no      | android      | no |

## 遗留问题

- arkui侧的toast的hide()方法暂时没有[issue#3](https://github.com/react-native-oh-library/react-native-toast/issues/3)

## 其他

## 开源协议

本项目基于 [The MIT License](https://github.com/remobile/react-native-toast/blob/master/LICENSE)，请自由地享受和参与开源。

<!--{%endraw%}-->
