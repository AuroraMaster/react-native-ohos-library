> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-exception-handler</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/a7ul/react-native-exception-handler">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/a7ul/react-native-exception-handler/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-exception-handler)

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-exception-handler`，具体版本所属关系如下：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.10.10    | [@react-native-oh-tpl/react-native-exception-handler Releases](https://github.com/react-native-oh-library/react-native-exception-handler/releases) | 0.72       |
| 2.11.0     | [@react-native-ohos/react-native-exception-handler Releases]() | 0.77       |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-exception-handler

# 0.77
npm install @react-native-ohos/react-native-exception-handler
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-exception-handler

# 0.77
yarn add @react-native-ohos/react-native-exception-handler
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

To catch <b>JS_Exceptions</b>

```typescript
import { View, Button } from "react-native";
import { setJSExceptionHandler, getJSExceptionHandler } from "react-native-exception-handler";

export const ReactNativeExceptionHandler = () => {

    const exceptionhandler = (error, isFatal) => {
        // your error handler function
    };

    const setJSExceptionHandlerClick = () => {
        setJSExceptionHandler(exceptionhandler, true);
    }

    const getJSExceptionHandlerClick = () => {
        // getJSExceptionHandler gives the currently set JS exception handler
        const currentHandler = getJSExceptionHandler();
    }

    return (
        <View style={{ flexDirection: "column", justifyContent: "space-between" }}>
            <Button
                title="setJSExceptionHandler"
                onPress={setJSExceptionHandlerClick}
            />
            <Button
                title="getJSExceptionHandler"
                onPress={getJSExceptionHandlerClick}
            />
        </View>
    );
};
```

To catch <b>Native_Exceptions</b>

```typescript
import { View, Button } from "react-native";
import { setNativeExceptionHandler } from "react-native-exception-handler";

export const ReactNativeExceptionHandler = () => {

    const exceptionhandler = (exceptionString) => {
        // your exception handler code here
    };

    const setNativeExceptionHandlerClick = () => {
        setNativeExceptionHandler(
            exceptionhandler,
            forceAppQuit,
            executeDefaultHandler
        );
        // - exceptionhandler is the exception handler function
        // - forceAppQuit is an optional ANDROID specific parameter that defines
        //    if the app should be force quit on error.  default value is true.
        //    To see usecase check the common issues section.
        // - executeDefaultHandler is an optional boolean (both IOS, ANDROID)
        //    It executes previous exception handlers if set by some other module.
        //    It will come handy when you use any other crash analytics module along with this one
        //    Default value is set to false. Set to true if you are using other analytics modules.
    }

    return (
        <View style={{ flexDirection: "column", justifyContent: "space-between" }}>
            <Button
                title="setNativeExceptionHandler"
                onPress={setNativeExceptionHandlerClick}
            />
        </View>
    );
};
```

##  使用 Codegen

> [!TIP]  0.72 不需要执行 Codegen。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](https://gitee.com/react-native-oh-library/usage-docs/blob/39316eccca7657d77dfdc9e90cfbf64e6a7713f3/zh-cn/codegen.md)。

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

-  0.72

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-exception-handler": "file:../../node_modules/@react-native-oh-tpl/react-native-exception-handler/harmony/exception_handler.har",
  }
```

-  0.77

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-ohos/react-native-exception-handler": "file:../../node_modules/@react-native-ohos/react-native-exception-handler/harmony/exception_handler.har",
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

### 3.配置 CMakeLists 和引入 ExceptionHandlerPackage

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

#  0.72

+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-exception-handler/src/main/cpp" ./exception-handler)

#  0.77

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-exception-handler/src/main/cpp" ./exception-handler)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_exception_handler)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ExceptionHandlerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ExceptionHandlerPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 ExceptionHandlerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：
-  0.72
```diff
    ...
+   import {ExceptionHandlerPackage} from '@react-native-oh-tpl/react-native-exception-handler/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ExceptionHandlerPackage(ctx)
  ];
}
```
-  0.77
```diff
    ...
+   import {ExceptionHandlerPackage} from '@react-native-ohos/react-native-exception-handler/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ExceptionHandlerPackage(ctx)
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

在下述版本验证通过：

RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release SDK；IDE：DevEco Studio  6.0.0.868; ROM：6.0.0.112; 

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                    | Description          | Type     | Required | Platform | HarmonyOS Support |
| ----------------------- | -------------------- | -------- | -------- | -------- | ----------------- |
| `setJSExceptionHandler` | 设置 JS 异常处理方法 | function | no       | Android, iOS      | yes               |
| `getJSExceptionHandler` | 获取 JS 异常处理方法 | function | no       | Android, iOS      | yes               |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                        | Description              | Type     | Required | Platform | HarmonyOS Support |
| --------------------------- | ------------------------ | -------- | -------- | -------- | ----------------- |
| `setNativeExceptionHandler` | 设置 native 异常处理方法 | function | no       | Android, iOS      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/a7ul/react-native-exception-handler/blob/master/LICENSE) ，请自由地享受和参与开源。
