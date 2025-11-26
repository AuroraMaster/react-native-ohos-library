> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-theme-control</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/vonovak/react-native-theme-control">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vonovak/react-native-theme-control/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-theme-control)

Please check the matching version information at the Releases page of the third-party library:

| Version                        | Package Name                                  | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 6.0.1 | @react-native-oh-tpl/react-native-theme-control | [Github](https://github.com/react-native-oh-library/react-native-theme-control) | [Github Releases](https://github.com/react-native-oh-library/react-native-theme-control/releases) | 0.72 |
| 6.1.1                        | @react-native-ohos/react-native-theme-control       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-theme-control) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-theme-control/releases) | 0.77 |

## Installation and Usage

Navigate to the project directory and enter the following commands:

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-theme-control

# 0.77
npm install @react-native-ohos/react-native-theme-control
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-theme-control

# 0.77
yarn add @react-native-ohos/react-native-theme-control
```

> [!TIP] This library also depends on [react-native-community/segmented-control](/en/react-native-community-segmented-control.md)

<!-- tabs:end -->

The following code shows the basic usage scenario of this library:

> [!WARNING] When using it, the imported library name remains unchanged.

```js
import * as React from 'react';
import { Text, useColorScheme, View } from 'react-native';
import {
    setThemePreference,
    SystemBars,
    ThemePreference,
    useThemePreference,
} from '@vonovak/react-native-theme-control';
// @ts-ignore
import SegmentedControl from '@react-native-segmented-control/segmented-control/js/SegmentedControl.js';

export function SimpleScreen() {
    const colorScheme = useColorScheme();
    const isDarkMode = colorScheme === 'dark';
    const themePreference = useThemePreference();
    const bgColor = isDarkMode ? '#2A2550' : '#FFF6EA';
    const textColor = isDarkMode ? 'white' : 'black';
    const barsBackground = isDarkMode ? '#9900F0' : '#A0BCC2';
    const dividerColor = textColor;
    const textColorStyle = { color: textColor };
    const values: Array<ThemePreference> = ['light', 'dark', 'system'];
    return (
        <View
            style={{
                backgroundColor: bgColor,
                flexGrow: 1,
                flexShrink: 1,
                alignItems: 'center',
                justifyContent: 'space-evenly',
            }}
        >
            <SystemBars
                backgroundColor={barsBackground}
                dividerColor={dividerColor}
            />
            <SegmentedControl
                style={{ width: '100%' }}
                values={values}
                selectedIndex={values.indexOf(themePreference)}
                onChange={({ nativeEvent }: { nativeEvent: any }) => {
                    setThemePreference(nativeEvent.value as ThemePreference);
                }}
            />
            <Text style={textColorStyle}>useColorScheme(): {colorScheme}</Text>
            <Text style={textColorStyle}>
                useThemePreference(): {themePreference}
            </Text>
        </View>
    );
}
```

## Use Codegen

> [!TIP] V0.77 does not require Codegen execution.

This library has been adapted to `Codegen`. Before using it, you need to actively generate the third-party library bridge code. For details, please refer to [Codegen Usage Document](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink, so the Link step needs to be manually configured.

First, you need to open the HarmonyOS project `harmony` in the project with DevEco Studio.

### 1. Add overrides field in `oh-package.json5` in the project root directory

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Import native code

There are currently two methods:

1. Import through har package (this method will be deprecated after the IDE improves related functions, currently the preferred method);
2. Directly link the source code.

Method 1: Import through har package (recommended)

> [!TIP] The har package is located in the `harmony` folder of the third-party library installation path.

Open `entry/oh-package.json5` and add the following dependencies:

- 0.72

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-theme-control": "file:../../node_modules/@react-native-oh-tpl/react-native-theme-control/harmony/themecontrol.har"
  }
```

- 0.77

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-theme-control": "file:../../node_modules/@react-native-ohos/react-native-theme-control/harmony/themecontrol.har"
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

### 3. Configure CMakeLists and import RNThemeControlPackage

> [!TIP] V0.77 needs to configure CMakeLists and import RNThemeControlPackage.

Open `entry/src/main/cpp/CMakeLists.txt` and add:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/@react-native-ohos/react-native-theme-control/src/main/cpp" ./themecontrol)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_theme_control)
# RNOH_BEGIN: manual_package_linking_2
```

> [!Tip] Note: The NODE_MODULES definition above is the installation path of the source library. Users can define NODE_MODULES according to the path where the source library is installed.

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNThemeControlPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNThemeControlPackage>(ctx)
    };
}
```

### 4. Import RNThemeControlPackage on the ArkTs side

Open `entry/src/main/ets/RNPackagesFactory.ts` and add:

```diff
  ...
// 0.72
+ import { RNThemeControlPackage } from '@react-native-oh-tpl/react-native-theme-control/ts'

// 0.77
+ import { RNThemeControlPackage } from '@react-native-ohos/react-native-theme-control/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNThemeControlPackage(ctx)
  ];
}
```

### 5. Add the `MyAbilityStage.ets` in `entry/src/main/ets/abilityStage`

Open the `entry/src/main/ets/abilityStage/MyAbilityStage.ets` file and add the following code:

```diff
import appRecovery from '@ohos.app.ability.appRecovery';
import AbilityStage from '@ohos.app.ability.AbilityStage';
import { Want } from '@kit.AbilityKit';

export default class MyAbilityStage extends AbilityStage {
  onCreate() {
      appRecovery.enableAppRecovery(
      appRecovery.RestartFlag.ALWAYS_RESTART,
      appRecovery.SaveOccasionFlag.SAVE_WHEN_ERROR,
      appRecovery.SaveModeFlag.SAVE_WITH_FILE
    );

    let wantObj: Want = {
      bundleName: 'com.rnoh.tester',
      abilityName: 'EntryAbility'
    };

    appRecovery.setRestartWant(wantObj)
  }
}
```

### 6. Open the `entry/src/main/ets/entryability/EntryAbility.ets` file and add the following code:

Open `entry/src/main/ets/entryability/EntryAbility.ets` and add:

```diff
+ import {RNAbility} from '@rnoh/react-native-openharmony';
+ import Want from '@ohos.app.ability.Want';
// 0.72
+ import { RNThemeControlModule } from '@react-native-oh-tpl/react-native-theme-control';

// 0.77
+ import { RNThemeControlModule } from '@react-native-ohos/react-native-theme-control';

+  export default class EntryAbility extends RNAbility {
+    onCreate(want: Want): void {
+    super.onCreate(want);
+    RNThemeControlModule.recoverApplicationTheme(this.context);
+   }
  getPagePath() {
    return 'pages/Index';
  }
}
```

Open the `entry/src/main/module.json5` file and add the following code：

```diff
"module": {
    "name": "entry",
+   "srcEntry": "./ets/abilityStage/MyAbilityStage.ets",
    "type": "entry",
    .....

"abilities": [
  {
    "name": "EntryAbility",
     .....
     "visible": true,
+    "recoverable": true,
     .....
```

### 7. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

Verified on the following versions:

1. RNOH:0.72.28; SDK:HarmonyOS NEXT DB2; IDE:DevEco Studio 5.0.3.500; ROM:3.0.0.28;
2. RNOH: 0.77.1;SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                | Description                                                                                                                                               | Type       | Required | Platform    | HarmonyOS Support |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | -------- | ----------- | ----------------- |
| SystemBars          | Setting the System Status Bar                                                                                                                             | Components | No       | IOS/Android | Yes               |
| NavigationBar       | Setting the Navigation Bar                                                                                                                                | Components | No       | Android     | No                |
| AppBackground       | Sets the background color of the UIApplication window (iOS) or the current Activity (Android).                                                            | Components | No       | IOS/Android | Yes               |
| setNavbarAppearance | Set the appearance of the navigation bar imperatively                                                                                                     | Function   | No       | Android     | No                |
| setAppBackground    | Set background color                                                                                                                                      | Function   | No       | IOS/Android | Yes               |
| setThemePreference  | Set the theme                                                                                                                                             | Function   | No       | IOS/Android | Yes               |
| getThemePreference  | Get Subject                                                                                                                                               | Function   | No       | IOS/Android | Yes               |
| useThemePreference  | A React hook that returns the current theme preference, which might be dark, light (if you have set the theme before by calling setAppearance) or system. | Function   | No       | IOS/Android | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/vonovak/react-native-theme-control/blob/main/LICENSE).