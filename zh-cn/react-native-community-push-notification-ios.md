> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>@react-native-community/push-notification-ios</code> </h1>
</p>

本项目基于 [@react-native-community/push-notification-ios@1.11.0](https://github.com/react-native-push-notification/ios/tree/v1.11.0) 开发。

该第三方库的仓库已迁移至 GitCode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/push-notification-ios`，具体版本所属关系如下：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.11.0@deprecated     | [@react-native-oh-tpl/push-notification-ios Releases(deprecated)](https://github.com/react-native-oh-library/react-native-push-notification-ios/releases) | 0.72       |
| 1.11.2      | [@react-native-ohos/push-notification-ios Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-push-notification-ios/releases) | 0.72       |
| 1.12.0      | [@react-native-ohos/push-notification-ios Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-push-notification-ios/releases) | 0.77       |

## 1. 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/push-notification-ios
```

#### **yarn**

```bash
yarn add @react-native-ohos/push-notification-ios
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { View, Text, Button } from "react-native";

import PushNotification from "@react-native-community/push-notification-ios";

export const App = () => {
  const [data, setData] = useState({});

  const addNotificationRequest = () => {
    PushNotification.addNotificationRequest({
      id: "test",
      title: "title",
      subtitle: "subtitle",
      body: "body",
      fireDate: new Date(new Date().valueOf() + 1000),
      repeats: true,
    });
  };

  const addSilentNotificationRequest = () => {
    PushNotification.addNotificationRequest({
      id: "test-4",
      title: "title",
      subtitle: "subtitle",
      body: "body",
      isSilent: true,
      fireDate: new Date(new Date().valueOf() + 2000),
      repeats: true,
      userInfo: {
        data: "123456",
      },
    });
  };

  const addMultipleRequests = () => {
    PushNotification.addNotificationRequest({
      id: "test-1",
      title: "First",
      subtitle: "subtitle",
      body: "First Notification out of 3",
      fireDate: new Date(new Date().valueOf() + 10000),
      repeats: true,
    });

    PushNotification.addNotificationRequest({
      id: "test-2",
      title: "Second",
      subtitle: "subtitle",
      body: "Second Notification out of 3",
      fireDate: new Date(new Date().valueOf() + 12000),
      repeats: true,
    });

    PushNotification.addNotificationRequest({
      id: "test-3",
      title: "Third",
      subtitle: "subtitle",
      body: "Third Notification out of 3",
      fireDate: new Date(new Date().valueOf() + 14000),
      repeats: true,
    });
  };

  const removeAllDeliveredNotifications = () => {
    PushNotification.removeAllDeliveredNotifications();
  };

  const removeDeliveredNotifications = () => {
    PushNotification.removeDeliveredNotifications(["test-1", "test-2"]);
  };

  const getDeliveredNotifications = () => {
    PushNotification.getDeliveredNotifications((data) => {
      if (data) {
        setData(data);
      } else {
        console.log("failed");
      }
    });
  };

  return (
    <View style={{ flexDirection: "column", justifyContent: "space-between" }}>
      <Button
        title="Add Notification Request"
        onPress={addNotificationRequest}
      />
      <Button
        title="Add Slient Notification Request"
        onPress={addSilentNotificationRequest}
      />
      <Button
        title="Add Multiple Notification Requests"
        onPress={addMultipleRequests}
      />
      <Button
        title="Set app's icon badge to 42"
        onPress={() => PushNotification.setApplicationIconBadgeNumber(42)}
      />
      <Button
        title="Clear app's icon badge"
        onPress={() => PushNotification.setApplicationIconBadgeNumber(0)}
      />
      <Button
        title="Remove All Delivered Notification Requests"
        onPress={removeAllDeliveredNotifications}
      />
      <Button
        title="Remove Delivered Notification Requests"
        onPress={removeDeliveredNotifications}
      />
      <View>
        <Button
          title="Get Delivered Notification"
          onPress={getDeliveredNotifications}
        />
        <Text>{JSON.stringify(data)}</Text>
      </View>
    </View>
  );
};
```

## 2. Manual Link

Version >= @react-native-ohos/push-notification-ios@1.11.2，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1. Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
  }
}
```

### 2.2. 引入原生端代码

目前有两种方法：

- 通过 har 包引入；
- 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@react-native-ohos/push-notification-ios": "file:../../node_modules/@react-native-ohos/push-notification-ios/harmony/push_notification.har"
  }
```

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 2.3. 配置 CMakeLists 和引入 PushNotificationPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/push-notification-ios/src/main/cpp" ./push_notification)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_push_notification)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "PushNotificationPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<PushNotificationPackage>(ctx)
    };
}
```

### 2.4. 在 ArkTs 侧引入 PushNotificationPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { PushNotificationPackage } from '@react-native-ohos/push-notification-ios/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new PushNotificationPackage(ctx)
  ];
}
```

### 2.5. 在 ArkTs 侧Ability中添加

打开 `entry/src/main/ets/entryability/EntryAbility.ets`，在onNewWant回调中添加：

```diff
  ...
+ import { PushNotificationModule } from '@react-native-ohos/push-notification-ios/ts';
  ...
onNewWant(want: Want, _launchParam: AbilityConstant.LaunchParam): void {
+ PushNotificationModule.getInstance().didReceiveRemoteNotification(want);
}
```

### 2.6. 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1. 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

## 4. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                            | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ------------------------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| addNotificationRequest          | 按指定的触发时间（firedate）向通知中心发送通知请求（notificationRequest）。若未设置触发时间，则立即发送。 | function | no       | iOS      | yes               |
| getDeliveredNotifications       | 返回仍显示在通知中心的应用通知列表                           | function | no       | iOS      | yes               |
| removeAllDeliveredNotifications | 从通知中心移除所有已送达的通知                               | function | no       | iOS      | yes               |
| removeDeliveredNotifications    | 从通知中心移除指定的已送达通知                               | function | no       | iOS      | yes               |
| setApplicationIconBadgeNumber   | 设置主屏幕上应用图标的角标数字                               | function | no       | iOS      | yes               |
| getApplicationIconBadgeNumber   | 获取主屏幕上应用图标的当前角标数字                           | function | no       | iOS      | no                |
| cancelLocalNotifications        | 取消本地通知                                                 | function | no       | iOS      | no                |
| requestPermissions              | 向 iOS 申请通知权限，触发用户授权弹窗。默认情况下会申请所有通知权限，也可通过传入权限映射对象申请部分权限。 支持的权限如下 | function | no       | iOS      | no                |
| abandonPermissions              | 取消注册通过 Apple 推送通知服务（Apple Push Notification service）接收的所有远程通知 | function | no       | iOS      | no                |
| checkPermissions                | 查看当前已启用的推送权限                                     | function | no       | iOS      | no                |
| getInitialNotification          | 若应用是通过推送通知启动的，该 Promise 会解析为 PushNotificationIOS 类型的对象；否则解析为 null。 | function | no       | iOS      | no                |
| getScheduledLocalNotifications  | 获取当前已调度（待发送）的本地通知                           | function | no       | iOS      | no                |

## 5. 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


**Parameters:**

_NotificationRequest:_

| Name                  | Description                                                  | Type    | Required | Platform | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| `id`                  | 通知的唯一标识                                               | string  | yes      | All      | yes               |
| `title`               | 通知事由的简要描述                                           | string  | yes      | All      | yes               |
| `subtitle`            | 通知事由的次要描述                                           | string  | no       | All      | no                |
| `body`                | 通知中显示的消息内容                                         | string  | yes      | All      | yes               |
| `badge`               | 应用图标上显示的角标数字                                     | number  | no       | All      | yes               |
| `fireDate`            | 系统应送达通知的日期和时间                                   | object  | no       | All      | no                |
| `repeats`             | 设置通知是否重复发送                                         | boolean | no       | All      | no                |
| `repeatsComponent`    | 定义 fireDate 中需重复的时间部分的对象                       | object  | no       | All      | no                |
| `sound`               | 通知触发时播放的音效                                         | string  | no       | All      | no                |
| `category`            | 通知的分类，可交互通知（actionable notifications）必需配置此参数 | string  | no       | All      | no                |
| `isSilent`            | 若为 true，通知将无音效显示                                  | boolean | no       | All      | yes               |
| `isCritical`          | 若为 true，即使设备处于锁定、静音或勿扰模式，通知音效仍会播放 | boolean | no       | All      | no                |
| `criticalSoundVolume` | 重要通知（critical notification）的音量值（取值范围 0-1）。未指定时使用默认音量 | number  | no       | All      | no                |
| `userInfo`            | 包含额外通知数据的对象                                       | object  | no       | All      | yes               |
| `isTimeZoneAgnostic`  | 若为 true，时区变更时 fireDate 会自动调整（例如闹钟场景）    | boolean | no       | All      | no                |
| `interruptionLevel`   | 指定通知干扰级别（interruption level）的字符串。有效值为 `'active'`（主动）、`'passive'`（被动）、`'timeSensitive'`（时间敏感）或 `'critical'`（重要） | string  | no       | All      | no                |

## 6. 遗留问题

- [ ] HarmonyOS 的 NotificationManager 的规格和 IOS 不一致，其 NotificationRequest 所含参数，在 HarmonyOS 上部分没有适配对应参数，问题: [issue#1](https://github.com/react-native-oh-library/react-native-push-notification-ios/issues/4)
- [ ] 原库部分接口在 HarmonyOS 中没有对应接口处理相关逻辑，问题: [issue#2](https://github.com/react-native-oh-library/react-native-push-notification-ios/issues/3)

## 7. 其他

## 8. 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-push-notification/ios/blob/master/LICENSE) ，请自由地享受和参与开源。