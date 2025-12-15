> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-touch-id</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/naoufal/react-native-touch-id">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/naoufal/react-native-touch-id?tab=readme-ov-file#license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-touch-id)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本                     | 发布信息                                     |Supported RN Version  |
|---------------------------|--------------------------------------------| -------------------- |
| <= 4.4.1-0.0.3@deprecated | [@react-native-oh-tpl/react-native-touch-id Releases(deprecated)](https://github.com/react-native-oh-library/react-native-touch-id/releases) | 0.72                 |
| 4.4.2                     | [@react-native-ohos/react-native-touch-id Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-touch-id/releases)               | 0.72       |
| 4.5.0                     | [@react-native-ohos/react-native-touch-id Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-touch-id/releases)               | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-touch-id
```

如果在编译时报错为需引入源库，可以运行如下指令

```bash
npm install --force
```
#### **yarn**

```bash
yarn add @react-native-ohos/react-native-touch-id
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component, useState } from 'react';
import { Alert, View, Button, Text } from 'react-native';
import TouchID from 'react-native-touch-id';

const App = () => {
  const [result, setResult] = useState<string>('')
  return (
     <View>
      <Text style={{ height: 40, backgroundColor: 'white', textAlign: 'center' }}>{result}</Text>
      <Button title='验证是否有指纹权限'
        onPress={() => {
          TouchID.isSupported({ unifiedErrors: false }).then((res: any) => {
            setResult(res)
          }).catch((err: any) => {
            setResult(err.message)
          })
        }}
      ></Button>
      <Button title='校验指纹'
        onPress={() => {
          TouchID.authenticate().then((res: boolean) => {
            setResult('认证成功')
          }).catch((err: any) => {
            setResult(err.message)
          })
        }}
      ></Button>
    </View>
  )
};

export default App;

```
## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

|                                       | 是否支持autolink | RN框架版本 |
|---------------------------------------|-----------------|------------|
| ~4.5.0                                |  No              |  0.77     |
| ~4.4.2                                |  Yes             |  0.72     |
| <= 4.4.1-0.0.3@deprecated             |  No              |  0.72     |

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
    "@react-native-ohos/react-native-touch-id": "file:../../node_modules/@react-native-ohos/react-native-touch-id/harmony/touch_id.har"
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


### 3.配置 CMakeLists 和引入 TouchIdPackage

> 若使用的是 <= 4.4.1-0.0.3 版本，请跳过本章。

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-touch-id/src/main/cpp" ./touch_id)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_touch_id)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "TouchIdPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<TouchIdPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 TouchIdPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { TouchIdPackage } from "@react-native-ohos/react-native-touch-id/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new TouchIdPackage(ctx)
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

### 权限要求

（填入相关权限配置）

Add the following permissions to their respective files:

In your `module.json5`

```
 "requestPermissions": [
      {
        "name": "ohos.permission.ACCESS_BIOMETRIC"
      }
    ]
```

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| isSupported  | 是否支持 Touch ID | function  | yes | ios/andriod      | yes |
| authenticate  | 验证 Touch ID | function  | yes | ios/andriod      | yes |

## API 参数介绍
### authenticate(reason?: string, config?: AuthenticateConfig);
* **reason**: 提供请求身份验证的明确原因的字符串
* **config**: 用于更详细对话框设置的配置对象
  * **AuthenticateConfig**:
	| Name | Description | Type | Required | Platform | HarmonyOS Support  |
	| ---- | ----------- | ---- | -------- | -------- | ------------------ |
	| title  | **仅Android** - 确认对话框的标题 | string  | no | ios/andriod      | yes |
	| imageColor  | **仅Android** - 指纹图像的颜色 | string  | no | ios/andriod      | no |
	| imageErrorColor  | **仅Android** - 尝试失败后指纹图像的颜色 | string  | no | ios/andriod      | no |
	| sensorDescription  | **仅Android** - 指纹图像旁边显示的文字 | string  | no | ios/andriod      | no |
	| sensorErrorDescription  | **仅Android** - 尝试失败后指纹图像旁边显示的文字 | string  | no | ios/andriod      | no |
	| cancelText  | **仅Android** - 取消按钮文字 | string  | no | ios/andriod      | yes |
	| fallbackLabel  | **仅iOS** - 默认显示"显示密码"标签。如果设置为空字符串，标签将不可见 | string  | no | ios/andriod      | no |
	| passcodeFallback  | **仅iOS** - 默认设置为false。如果设置为true，将允许使用键盘密码 | boolean  | no | ios/andriod      | no |
### isSupported(config?: IsSupportedConfig): `Promise<BiometryType>`;
* **config** - 返回一个`Promise`，如果TouchID不支持则会拒绝。在iOS上会解析为一个`biometryType`字符串，值为`FaceID`或`TouchID`
 * **IsSupportedConfig**:
 	| Name | Description | Type | Required | Platform | HarmonyOS Support  |
	| ---- | ----------- | ---- | -------- | -------- | ------------------ |
    | unifiedErrors| 返回统一的错误信息 |boolean| no | ios/andriod      | yes |
## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Errors

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| 201  | Permission verification failed | string  | no | harmonry      | yes |
| 401  | Incorrect parameters | string  | no | harmonry      | no |
| 12500001  | Authentication failed  | string  | no | harmonry  | yes |
| 12500002  | General operation error   | string  | no | harmonry  | no |
| 12500003  | The operation is canceled   | string  | no | harmonry  | yes |
| 12500004  | The operation is time-out | string  | no | harmonry  | no |
| 12500005  | The authentication type is not supported   | string | no | harmonry  | no |
| 12500006  | The authentication trust level is not supported | string  | no | harmonry      | no |
| 12500007  | The authentication task is busy | string  | no | harmonry      | no |
| 12500009  | The authenticator is locked  | string  | no | harmonry  | yes |
| 12500010  | The type of credential has not been enrolled   | string | no | harmonry  | yes |
| 12500011  | The authentication is canceled from widget's navigation button   | string | no | harmonry  | yes |
| 12500013  | Indicates that current authentication failed because of PIN expired   | string | no | harmonry  | no |

## 遗留问题

- [ ] config参数部分支持.[issue#13](https://github.com/react-native-oh-library/react-native-touch-id/issues/13)
- [ ] error部分触发。[issue#12](https://gitcode.com/openharmony-sig/rntpc_react-native-touch-id/issues/12)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/naoufal/react-native-touch-id?tab=readme-ov-file#license) ，请自由地享受和参与开源。
