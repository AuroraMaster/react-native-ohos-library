> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-screen-capture</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/recepkocur/react-native-screen-capture">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/recepkocur/react-native-screen-capture?tab=readme-ov-file#license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/recepkocur/react-native-screen-capture)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Version                           | Release Information                        |Supported RN Version  |
|-----------------------------------|--------------------------------------------| -------------------- |
| 0.2.4 | [@react-native-ohos/react-native-screen-capture](https://gitcode.com/OpenHarmony-RN/rntpc_react-native-screen-capture/releases) | 0.72/0.77  

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-screen-capture
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-screen-capture
```


<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import { View, Button, Text, StyleSheet } from 'react-native';
import { disallowScreenshot, keepAwake } from 'react-native-screen-capture';

class AppDemo extends React.Component {
  state = {
    isVisible: false,
    screenOn: false, // False denote allow screenshots, true denote disallow screenshots.
  };

  handleDisallowScreenshot = () => {
    // Switch state: If the current status is false (screen capture allowed), clicking will change it to true (screen capture disabled)
    const newState = !this.state.screenOn;
    this.setState({ screenOn: newState });
    disallowScreenshot(newState);
  };

  handleKeepAwake = () => {
    const newState = !this.state.isVisible;
    this.setState({ isVisible: newState });
    keepAwake(newState);
  };

  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.status}>
          Anti screenshot status: {this.state.screenOn ? 'banned' : 'allowed'}
        </Text>
        <Button
          title={this.state.screenOn ? "Allow screenshots" : "Ban screenshots"}
          onPress={this.handleDisallowScreenshot}
        />
        <Text style={styles.status}>
          Screen keep awake status: {this.state.isVisible ? 'enabled' : 'disabled'}
        </Text>
        <Button
          title={this.state.isVisible ? "Disable screen keep awake" : "Enable screen keep awake"}
          onPress={this.handleKeepAwake}
        />
      </View>
    )
  };
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    flexDirection: 'column',
    alignItems: 'center'
  },
  label: {
    fontSize: 30
  },
  status: {
    fontSize: 18,
    marginVertical: 10,
    color: '#333'
  }
})

export default AppDemo;

```

## Link
  <summary>this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

### 1. Overrides RN SDK

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

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
  "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
  "@react-native-ohos/react-native-screen-capture": "file:../../node_modules/@react-native-ohos/react-native-screen-capture/harmony/screen_capture.har"
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

### 3. Configuring CMakeLists and Introducing ScreenCapturePackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-screen-capture/src/main/cpp" ./screen-capture)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_screen_capture)
# RNOH_END: manual_package_linking_2

```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ScreenCapturePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ScreenCapturePackage>(ctx)
    };
}
```

### 4.Introducing ScreenCapturePackage to ArkTS 

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { ScreenCapturePackage } from '@react-native-ohos/react-native-screen-capture/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+    new ScreenCapturePackage(ctx)
  ];
}
```

## Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility


To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### Permission Requirements

(Enter the related permission configuration.)

Add the following permissions to their respective files:

In your `entry/src/main/module.json5`

```
 "requestPermissions": [
    {
      "name": "ohos.permission.PRIVACY_WINDOW"
    }
  ]
```

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| disallowScreenshot  | Whether to disallow screenshots | function  | yes | ios/andriod      | yes |
| keepAwake  | Whether to keep the device awake | function  | yes | ios/andriod      | yes |

## API Parameters Introduction

### disallowScreenshot(state: boolean);
* **state**: A parameter of type boolean, used to switch the state. False denote allow screenshots, true denote disallow screenshots.
  
### keepAwake(state: boolean);
* **state**: A parameter of type boolean, used to switch the state. False denote allow screen sleep, true denote keep screen awake.

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/recepkocur/react-native-screen-capture/blob/0.2.3/LICENSE).
