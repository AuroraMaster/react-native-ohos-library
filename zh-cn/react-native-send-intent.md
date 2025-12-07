> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-send-intent</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lucasferreira/react-native-send-intent">
        <img src="https://img.shields.io/badge/platforms-android%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/lucasferreira/react-native-send-intent?tab=readme-ov-file#license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-send-intent)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                  | 支持RN版本 |
|--------| ------------------------------------------------------------ | ---------- |
| <=1.3.0-0.0.5@deprecated | [@react-native-oh-tpl/react-native-send-intent Releases(deprecated)](https://github.com/react-native-oh-library/react-native-send-intent/releases) | 0.72       |
| 1.3.1             | [@react-native-ohos/react-native-send-intent Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-send-intent/releases)   | 0.72       |
| 1.4.0             | [@react-native-ohos/react-native-send-intent Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-send-intent/releases)   | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-ohos/react-native-send-intent
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-send-intent
```

<!-- tabs:end -->


下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useState, useEffect } from 'react';
import {Button, Text} from 'react-native';
import NativeSendIntent from 'react-native-send-intent'

function SendIntent() {

    return (
        <>
            <>
                <Text style={{ color: "red" }}>NativeSendIntent.sendPhoneDial</Text>
                <Button
                    onPress={() => {
                        NativeSendIntent.sendPhoneDial('10086', false);
                    }}
                    title=""
                    color="#841584"
                />
            </>
            <>
                <Text style={{ color: "red" }}>NativeSendIntent.sendSms</Text>
                <Button
                    onPress={() => {
                        NativeSendIntent.sendSms('100010', 'text SMS');
                    }}
                    title=""
                    color="#DC143C"
                />
            </>
            <>
                <Text style={{ color: "red" }}>NativeSendIntent.openCalendar</Text>
                <Button
                    onPress={() => {
                        NativeSendIntent.openCalendar();
                    }}
                    title=""
                    color="#D2691E"
                />
            </>
            <>
                <Text style={{ color: "red" }}>NativeSendIntent.sendMail</Text>
                <Button
                    onPress={() => {
                        NativeSendIntent.sendMail('mailto:someone@example.com', 'This%20is%20the%20subject', 'This%20is%20the%20body');
                    }}
                    title=""
                    color="#B8860B"
                />
            </>
            <>
                <Text style={{ color: "red" }}>NativeSendIntent.openMaps</Text>
                <Button
                    onPress={() => {
                        NativeSendIntent.openMaps('武昌火车站');
                    }}
                    title=""
                    color="#FF0000"
                />
            </>
            <>
                <Text style={{ color: "red" }}>NativeSendIntent.openCamera</Text>
                <Button
                    onPress={() => {
                        NativeSendIntent.openCamera();
                    }}
                    title=""
                    color="#FF1493"
                />
            </>
            <>
                <Text style={{ color: "red" }}>NativeSendIntent.openSettings</Text>
                <Button
                    onPress={() => {
                        NativeSendIntent.openSettings('bluetooth_entry');
                    }}
                    title=""
                    color="#8B4513"
                />
            </>
            <>
                <Text style={{ color: "red" }}>NativeSendIntent.gotoHomeScreen</Text>
                <Button
                    onPress={() => {
                        NativeSendIntent.gotoHomeScreen();
                    }}
                    title=""
                    color="#006400"
                />
            </>
        </>
    );
};
export default SendIntent;
```

## 使用 Codegen

Version >= @react-native-ohos/react-native-send-intent@1.3.1，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-send-intent@1.3.1，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入 (推荐)

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-send-intent": "file:../../node_modules/@react-native-ohos/react-native-send-intent/harmony/send_intent.har"
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

### 3.配置 CMakeLists 和引入 SendIntentPackage

> 若使用的是 <=1.3.0-0.0.5 版本，请跳过本章。

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-send-intent/src/main/cpp" ./send_intent)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_send_intent)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SendIntentPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<SendIntentPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 RNSendIntentPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {RNSendIntentPackage} from '@react-native-ohos/react-native-send-intent/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+    new RNSendIntentPackage(ctx)
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

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## API

| Name                                   | Description                                       | Type     | Required | Platform | HarmonyOS Support |
| -------------------------------------- | ------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| sendText                               | 文本分享功能（Share）                             | Function | no       | Android  | yes               |
| sendMail                               | 发送邮件功能（仅支持 text/plain 格式）            | Function | no       | Android  | yes               |
| sendSms                                | 短信发送功能                                      | Function | no       | Android  | yes               |
| sendPhoneCall                          | 电话拨号界面调用功能                              | Function | no       | Android  | yes               |
| sendPhoneDial                          | 电话拨号界面调用功能（原文拼写修正：Usage of）    | Function | no       | Android  | yes               |
| addCalendarEvent                       | 创建日历事件                                      | Function | no       | Android  | no                |
| isAppInstalled                         | 检查应用是否已安装                                | Function | no       | Android  | no                |
| installRemoteApp                       | 安装远程 APK 文件                                 | Function | no       | Android  | no                |
| openApp                                | 打开应用                                          | Function | no       | Android  | yes               |
| openAppWithData                        | 携带数据打开应用                                  | Function | no       | Android  | no                |
| openChromeIntent                       | 打开浏览器                                        | Function | no       | Android  | yes               |
| openCalendar                           | 打开日历（原文描述修正：Open Calendar Intent）    | Function | no       | Android  | yes               |
| openCamera                             | 打开相机                                          | Function | no       | Android  | yes               |
| openEmailApp                           | 打开邮件应用                                      | Function | no       | Android  | yes               |
| openAllEmailApp                        | 打开设备上所有可用的邮件应用                      | Function | no       | Android  | yes               |
| openDownloadManager                    | 打开下载管理器                                    | Function | no       | Android  | yes               |
| openChooserWithOptions                 | 打开 “分享至” 对话框                              | Function | no       | Android  | yes               |
| openChooserWithMultipleOptions         | 打开多文件 “分享至” 对话框                        | Function | no       | Android  | yes               |
| openMaps                               | 打开地图应用                                      | Function | no       | Android  | yes               |
| openMapsWithRoute                      | 打开地图并显示路线                                | Function | no       | Android  | yes               |
| shareTextToLine                        | 向 Line 应用分享文本                              | Function | no       | Android  | no                |
| shareImageToInstagram                  | 向 Instagram 应用分享图片                         | Function | no       | Android  | no                |
| openSettings                           | 打开系统设置                                      | Function | no       | Android  | yes               |
| getVoiceMailNumber                     | 获取语音信箱号码                                  | Function | no       | Android  | no                |
| openFileChooser                        | 打开文件选择器                                    | Function | no       | Android  | yes               |
| openFilePicker                         | 打开 Android 系统自带文件选择器，返回文件路径回调 | Function | no       | Android  | yes               |
| getPhoneNumber                         | 获取设备电话号码                                  | Function | no       | Android  | no                |
| requestIgnoreBatteryOptimizations      | 申请 “忽略电池优化” 权限                          | Function | no       | Android  | no                |
| showIgnoreBatteryOptimizationsSettings | 显示电池优化设置界面                              | Function | no       | Android  | no                |
| gotoHomeScreen                         | 跳转至设备主屏幕                                  | Function | no       | Android  | yes               |
| openAppWithUri                         | 打开应用（若未安装则跳转至应用商店）              | Function | no       | Android  | yes               |

## 遗留问题
 - [ ] react-native-send-intent部分方法未实现HarmonyOS化 [issue#2](https://github.com/react-native-oh-library/react-native-send-intent/issues/2) 

## 其他
- installRemoteApp(); 不支持通过一个链接下载一个包，进行安装，只能通过应用市场
- shareTextToLine(); 共享的应用android源码为海外应用,无法打开
- shareImageToInstagram(); Instagram为海外应用,无法打开
- getVoiceMailNumber(); ICCID和号码信息为敏感数据，不开放(https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-sim-V5)
- getPhoneNumber(); ICCID和号码信息为敏感数据，不开放(https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-sim-V5)

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/lucasferreira/react-native-send-intent?tab=readme-ov-file#license) ，请自由地享受和参与开源。
