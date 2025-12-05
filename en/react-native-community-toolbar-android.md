> Template Version: v0.3.0

<p align="center">
  <h1 align="center"> <code>@react-native-community/toolbar-android</code> </h1>
</p>

This project is based on [@react-native-toolbar-android/toolbar-android@v0.2.1](https://github.com/react-native-toolbar-android/toolbar-android/tree/v0.2.1).

The third-party library repository has been migrated to Gitee and supports direct download from npm. The new package name is: `@react-native-ohos/toolbar-android`. The specific version relationships are as follows:

| Version | Package Name | Repository | Release | Supported RN Version |
|-----------------|-----|--------|----------------------------------- | ------------------ | 
| <= 0.2.1-0.0.4@deprecated  | @react-native-oh-tpl/toolbar-android| [Github(deprecated)](https://github.com/react-native-oh-library/toolbar-android)| [@react-native-oh-tpl/toolbar-android Releases(deprecated)](https://github.com/react-native-oh-library/toolbar-android/releases) | 0.72
| 0.2.2  | @react-native-ohos/toolbar-android | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_toolbar-android/tree/master)| [@react-native-ohos/toolbar-android Releases](https://gitcode.com/openharmony-sig/rntpc_toolbar-android/releases) | 0.72
| 0.3.0  | @react-native-ohos/toolbar-android | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_toolbar-android/tree/master)| [@react-native-ohos/toolbar-android Releases](https://gitcode.com/openharmony-sig/rntpc_toolbar-android/releases) | 0.77 

## 1. Installation & Usage

Navigate to your project directory and run the following command:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/toolbar-android
```

#### **yarn**

```bash
yarn add @react-native-ohos/toolbar-android
```

<!-- tabs:end -->

The following code demonstrates basic usage scenarios of this library:

> [!WARNING] The import library name remains unchanged during use.

```js
import React, { useState } from "react";
import { StyleSheet, View, Text } from "react-native";
import ToolbarAndroid from "@react-native-community/toolbar-android";
function App({}): JSX.Element {
  const [state, setState] = useState<{
    message?: string;
  }>({
    message: undefined,
  });

  const { message } = state;

  return (
    <View style={styles.container}>
      <ToolbarAndroid
        navIcon={require("./assets/ic_menu_black_24dp.png")}
        logo={require("./assets/icon_app.png")}
        title={"ToolbarAndroid Example"}
        subtitle={"ToolbarAndroid Subtitle"}
        titleColor={"#FFFFFF"}
        subtitleColor={"#FF00FF"}
        contentInsetStart={10}
        contentInsetEnd={10}
        rtl={false}
        style={styles.toolbar}
        actions={[
          {
            title: "Action1",
            icon: require("./assets/icon_phone.png"),
            show: "ifRoom",
            showWithText: true,
          },
        ]}
        overflowIcon={require("./assets/relay.png")}
        onIconClicked={() => setState({ message: "Clicked nav icon" })}
        onActionSelected={(position: number) =>
          setState({ message: `Clicked Menu-${position}` })
        }
      />
      <View style={styles.centerContainer}>
        <Text style={styles.headText}>
          Click nav or action icon will trigger some events!
        </Text>
        <Text style={styles.contentText}>{message}</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  toolbar: {
    backgroundColor: "#E9EAED",
    height: 56,
  },
  centerContainer: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#F5FCFF",
  },
  headText: {
    fontSize: 16,
  },
  contentText: {
    fontSize: 18,
    fontWeight: "bold",
    color: "#ff681f",
  },
});

export default App;
```

## 2. Manual Link

This step provides guidance for manually configuring native dependencies.

First, you need to open the HarmonyOS project `harmony` within your project using DevEco Studio.

### 2.1. Overrides RN SDK

To ensure the project depends on the same version of RN SDK, you need to add the overrides field to the root `oh-package.json5`, pointing to the RN SDK version required by the project. The replaced version can be a specific version number, a fuzzy version, or a locally existing HAR package or source code directory.

For details about this field, please read the [official documentation](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm online version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // path to local har package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // path to source code
  }
}
```

### 2.2. Import Native Code

There are currently two methods:

- Import via har package;
- Link source code directly.

Method 1: Import via har package (Recommended)

> [!TIP] The har package is located in the `harmony` folder of the installed third-party library path.

Open `entry/oh-package.json5` and add the following dependencies:

```json
"dependencies": {
    "@react-native-ohos/toolbar-android": "file:../../node_modules/@react-native-ohos/toolbar-android/harmony/toolbar_android.har"
  }
```

Click the `sync` button in the top right corner.

Or execute in the terminal:

```bash
cd entry
ohpm install
```

Method 2: Link Source Code Directly

> [!TIP] If you need to link source code directly, please refer to the [Direct Link Source Code Guide](/zh-cn/link-source-code.md)

### 2.3. Configure CMakeLists and Import ToolbarAndroidPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add:

```cmake
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

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/toolbar-android/src/main/cpp" ./toolbar-android)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_toolbar_android)
# RNOH_END: link_packages
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```c++
...
+ #include "ToolbarAndroidPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      ...
+     std::make_shared<ToolbarAndroidPackage>(ctx),
    };
}
```

### 2.4. Import RNCCheckBoxPackage on the ArkTS Side

> [!TIP] Required for version v0.2.22 and above

Open `entry/src/main/ets/RNPackagesFactory.ts` and add:

```typescript
  ...
+ import {ToolbarAndroidPackage} from '@react-native-ohos/toolbar-android/src/main/ets/ToolbarAndroidPackage';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   return [new ToolbarAndroidPackage(ctx)];
  ];
}
```

### 2.5. Import RNCToolbarAndroid Component on the ArkTS Side

Find **function buildCustomRNComponent()**, usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add:

```typescript
  ...
+ import { RNCToolbarAndroid} from '@react-native-ohos/toolbar-android/src/main/ets/RNCToolbarAndroid'

  @Builder
  function buildCustomRNComponent(ctx: ComponentBuilderContext) {
    ...
+   if (ctx.componentName === RNCToolbarAndroid.NAME) {
+     RNCToolbarAndroid({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag
+     })
+   }
    ...
  }
  ...
```

> [!TIP] This library uses a hybrid solution and requires adding the component name.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array:

```typescript
const arkTsComponentNames: Array<string> = [
  ...
+ RNCToolbarAndroid.NAME
];
```

### 2.6. Run

Click the `sync` button in the top right corner.

Or execute in the terminal:

```bash
cd entry
ohpm install
```

Then compile and run.

## 3. Constraints & Limitations

### 3.1 Compatibility

To use this library, you need the correct React-Native and RNOH versions. Additionally, you need to use the matching DevEco Studio and phone ROM.

Verified in the following versions:

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.868; ROM: 6.0.0.112;

## 4. Props

> [!TIP] The "Platform" column indicates the platforms supported by the original third-party library for that property.

> [!TIP] The "HarmonyOS Support" column: 'Yes' means the property is supported on the HarmonyOS platform; 'No' means it is not supported; 'partially' means partial support. The usage method is consistent across platforms, with effects benchmarked against iOS or Android.

Inherits [View Props](https://reactnative.dev/docs/view#props).

| Name | Description | Type | Required | Platform | HarmonyOS Support |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|-----------|----------|-------------------|
| actions | Sets possible actions on the toolbar as part of the action menu. These are displayed as icons or text on the right side of the widget. If they don't fit they are placed in an 'overflow' menu. | array of object: {title: string,icon: ImageSource,show: enum('always', 'ifRoom', 'never'),showWithText: bool} | No | Android | Yes |
| contentInsetStart | Sets the content inset for the toolbar starting edge. | number | No | Android | Yes |
| contentInsetEnd | Sets the content inset for the toolbar ending edge. | number | No | Android | Yes |
| logo | Sets the toolbar logo. | ImageSource | No | Android | Yes |
| navIcon | Sets the navigation icon. | ImageSource | No | Android | Yes |
| onActionSelected | Callback that is called when an action is selected. The only argument that is passed to the callback is the position of the action in the actions array. | function | No | Android | Yes |
| onIconClicked | Callback called when the icon is selected. | function | No | Android | Yes |
| overflowIcon | Sets the overflow icon. | ImageSource | No | Android | Yes |
| rtl | Used to set the toolbar direction to RTL. | bool | No | Android | Yes |
| subtitle | Sets the toolbar subtitle. | string | No | Android | Yes |
| subtitleColor | Sets the toolbar subtitle color. | string | No | Android | Yes |
| title | Sets the toolbar title. | string | No | Android | Yes |
| titleColor | Sets the toolbar title color. | string | No | Android | Yes |

#### 4.1. Props of ImageSource

| Name | Description | Type | Required | Platform | HarmonyOS Support |
|------|---------------------------------------------------------------------------------------------------------------------------------------|--------|----------|----------|-------------------|
| uri | load image from a url, e.g. require('./some_icon.png') | string | Yes | android | Yes |
| width | the width of the image | number | No | android | Yes |
| height | the height of the image | number | No | android | Yes |

## 5. Known Issues

## 6. Others

## 7. License

This project is based on [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_toolbar-android/blob/master/LICENSE). Feel free to enjoy and contribute to open source.