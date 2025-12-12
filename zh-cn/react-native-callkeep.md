模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-callkeep</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/react-native-webrtc/react-native-callkeep">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-webrtc/react-native-callkeep/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-callkeep)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本            | 发布信息                                                     | 支持RN版本 |
|------------------| ------------------------------------------------------------ | ---------- |
| <= 4.3.14-0.0.1  | [@react-native-oh-tpl/react-native-callkeep Releases(deprecated)](https://github.com/react-native-oh-library/react-native-callkeep/releases) | 0.72       |
| 4.3.15           | [@react-native-ohos/react-native-callkeep Releases](https://github.com/react-native-oh-library/react-native-callkeep/releases)               | 0.72       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-callkeep
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-callkeep
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState, useEffect } from 'react';
import {
    Button,
    View,
    Alert,
    Text,
} from 'react-native';

import RNCallKeep from 'react-native-callkeep';

export function CallKeepExample() {
    const handleClick = (buttonId: number) => {
        switch (buttonId) {
            case 1:
                RNCallKeep.startCall("0x123456", "10086");
                break;
            case 2:
                RNCallKeep.isCallActive("0x123456").then(res => {
                    Alert.alert('isCallActive value:' + res);
                });
                break;
            case 3:
                RNCallKeep.checkIfBusy().then(res => {
                    Alert.alert('checkIfBusy value:' + res);
                });
                break;

            default:
                break;
        }
    };
    return (
        <>
            <Text style={{ color: "red" }}>RNCallKeep.startCall</Text>
            <Button title='startCall' onPress={() => handleClick(1)} ></Button>

            <Text style={{ color: "red" }}>RNCallKeep.isCallActive</Text>
            <Button title='isCallActive' onPress={() => handleClick(2)} ></Button>

            <Text style={{ color: "red" }}>RNCallKeep.checkIfBusy</Text>
            <Button title='checkIfBusy' onPress={() => handleClick(3)} ></Button>
        </>
    );
}

```
## 使用 Codegen

Version >= @react-native-ohos/react-native-callkeep@4.3.15，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-callkeep@4.3.15，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
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
    "@react-native-ohos/react-native-callkeep": "file:../../node_modules/@react-native-ohos/react-native-callkeep/harmony/call_keep.har"
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

### 3.配置 CMakeLists 和引入 RNCallKeepPackage

> 若使用的是 <= 4.3.14-0.0.1 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
...

project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-callkeep/src/main/cpp" ./callkeep)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_callkeep)
# RNOH_BEGIN: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
+ #include "RNCallKeepPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<RNCallKeepPackage>(ctx)
}
```


### 4.在 ArkTs 侧引入 RNCallKeepPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNCallKeepPackage } from '@react-native-ohos/react-native-callkeep';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNCallKeepPackage(ctx),
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

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 YES 表示 HarmonyOS 平台支持该属性；NO 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | :------: | :------: | :----------------: |
| isCallActive() | The call exists  user has already answered the call | RNCallKeep.isCallActive(uuid) |    NO    |   iOS    |        YES        |
| checkIfBusy() | Checks if there are any active calls on the device | RNCallKeep.checkIfBusy() | NO | iOS | YES |
| getCalls() | Returns a Promise. The result will be an array with all current calls and their states | RNCallKeep.getCalls() | NO | iOS | NO |
| checkSpeaker() | Checks if the device speaker is on and returns a promise with a boolean value | RNCallKeep.checkSpeaker() | NO | iOS | NO |
| startCall() | Make an outgoing call | RNCallKeep.startCall(uuid, handle, contactIdentifier, handleType, hasVideo) | NO | ALL | YES |
| displayIncomingCall() | Display system UI for incoming calls | RNCallKeep.displayIncomingCall() | NO | ALL | NO |
| answerIncomingCall() | Use this to tell the sdk a user answered a call from the app UI | RNCallKeep.answerIncomingCall(uuid) | NO | ALL | NO |
| updateDisplay() | Use this to update the display after an outgoing call has started | RNCallKeep.updateDisplay(uuid, displayName, handle) | NO | ALL | NO |
| endCall() | When finish an incoming/outgoing call | RNCallKeep.endCall(uuid) | NO | ALL | NO |
| endAllCalls() | End all ongoing calls | RNCallKeep.endAllCalls() | NO | ALL | NO |
| rejectCall() | When you reject an incoming call | RNCallKeep.rejectCall(uuid) | NO | ALL | NO |
| reportEndCallWithUUID() | Report that the call ended without the user initiating | RNCallKeep.reportEndCallWithUUID(uuid, reason) | NO | ALL | NO |
| setMutedCall() | Switch the mic on/off | RNCallKeep.setMutedCall(uuid, true) | NO | ALL | NO |
| setOnHold() | Set a call on/off hold | RNCallKeep.setOnHold(uuid, true) | NO |   ALL    | NO |
| removeEventListener() | Allows to remove the listener on an event | RNCallKeep.removeEventListener() | NO |   ALL    |        NO         |
| setup()                        | Doing this allows capturing events prior to the react native event bridge being up | RNCallKeep.setup()                                           |    NO    |   ALL    |        NO         |
| setSettings()                  | Initialize Operation Settings                                | RNCallKeep.setSettings()                                     |    NO    |   ALL    |        NO         |
| getAudioRoutes()               | Get the list of available audio routes. i.e. bluetooth, wired/ear-piece, speaker and phone | RNCallKeep.getAudioRoutes()                                  |    NO    |   ALL    |        NO         |
| setAudioRoute()                | Set audio route using a route                                | RNCallKeep.setAudioRoute(uuid, routeName)                    |    NO    |   ALL    |        NO         |
| getInitialEvents()             | This is alternative to     event                             | RNCallKeep.getInitialEvents()                                |    NO    |   ALL    |        NO         |
| clearInitialEvents()           | Clear all pending actions returned                           | RNCallKeep.clearInitialEvents()                              |    NO    |   ALL    |        NO         |
| setAvailable()                 | Tell *ConnectionService* that the device is ready to make outgoing calls via the native Phone app | RNCallKeep.setAvailable(true)                                |    NO    | Android  |        NO         |
| setForegroundServiceSettings() | Configures the Foreground Service                            | RNCallKeep.setForegroundServiceSettings()                    |    NO    | Android  |        NO         |
| canMakeMultipleCalls()         | Disable the "Add call" button in ConnectionService UI        | RNCallKeep.canMakeMultipleCalls(false)                       |    NO    | Android  |        NO         |
| setCurrentCallActive()         | Mark the current call as active                              | RNCallKeep.setCurrentCallActive(uuid)                        |    NO    | Android  |        NO         |
| checkIsInManagedCall()         | Returns true if there is an active native call               | RNCallKeep.checkIsInManagedCall()                            |    NO    | Android  |        NO         |
| setConnectionState()           | Change the state of the call                                 | RNCallKeep.setConnectionState(uuid, state)                   |    NO    | Android  |        NO         |
| toggleAudioRouteSpeaker()      | Update the audio route of Audio Service                      | RNCallKeep.toggleAudioRouteSpeaker(uuid, true)               |    NO    | Android  |        NO         |
| backToForeground()             | Use this to display the application in foreground if the application was in background state | RNCallKeep.backToForeground()                                |    NO    | Android  |        NO         |
| registerPhoneAccount()         | Registers Android phone account manually                     | RNCallKeep.registerPhoneAccount(options)                     |    NO    | Android  |        NO         |
| registerEvents()               | Registering Initialization Events | RNCallKeep.registerAndroidEvents() | NO | Android | NO |
| sendDTMF()                     | On Play Dtmf Tone | RNCallKeepModule.sendDTMF(uuid, key) | NO | Android | NO |
| unregisterEvents()             | Unregistering Initialization Events | RNCallKeep.unregisterAndroidEvents() | NO | Android | NO |
| setReachable()                 | Check if the application is reachable before making a call from the native phone application. | RNCallKeep.setReachable() | NO | Android | NO |
| supportConnectionService()     | Tells if `ConnectionService` is available on the device      | RNCallKeep.supportConnectionService()                        |    NO    | Android  |        NO         |
| hasPhoneAccount()              | Checks if the user has enabled the phone account for your application | RNCallKeep.hasPhoneAccount()                                 |    NO    | Android  |        NO         |
| hasOutgoingCall()              | When waking up the Android application in background mode    | RNCallKeep.hasOutgoingCall()                                 |    NO    | Android  |        NO         |
| hasDefaultPhoneAccount()       | Checks if the user has set a default phone account           | RNCallKeep.hasDefaultPhoneAccount(options)                   |    NO    | Android  |        NO         |
| checkPhoneAccountEnabled()     | Checks if the user has set a default phone account and it's enabled | RNCallKeep.checkPhoneAccountEnabled()                        |    NO    | Android  |        NO         |
| isConnectionServiceAvailable() | Check if the device support ConnectionService                | RNCallKeep.isConnectionServiceAvailable() |    NO    | Android  |        NO         |

## 遗留问题

- [ ]   react-native-callkeep 部分方法未实现 HarmonyOS 化： [issue#2](https://github.com/react-native-oh-library/react-native-callkeep/issues/2)。



## 其他

## 开源协议

本项目基于 [The ISC License (ISC)](https://github.com/react-native-webrtc/react-native-callkeep/blob/master/LICENSE) ，请自由地享受和参与开源。