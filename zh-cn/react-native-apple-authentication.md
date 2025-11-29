> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-apple-authentication</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/invertase/react-native-apple-authentication">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/invertase/react-native-apple-authentication/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache%202.0-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-apple-authentication)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.3.0@deprecated      | [@react-native-oh-tpl/react-native-apple-authentication Releases(deprecated)](https://github.com/react-native-oh-library/react-native-apple-authentication/releases) | 0.72       |
| 2.3.1      | [@react-native-ohos/react-native-apple-authentication Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-apple-authentication/releases) | 0.72       |
| 2.4.2      | [@react-native-ohos/react-native-apple-authentication Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-apple-authentication/releases) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-ohos/react-native-apple-authentication
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-apple-authentication
```

#### **配置用于 Web 的“通过 Apple 登录”**
首先需要进行客户端id配置：[Initial Development Environment Setup](https://github.com/invertase/react-native-apple-authentication/blob/main/docs/INITIAL_SETUP.md)

然后需要进行服务设置：[Services setup](https://github.com/invertase/react-native-apple-authentication/blob/main/docs/ANDROID_EXTRA.md)

Apple官方配置说明：[Configure Sign in with Apple for the web](https://developer.apple.com/help/account/configure-app-capabilities/configure-sign-in-with-apple-for-the-web)

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
import React from 'react';
import { appleAuthHarmony, AppleButton } from '@invertase/react-native-apple-authentication';

const AppleAuthenticationDemo: React.FC = (): JSX.Element => {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <AppleButton
                onPress={async () => {
                    appleAuthHarmony.configure({
                        // 以下配置请参考原库AppleId登录文档:
                        // https://github.com/invertase/react-native-apple-authentication/blob/main/docs/INITIAL_SETUP.md
                        // https://github.com/invertase/react-native-apple-authentication/blob/main/docs/ANDROID_EXTRA.md
                        clientId: 'com.example.client', 
                        redirectUri: 'https://example.com'
                    })
                    const singInRes = await appleAuthHarmony.signIn()
                    console.log(singInRes)
                }}
            />
        </View>
    )
}

export default AppleAuthenticationDemo;
```

## 使用 Codegen

> [!TIP] V2.3.1 不需要执行 Codegen。

本库已经适配了 Codegen ，在使用前需要主动执行生成三方库桥接代码，详细请参考 [Codegen 文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-apple-authentication@2.3.1，已支持 Autolink，无需手动配置，目前只支持72框架。
Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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
    "@react-native-ohos/react-native-apple-authentication": "file:../../node_modules/@react-native-ohos/react-native-apple-authentication/harmony/react-native-apple-authentication.har"
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

### 3.配置 CMakeLists 和引入 RNOHAppleAuthenticationPackage

> V2.3.1 需要配置 CMakeLists 和引入 RNOHAppleAuthenticationPackage。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

# (VM) Define a variable and assign it to the current module's cpp directory
set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})

# Add the Header File directory, including cpp, cpp/include, and tell cmake to find the Header Files introduced by the code here
include_directories(${NATIVERENDER_ROOT_PATH}
                    ${NATIVERENDER_ROOT_PATH}/include)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-apple-authentication/src/main/cpp" ./react-native-apple-authentication)
# RNOH_BEGIN: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "${CMAKE_CURRENT_SOURCE_DIR}/generated/*.cpp") # this line is needed by codegen v1

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)
+ target_link_libraries(rnoh_app PUBLIC rnoh_apple_authentication)

```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff

#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "RNOHAppleAuthenticationPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx)
{
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+ 			std::make_shared<RNOHAppleAuthenticationPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 RNAppleAuthPackage

打开 `entry/src/main/ets/RNPackagesFactory.ets`，添加：

```diff
  ...
+ import { RNAppleAuthPackage } from '@react-native-ohos/react-native-apple-authentication';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNAppleAuthPackage(ctx)
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

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.3.0@deprecated      | [@react-native-oh-tpl/react-native-apple-authentication Releases(deprecated)](https://github.com/react-native-oh-library/react-native-apple-authentication/releases) | 0.72       |
| 2.3.1      | [@react-native-ohos/react-native-apple-authentication Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-apple-authentication/releases) | 0.72       |
| 2.4.2      | [@react-native-ohos/react-native-apple-authentication Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-apple-authentication/releases) | 0.77       |

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.403; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH：0.77.18; SDK：HarmonyOS 5.1.1 Release; IDE: DevEco Studio 5.1.1.830; ROM：NEXT 5.1.0.150;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**AppleButton**：Apple身份验证按钮组件。

| Name         | Description        | Type                                                         | Required | Platform | HarmonyOS Support |
| ------------ | ------------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| style        | 按钮样式           | StyleProp< [ViewStyle](https://gitee.com/link?target=https%3A%2F%2Freactnative.dev%2Fdocs%2Fview%23props) > | no       | all      | yes               |
| textStyle    | 按钮内文字样式     | StyleProp< [TextStyle](https://gitee.com/link?target=https%3A%2F%2Freactnative.dev%2Fdocs%2Ftext%23props) > | no       | all      | yes               |
| cornerRadius | 按钮边框圆角弧度   | number                                                       | no       | all      | yes               |
| buttonStyle  | 按钮样式(预设枚举) | [AppleButtonStyle](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Finvertase%2Freact-native-apple-authentication%2Fblob%2Fmain%2Ftypedocs%2Fenums%2FAppleButtonStyle.md) | no       | all      | yes               |
| buttonType   | 按钮类型(预设枚举) | [AppleButtonType](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Finvertase%2Freact-native-apple-authentication%2Fblob%2Fmain%2Ftypedocs%2Fenums%2FAppleButtonType.md) | no       | all      | yes               |
| onPress      | 按钮点击事件       | () => void                                                   | yes      | all      | yes               |
| leftView     | 按钮内左侧图标     | ReactNode                                                    | no       | all      | yes               |
| buttonText   | 按钮内文字内容     | string                                                       | no       | all      | yes               |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**appleAuthHarmony**：Apple身份验证对象，包含2个方法。

| Name      | Description                                             | Type                                                         | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| configure | 配置 Apple 身份验证的信息，此接口必须在 signIn 之前调用 | ([Config](https://github.com/invertase/react-native-apple-authentication/blob/main/typedocs/interfaces/AndroidConfig.md)) => void | no       | all      | yes               |
| signIn    | 弹出 webview 以进行 Apple 身份验证                      | () => Promise< [SigninResponse](https://github.com/invertase/react-native-apple-authentication/blob/main/typedocs/interfaces/AndroidSigninResponse.md) > | no       | all      | no                |

## 其他

## 遗留问题

- [ ] 由于 Apple 开发者账户验证问题，HarmonyOS暂无法实现的接口：[issue#1](https://github.com/react-native-oh-library/react-native-apple-authentication/issues/1)


## 开源协议

本项目基于 [Apache License 2.0](https://github.com/invertase/react-native-apple-authentication/blob/main/LICENSE) ，请自由地享受和参与开源。