> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>@react-native-community/push-notification-ios</code> </h1>
</p>


This project is based on [@react-native-community/push-notification-ios@1.11.0](https://github.com/react-native-push-notification/ios/tree/v1.11.0)。

This third-party library has been migrated to GitCode and is now available for direct download from npm, the new package name is: `@react-native-ohos/push-notification-ios`, The version correspondence details are as follows:

| Third-party Library Version | Release Information    | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.11.0@deprecated     | [@react-native-oh-tpl/push-notification-ios Releases(deprecated)](https://github.com/react-native-oh-library/react-native-push-notification-ios/releases) | 0.72       |
| 1.11.2      | [@react-native-ohos/push-notification-ios Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-push-notification-ios/releases) | 0.72       |
| 1.12.0      | [@react-native-ohos/push-notification-ios Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-push-notification-ios/releases) | 0.77       |

## 1. Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

Version >= @react-native-ohos/push-notification-ios@1.11.2，now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1. Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2. Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@react-native-ohos/push-notification-ios": "file:../../node_modules/@react-native-ohos/push-notification-ios/harmony/push_notification.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 2.3. Configuring CMakeLists and Introducing PushNotificationPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/push-notification-ios/src/main/cpp" ./push_notification)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_push_notification)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 2.4. Introducing PushNotificationPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 2.5. Introducing PushNotificationModule to ArkTS

Open the `entry/src/main/ets/entryability/EntryAbility.ets`，file and add the following code：

```diff
  ...
+ import { PushNotificationModule } from '@react-native-ohos/push-notification-ios/ts';
  ...
onNewWant(want: Want, _launchParam: AbilityConstant.LaunchParam): void {
+ PushNotificationModule.getInstance().didReceiveRemoteNotification(want);
}
```

### 2.6. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1. Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

The following combinations have been verified:

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

## 4. API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                            | Description                                                                                                       | Type     | Required | Platform      | HarmonyOS Support |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------- | -------- | -------- | ------------- | ----------------- |
| addNotificationRequest          | Sends notificationRequest to notification center at specified firedate. Fires immediately if firedate is not set. | function | no       | iOS | yes               |
| getDeliveredNotifications       | Provides you with a list of the app’s notifications that are still displayed in Notification Center               | function | no       | iOS           | yes               |
| removeAllDeliveredNotifications | Remove all delivered notifications from Notification Center                                                       | function | no       | iOS           | yes               |
| removeDeliveredNotifications    | Removes the specified delivered notifications from Notification Center                                            | function | no       | iOS           | yes               |
| setApplicationIconBadgeNumber   | Sets the badge number for the app icon on the home screen                                                         | function | no       | iOS           | yes               |
| getApplicationIconBadgeNumber   | Gets the current badge number for the app icon on the home screen                                                         | function | no       | iOS           | no               |
| cancelLocalNotifications   | Cancel local notifications                                                         | function | no       | iOS           | no               |
| requestPermissions   | Requests notification permissions from iOS, prompting the user's dialog box. By default, it will request all notification permissions, but a subset of these can be requested by passing a map of requested permissions. The following permissions are supported                                                         | function | no       | iOS           | no               |
| abandonPermissions   | Unregister for all remote notifications received via Apple Push Notification service                                                         | function | no       | iOS           | no               |
| checkPermissions   | See what push permissions are currently enabled                                                         | function | no       | iOS           | no               |
| getInitialNotification   | This method returns a promise. If the app was launched by a push notification, this promise resolves to an object of type PushNotificationIOS. Otherwise, it resolves to null.                                                         | function | no       | iOS           | no               |
| getScheduledLocalNotifications   | Gets the local notifications that are currently scheduled                                                         | function | no       | iOS           | no               |

## 5. Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**Parameters:**

_NotificationRequest:_

| Name       | Description                                                       | Type    | Required | Platform | HarmonyOS Support |
| ---------- | ----------------------------------------------------------------- | ------- | -------- | -------- | ----------------- |
| `id`       | Identifier of the notification                                    | string  | yes      | All      | yes               |
| `title`    | A short description of the reason for the notification            | string  | yes      | All      | yes               |
| `subtitle` | A secondary description of the reason for the notification        | string  | no       | All      | no               |
| `body`     | The message displayed in the notificatio                          | string  | yes      | All      | yes               |
| `badge`    | The number to display as the app's icon badge                     | number  | no       | All      | yes               |
| `fireDate` | The date and time when the system should deliver the notification | object  | no       | All      | no               |
| `repeats`  | Sets notification to repeat                                       | boolean | no       | All      | no               |
| `repeatsComponent`  | An object indicating which parts of fireDate should be repeated                                       | object | no       | All      | no               |
| `sound`  | The sound played when the notification is fired                                       | string | no       | All      | no               |
| `category`  | The category of this notification, required for actionable notifications                                       | string | no       | All      | no               |
| `isSilent` | If true, the notification will appear without sound               | boolean | no       | All      | yes               |
| `isCritical` |  If true, the notification sound be played even when the device is locked, muted, or has Do Not Disturb enabled               | boolean | no       | All      | no               |
| `criticalSoundVolume` | A number between 0 and 1 for volume of critical notification. Default volume will be used if not specified               | number | no       | All      | no               |
| `userInfo` | An object containing additional notification data                 | object  | no       | All      | yes               |
| `isTimeZoneAgnostic` | If true, fireDate adjusted automatically upon time zone changes (e.g. for an alarm clock)                 | boolean  | no       | All      | no               |
| `interruptionLevel` | A string specifying the interruption level. Valid values are `'active'`, `'passive'`, `'timeSensitive'`, or `'critical'`                 | string  | no       | All      | no               |

## 6. Known Issues

- [ ] The **NotificationManager** specifications of HarmonyOS are different from those of iOS. Some parameters contained in **NotificationRequest** are not adapted to HarmonyOS: [issue#1](https://github.com/react-native-oh-library/react-native-push-notification-ios/issues/4).
- [ ] Some APIs in the source library do not have the corresponding API processing logic on HarmonyOS: [issue#2](https://github.com/react-native-oh-library/react-native-push-notification-ios/issues/3).

## 7. Others

## 8. License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-push-notification/ios/blob/master/LICENSE).
