> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-theme-control)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 6.0.1-1.0.3@deprecated     | [@react-native-oh-tpl/react-native-theme-control Releases(deprecated)](https://github.com/react-native-oh-library/react-native-theme-control/releases) | 0.72       |
| 6.0.2      | [@react-native-ohos/react-native-theme-control Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-theme-control/releases) | 0.72       |
| 6.1.1      | [@react-native-ohos/react-native-theme-control Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-theme-control/releases) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-theme-control
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-theme-control
```

> [!TIP] 本库还依赖了[react-native-community/segmented-control](/zh-cn/react-native-community-segmented-control.md)

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

## 使用 Codegen

Version >= @react-native-ohos/react-native-theme-control@6.0.2，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-theme-control@6.0.2，已支持 Autolink，无需手动配置（仍需手动配置的内容已在对应标题处标记），目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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
    "@react-native-ohos/react-native-theme-control": "file:../../node_modules/@react-native-ohos/react-native-theme-control/harmony/themecontrol.har"
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

### 3.配置 CMakeLists 和引入 RNThemeControlPackage

> 若使用的是 <= 6.0.1-1.0.3 版本，请跳过本章。


打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

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

> [!Tip] 注意：上面NODE_MODULES定义，为源库的安装路径，用户可以根据安装源库的路径定义NODE_MODULES

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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

### 4.在 ArkTs 侧引入 RNThemeControlPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNThemeControlPackage } from '@react-native-ohos/react-native-theme-control/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNThemeControlPackage(ctx)
  ];
}
```

### 5.在 `entry/src/main/ets/abilityStage` 新建 `MyAbilityStage.ets`（该模块始终需要手动配置）

打开 `entry/src/main/ets/abilityStage/MyAbilityStage.ets`，添加：

```js
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

### 6.在 entry/src/main/ets/entryability/EntryAbility.ets 配置生命周期调用（该模块始终需要手动配置）

打开 `entry/src/main/ets/entryability/EntryAbility.ets`，添加：

```diff
+ import {RNAbility} from '@rnoh/react-native-openharmony';
+ import Want from '@ohos.app.ability.Want';
+ import { RNThemeControlModule } from '@react-native-ohos/react-native-theme-control';
    .....
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

打开 `entry/src/main/module.json5`，添加：

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

### 7.运行

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

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description                                                  | Type       | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ---------- | -------- | ----------- | ----------------- |
| `SystemBars`          | 设置系统状态栏                                               | Components | No       | IOS/Android | Yes               |
| `NavigationBar`       | 设置导航栏                                                   | Components | No       | Android     | No                |
| `AppBackground`       | 设置 UIApplication 窗口（iOS）或当前 Activity（Android）的背景色 | Components | No       | IOS/Android | Yes               |
| `setNavbarAppearance` | 主动设置导航栏的外观                                         | Function   | No       | Android     | No                |
| `setAppBackground`    | 设置背景颜色                                                 | Function   | No       | IOS/Android | Yes               |
| `setThemePreference`  | 设置主题                                                     | Function   | No       | IOS/Android | Yes               |
| `getThemePreference`  | 获取主题                                                     | Function   | No       | IOS/Android | Yes               |
| `useThemePreference`  | 一个 React 钩子，返回当前的主题偏好，可能是暗色、亮色（如果您之前调用 setAppearance 设置过主题）或系统默认 | Function   | No       | IOS/Android | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/vonovak/react-native-theme-control/blob/main/LICENSE) ，请自由地享受和参与开源。
