> Template version: v0.4.0

<p align="center">
  <h1 align="center"> <code>react-native-orientation-locker</code> </h1>
</p>

This project is based on [react-native-orientation-locker](https://github.com/wonday/react-native-orientation-locker) 。

This third-party library has been migrated to Gitcode and is now available for direct download from npm, the new package name is：`@react-native-ohos/react-native-orientation-locker` The version correspondence details are as follows：
| Name | Version | Release Information | Supported RN Version | Supported Autolink | Compile API Version | Community Baseline Version | npm Address     |
| ------------ | ------------ | ------------------------------ | ------------- | ------------- |------------------------ | ------------- | ------------- |
| @react-native-ohos/react-native-orientation-locker |  1.8.0   | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-orientation-locker/releases) | 0.77 | 否 | API12+ | 1.7.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-orientation-locker) |
| @react-native-ohos/react-native-orientation-locker | 1.7.1   | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-orientation-locker/releases) | 0.72 | 否 | API12+ | 1.7.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-orientation-locker) |
| @react-native-oh-tpl/react-native-orientation-locker | <= 1.7.0-0.0.7@deprecated    | [Gitcode Releases](https://github.com/react-native-oh-library/react-native-orientation-locker/releases) | 0.72 | 否 | API12+ | 1.7.0 | [Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/react-native-orientation-locker) |


## 1. Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/react-native-orientation-locker
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-orientation-locker
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx

import {
  Alert,
  Button,
  StyleSheet,
  Text,
  TouchableOpacity,
  View,
} from "react-native";
import { useCallback, useEffect, useState } from "react";
import Orientation, {
  OrientationLocker,
  PORTRAIT,
  LANDSCAPE,
  useOrientationChange,
  useDeviceOrientationChange,
  useLockListener,
} from "react-native-orientation-locker";
import React from 'react';

export function OrientationLockerExample() {
  const [showVideo, setShowVideo] = useState(true);
  const [orientation, setOrientation] = useState<string>();
  const [isLock, setIsLock] = useState<boolean>(false);
  const updateOrientation = (orientation: string) => {
    console.info("---orientation-----22222", orientation);
    setOrientation(orientation);
  };

  const updateDeviceOrientation = (orientation: string) => {
    console.info("---updateDeviceOrientation-----1111111", orientation);
    setOrientation(orientation);
  };

  const updateLock = (orientation: string) => {
    console.info("---updateLock-----", orientation);
  };

  useEffect(() => {
    getOrientationInt();
  }, []);

  const getOrientationInt = () => {
    Orientation.getOrientation((orientation: string) => {
      updateOrientation(orientation);
      if (orientation) {
        Alert.alert(`The current screen orientation is${orientation}`);
      } else {
        Alert.alert("Failed to obtain the current screen orientation");
      }
    });
  };

  const setLockToPortrait = () => {
    Orientation.lockToPortrait();
  };
  const setLockToLandscape = () => {
    Orientation.lockToLandscape();
  };
  const setLockToLandscapeLeft = () => {
    Orientation.lockToLandscapeLeft();
  };
  const setLockToLandscapeRight = () => {
    Orientation.lockToLandscapeRight();
  };
  const unlockAllOrientations = () => {
    Orientation.unlockAllOrientations();
  };
  const lockToPortraitUpsideDown = () => {
    Orientation.lockToPortraitUpsideDown();
  };
  const lockToAllOrientationsButUpsideDown = () => {
    Orientation.lockToAllOrientationsButUpsideDown();
  };
  const addTisten = () => {
    Orientation.addDeviceOrientationListener(updateDeviceOrientation);
  };
  const cancelAddTisten = () => {
    Orientation.removeDeviceOrientationListener(updateDeviceOrientation);
  };

  return (
    <View style={styles.container}>
      <Text>{`Current Orientation----: ${orientation}`}</Text>
      <TouchableOpacity
        onPress={lockToPortraitUpsideDown}
        style={styles.button}
      >
        <Text style={styles.instructions}>Lock the up and down direction</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={lockToAllOrientationsButUpsideDown}
        style={styles.button}
      >
        <Text style={styles.instructions}>
          Lock all directions except for up and down
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToPortrait} style={styles.button}>
        <Text style={styles.instructions}>
          Lock the current screen to portrait mode
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToLandscape} style={styles.button}>
        <Text style={styles.instructions}>
          Lock the current screen to landscape mode
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToLandscapeLeft} style={styles.button}>
        <Text style={styles.instructions}>
          Lock the current screen to landscape and rotate it to the left
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToLandscapeRight} style={styles.button}>
        <Text style={styles.instructions}>
          Lock the current screen to landscape and rotate it to the right
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={unlockAllOrientations} style={styles.button}>
        <Text style={styles.instructions}>
          Unlock the current screen rotation lock
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={addTisten} style={styles.button}>
        <Text style={styles.instructions}>Add monitoring</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={cancelAddTisten} style={styles.button}>
        <Text style={styles.instructions}>Cancel monitoring</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "flex-start",
    alignItems: "center",
    backgroundColor: "#F5FCFF",
    marginTop: 20,
  },
  welcome: {
    fontSize: 20,
    textAlign: "center",
    margin: 10,
  },
  instructions: {
    textAlign: "center",
    color: "#eeeeee",
    marginBottom: 0,
  },
  buttonContainer: {
    flex: 0,
    flexDirection: "row",
    justifyContent: "space-around",
  },
  button: {
    padding: 5,
    margin: 5,
    borderWidth: 1,
    borderColor: "white",
    borderRadius: 3,
    backgroundColor: "grey",
  },
});
```

## 2. Manual Link

|                                      | Supported Autolink | Supported RN Version |
|--------------------------------------|--------------|--------|
| ~1.8.0                     | No           | 0.77   |
| ~1.7.1                     | Yes          | 0.72   |
| <= 1.7.0-0.0.7@deprecated | No           | 0.72   |

Projects using AutoLink need to be configured according to this document, AutoLink framework guide.：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you are using supports Autolink and the project has integrated Autolink, you can skip the ManualLink configuration.

<details>
  <summary>ManualLink: This step provides guidance for manually configuring native dependencies.</summary>

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1. Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).
```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony"
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
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-orientation-locker":"file:../../node_modules/@react-native-ohos/react-native-orientation-locker/harmony/orientation_locker.har"
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

### 2.3. Configuring CMakeLists and Introducing OrientationLockerPackage

> If you are using version <= 1.7.0-0.0.7, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-orientation-locker/src/main/cpp" ./orientation_locker)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_orientation_locker)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "OrientationLockerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<OrientationLockerPackage>(ctx),
    };
}
```

### 2.4. Introducing RNOrientationLockerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+  import { RNOrientationLockerPackage } from '@react-native-ohos/react-native-orientation-locker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new RNOrientationLockerPackage(ctx)
  ];
}
```
</details>

### 2.5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1. Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### 3.2. Permission Requirements

Due to the fact that this library obtains data from acceleration sensors, corresponding permissions need to be configured when using it.
The permissions need to be configured in the entry/src/main directory and added to module.json5 as follows::

```diff
...
"requestPermissions": [
...
+      {
+        "name": "ohos.permission.ACCELEROMETER"
+       }
    ]
```

## 4. API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| -------------- | ---------------------------------------- | ------ | ------------------------  | ---------------- | ----------------- |
| lockToPortrait   |   Lock the orientation of the application to portrait (portrait)         |  function  | No       | IOS/Android | yes               |
| lockToLandscape  |    Lock the orientation of the application to landscape (landscape)         | function | No       | IOS/Android | yes               |
| lockToLandscapeLeft  | Lock the orientation of the app to landscape and rotated to the left         | function | No       | IOS/Android | yes               |
| lockToLandscapeRight  | Lock the orientation of the app to landscape and rotated to the right         | function | No       | IOS/Android | yes               |
| unlockAllOrientations  | Unlocks the orientation of the app, allowing the device to rotate freely          | function | No       | IOS/Android | yes               |
| getOrientation  | Get the direction of the current device        | callback | No       | IOS/Android | yes               |
| getDeviceOrientation  | Obtains the direction of the current device        | callback | No       | IOS/Android | yes               |

## 5. Events

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name   | Description                              | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | ---------------------------------------- | ------ | -------- | ----------- | ----------------- |
| addOrientationListener  | When UI orientation changed, callback function will be called. But if lockToXXX is called , callback function will be not called untill unlockAllOrientations. It can return either PORTRAIT LANDSCAPE-LEFT LANDSCAPE-RIGHT PORTRAIT-UPSIDEDOWN UNKNOWN When lockToXXX/unlockAllOrientations, it will force resend UI orientation changed event.| callback | No       | IOS/Android | yes               |
| addDeviceOrientationListener  | When device orientation changed, callback function will be called. When lockToXXX is called, callback function also can be called. It can return either PORTRAIT LANDSCAPE-LEFT LANDSCAPE-RIGHT PORTRAIT-UPSIDEDOWN UNKNOWN | callback | No       | IOS/Android | yes               |
| removeOrientationListener  | Remove a previously added screen orientation change listener   | callback | No       | IOS/Android | yes               |
| removeDeviceOrientationListener  |   Remove the event that monitors physical directional changes of the device      | callback | No       | IOS/Android | yes               |
| addLockListener  | When call lockToXXX/unlockAllOrientations, callback function will be called. It can return either PORTRAIT LANDSCAPE-LEFT LANDSCAPE-RIGHT UNKNOWN UNKNOWN means not be locked. | callback | No       | IOS/Android | yes               |
| removeLockListener  |  Remove the event that monitors changes in screen orientation lock status   | callback | No       | IOS/Android | yes              |
| removeAllListeners  |  Remove all listening events     | callback | No       | IOS/Android | yes              |


## 6. Known Issues

## 7. Others

## 8. License

This project is licensed under [The MIT License (MIT)](https://github.com/wonday/react-native-orientation-locker/blob/master/LICENSE).
