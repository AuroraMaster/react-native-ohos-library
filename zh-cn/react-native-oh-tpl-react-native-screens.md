> 模板版本：v0.2.2

<p align="center">[react-native-oh-tpl-react-native-screens.md](../en/react-native-oh-tpl-react-native-screens.md)
  <h1 align="center"> <code>@react-native-oh-tpl/react-native-screens</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-screens">
        <img src="https://img.shields.io/badge/platforms-iOS%20|%20Android%20|%20tvOS%20|%20Windows%20|%20Web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/software-mansion/react-native-screens/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-harmony-screens)

## 安装与使用
### 3.34.0
本库实现依赖 @react-navigation/native 、 @react-navigation/native-stack 、 @react-native-oh-tpl/react-native-safe-area-context 、 @react-native-oh-tpl/react-native-gesture-handler 的原生端代码，如已在工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

注：若已引入 `@react-native-oh-tpl/native-stack` 库，请务必卸载，否则本库将无法正确指向，导致无法使用。

如未引入请参照 [@react-navigation/native 文档的 Link 章节](/zh-cn/react-navigation-native.md) ，[@react-native-oh-tpl/react-native-gesture-handler 文档的 Link 章节](/zh-cn/react-native-gesture-handler.md) ，[@react-native-oh-tpl/react-native-safe-area-context 文档的 Link 章节](/zh-cn/react-native-safe-area-context.md)进行引入。

### 3.34.1
本库实现依赖 @react-navigation/native 、 @react-navigation/native-stack 、 @react-native-ohos/react-native-safe-area-context 、 @react-native-ohos/react-native-gesture-handler、@react-native-ohos/react-native-reanimated 的原生端代码，如已在工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

注：若已引入 `@react-native-oh-tpl/native-stack，@react-native-ohos/native-stack` 库，请务必卸载，否则本库将无法正确指向，导致无法使用。

如未引入请参照 [@react-navigation/native 文档的 Link 章节](/zh-cn/react-navigation-native.md) ，[@react-native-ohos/react-native-gesture-handler 文档的 Link 章节](/zh-cn/react-native-gesture-handler.md) ，[@react-native-ohos/react-native-safe-area-context 文档的 Link 章节](/zh-cn/react-native-safe-area-context.md)，[@react-native-ohos/react-native-reanimated 文档的 Link 章节](/zh-cn/react-native-reanimated.md)进行引入。

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                  | 支持RN版本 |
|--------| ------------------------------------------------------------ | ---------- |
| <= 3.34.0-0.0.2@deprecated  | [@react-native-oh-tpl/react-native-screens Releases(deprecated)](https://github.com/react-native-oh-library/react-native-harmony-screens/releases) | 0.72       |
| 3.34.1             | [@react-native-ohos/react-native-screens Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-screens/releases)   | 0.72       |
| 4.8.1              | [@react-native-ohos/react-native-screens Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-screens/releases)   | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

#### **npm**

```bash
# 0.72
npm install @react-native-ohos/react-native-screens@3.34.1-X.X.X
npm install @react-navigation/native-stack@6.9.13

# 0.77
npm install @react-native-ohos/react-native-screens@4.8.1-X.X.X
npm install @react-navigation/native-stack@7.2.0
```

#### **yarn**

```bash
# 0.72
yarn install @react-native-ohos/react-native-screens@3.34.1-X.X.X
yarn install @react-navigation/native-stack@6.9.13

# 0.77
yarn install @react-native-ohos/react-native-screens@4.8.1-X.X.X
yarn install @react-navigation/native-stack@7.2.0
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import { Button, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import { enableScreens } from "react-native-screens";
enableScreens(true);

function HomeScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button
        title="Go to Profile"
        onPress={() => navigation.navigate('Profile')}
      />
    </View>
  );
}

function ProfileScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button
        title="Go to Notifications"
        onPress={() => navigation.navigate('Notifications')}
      />
      <Button title="Go back" onPress={() => navigation.goBack()} />
    </View>
  );
}

function NotificationsScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button
        title="Go to Settings"
        onPress={() => navigation.navigate('Settings')}
      />
      <Button title="Go back" onPress={() => navigation.goBack()} />
    </View>
  );
}

function SettingsScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button title="Go back" onPress={() => navigation.goBack()} />
    </View>
  );
}

const Stack = createNativeStackNavigator();

function MyStack() {
  return (
    <Stack.Navigator
      initialRouteName="Home"
      screenOptions={{
        headerTintColor: '#999999',
        headerStyle: { backgroundColor: '#ff00ff' },
      }}
    >
      <Stack.Screen name="Home" component={HomeScreen} />
      <Stack.Screen name="Notifications" component={NotificationsScreen} />
      <Stack.Screen name="Profile" component={ProfileScreen} />
      <Stack.Screen name="Settings" component={SettingsScreen} />
    </Stack.Navigator>
  );
}

export default function App() {
  return (
    <NavigationContainer>
      <MyStack />
    </NavigationContainer>
  );
}

```

##  使用 Codegen

Version >= @react-native-ohos/react-native-screens@3.34.1，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-screens@3.34.1，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的HarmonyOS工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:../node_modules/@rnoh/react-native-harmony/harmony/react_native_openharmony.har"
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
    "@rnoh/react-native-openharmony": "file:../../node_modules/@rnoh/react-native-harmony/harmony/react_native_openharmony.har",
    "@react-native-ohos/react-native-screens": "file:../../node_modules/@react-native-ohos/react-native-screens/harmony/screens.har"
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

### 3.配置 CMakeLists 和引入 Package

> 若使用的是 <= 3.34.0-0.0.2 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
+ set(OH_MODULES_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES_DIR}/@react-native-ohos/react-native-screens/src/main/cpp" ./rnoh_screens)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_screens)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "RnohReactNativeHarmonyScreensPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+        std::make_shared<rnoh::RnohReactNativeHarmonyScreensPackage>(ctx),
    };
}
```

### 4.在ArkTs侧导入组件

找到 function buildCustomRNComponent()，一般位于 entry/src/main/ets/pages/index.ets 或 entry/src/main/ets/rn/LoadBundle.ets，添加：

```diff
  ...
+ import { componentBuilder } from "@react-native-ohos/react-native-screens"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
  Stack() {
+    componentBuilder(ctx)
  }
  ...
}
...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。

在entry/src/main/ets/pages/index.ets 或 entry/src/main/ets/rn/LoadBundle.ets 找到常量 arkTsComponentNames 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
+ "RNSScreen", 
+ "RNSFullWindowOverlay", 
+ "RNSModalScreen", 
+ "RNSScreenContainer", 
+ "RNSScreenNavigationContainer", 
+ "RNSScreenStack", 
+ "RNSScreenStackHeaderSubview", 
+ "RNSSearchBar", 
+ "RNSScreenStackHeaderConfig", 
];
```

### 5.在ArkTs侧引入Package

打开 `src/main/ets/RNOHPackagesFactory.ets`，添加：

```diff
  ...
import type { RNPackageContext, RNPackage } from '@rnoh/react-native-openharmony';
+ import RnohReactNativeHarmonyScreensPackage from '@react-native-ohos/react-native-screens';

export function createRNOHPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+    new RnohReactNativeHarmonyScreensPackage(ctx),
  ];
}

```

### 6.运行

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

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                                      | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| --------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| enableScreens                                             | 支持原生及其 React Native View                               | function | No       | iOS Android | Yes               |
| enableFreeze                                              | 对 react-freeze 的支持，使用 ReactSuspense 机制来防止 React 组件树的部分渲染 | function | No       | iOS Android | Yes               |
| createNativeStackNavigator                                | 提供屏幕切换的能力                                                                             | function | No       | iOS Android | NO                |
| NativeStackNavigationProp                                 | 切换页面属性的封装                                                                             | object   | No       | iOS Android | Yes               |
| NativeStackNavigationOptions                              | 导航栏属性设置封装                                                                             | object   | No       | iOS Android | NO                |
| FullWindowOverlay                                         | 一个组件，可以将其子组件放在其他组件之上                                                                  | object   | No       | iOS Android | NO                |
| SearchBarProps                                            | 搜索栏的属性设置封装                                                                            | object   | No       | iOS Android | NO                |
| SearchBarCommands                                         | 搜索栏的操作封装                                                                              | object   | No       | iOS Android | NO                |
| useTransitionProgress                                     | 提供屏幕过渡的动画插值器                                                                          | function | No       | iOS Android | NO                |
| userReanimatedTransitionProgress ReanimatedScreenProvider | 屏幕切换期间调用的帧回调，用于 react-native-reanimated 2.0 及其以上的版本，并使用 ReanimatedScreenProvider 进行封装 | function | No       | iOS Android | NO                |
| userHeaderHeight                                          | 计算静态标题栏的高度，当屏幕方向发生更改，此值会发生更改                                                          | function | No       | iOS Android | NO                |
| userAnimatedHeaderHeight                                  | 动态计算标题栏的高度，此值会随着每个视图布局变化而变化                                                           | function | No       | iOS Android | NO                |
| onAppear                                 | 页面显示         | function | No       | iOS Android |   Yes |
| onDisappear                              | 页面消失         | function | No       | iOS Android |   Yes |
| onWillAppear                             | 页面将显示       | function | No       | iOS Android |   Yes |
| onWillDisappear                          | 页面将消失       | function | No       | iOS Android |   Yes |
| fullScreenSwipeEnabled                   | 全屏滑动         | property | No       | iOS Android |   Yes |
| gestureEnabled                           | 是否开启手势滑动 | property | No       | iOS Android |   Yes |
| statusBarColor                           | 状态栏颜色       | property | No       | Android |   No  |
| screenOrientation                        | 屏幕显示方向     | property | No       | iOS Android |   Yes |
| statusBarStyle                           | 状态栏样式       | property | No       | iOS Android |   Yes |
| statusBarTranslucent                     | 状态栏是否透明化       | property | No       | iOS Android | Yes |
| statusBarHidden			   | 隐藏状态栏       | property | No       | iOS Android |   Yes |
| gestureResponseDistance                  | 手势滑动的有效区域       | property | No       | iOS Android |   Yes |
| stackPresentation                        | 页面类型       | property | No       | iOS Android |   Yes |
| stackAnimation                           | 转场动画类型       | property | No       | iOS Android |   Yes |
| replaceAnimation                         | 进出栈类型       | property | No       | iOS Android |   Yes |
| backgroundColor                          | 标题栏背景色       | property | No       | iOS Android |   Yes |
| hidden                           | 隐藏标题栏       | property | No       | iOS Android |   Yes |
| translucent                      | 标题栏是否透明化       | property | No       | iOS Android |   Yes |
| hideBackButton                   | 隐藏标题栏返回按钮      | property | No       | iOS Android |   Yes |
| backTitle                        | 返回按钮文本内容       | property | No       | iOS Android |   Yes |
| backTitleFontSize                | 返回按钮文本字号大小    | property | No       | iOS Android |   Yes |
| backTitleVisible                 | 返回按钮文本是否显示    | property | No       | iOS Android |  Yes |
| backTitleVisible<sup>4.8.1</sup>                 | 返回按钮文本是否显示    | property | No       | iOS Android |  No  |
| title                            | 标题栏标题       | property | No       | iOS Android |   Yes |
| titleFontSize                    | 标题字号大小        | property | No       | iOS Android |   Yes |
| titleFontWeight                  | 标题字号比重       | property | No       | iOS Android |   Yes |
| titleColor                       | 标题颜色 | property | No       | iOS Android |   Yes |
| type                             | 子标题类型      | property | No       | iOS Android |   Yes |
| onSearchFocus                    | 搜索栏聚焦       | function | No       | iOS Android |   Yes |
| onSearchBlur                     | 搜索栏失去焦点       | function | No       | iOS Android |   Yes |
| onSearchButtonPress              | 搜索       | function | No       | iOS Android |   Yes |
| onCancelButtonPress              | 取消搜索       | function | No       | iOS Android |   Yes |
| onChangeText                     | 搜索栏文本变更       | function | No       | iOS Android |   Yes |
| cancelButtonText                 | 取消按钮文本内容       | property | No       | iOS Android |   Yes |
| barTintColor                     | 搜索背景色       | property | No       | iOS Android |   Yes |
| tintColor                        | 搜索提示文字颜色       | property | No       | iOS Android |   Yes |
| textColor                        | 文字颜色       | property | No       | iOS Android |   Yes |
| inputType                        | 文本输入类型       | property | No       | iOS Android |   Yes |
| onClose                          | 关闭搜索       | function | No       | iOS Android |   Yes |
| onOpen                           | 展示搜索       | function | No       | iOS Android |   Yes |
| headerIconColor                  | 图标颜色       | property | No       | iOS Android |   Yes |
| shouldShowHintSearchIcon         | 是否隐藏搜索图标       | property | No       | iOS Android |   Yes |
| blurEffect<sup>4.8.1</sup>       | 应用于页眉的模糊效果       | property | No       | iOS  |   Yes |
| tintColor<sup>4.8.1</sup>       | 光标插入符和取消按钮文本的颜色       | property | No       | iOS  |   Yes |
| color<sup>4.8.1</sup>         | 控制标题上呈现的项目的颜色。这包括后退图标、后退文本（仅限iOS）和标题文本。如果希望标题具有不同的颜色，请使用titleColor属性。       | property | No       | iOS Android |   Yes |
| hideWhenScrolling<sup>4.8.1</sup>         | 布尔值，指示滚动时是否隐藏搜索栏。默认为“true”。       | property | No       | iOS  |   No |
| largeTitle<sup>4.8.1</sup>         | 当设置为“true”时，它会使用大标题效果显示标题。       | property | No       | iOS  |   No |
| largeTitleFontFamily<sup>4.8.1</sup>          | 自定义用于大标题的字体系列。        | property | No       | iOS  |   No |
| largeTitleFontSize<sup>4.8.1</sup>         | 自定义用于大标题的字体大小。       | property | No       | iOS  |   No |
| largeTitleFontWeight<sup>4.8.1</sup>         | 自定义用于大标题的字体的粗细。       | property | No       | iOS  |   No |
| largeTitleHideShadow<sup>4.8.1</sup>         | 布尔值，允许在任何可滚动内容的边缘到达导航栏的匹配边缘时禁用导航标题下的阴影。       | property | No       | iOS  |   No |
| largeTitleColor<sup>4.8.1</sup>         | 自定义用于大标题的颜色。默认情况下使用`titleColor`属性。       | property | No       | iOS  |   No |
| autoCapitalize<sup>4.8.1</sup>         | 控制用户输入文本时是否自动大写。   | property | No       | iOS  |   No |
| placement<sup>4.8.1</sup>         | 将搜索栏放置在导航栏中       | property | No       | iOS  |   No |
| obscureBackground<sup>4.8.1</sup>         | 布尔值，指示是否使用半透明覆盖来遮挡底层内容。默认为“true”。       | property | No       | iOS  |   No |
| hideNavigationBar<sup>4.8.1</sup>         | 布尔值，指示在搜索过程中是否隐藏导航栏。       | property | No       | iOS  |   No |
| disableBackButtonOverride<sup>4.8.1</sup>         | 默认行为是在搜索栏打开时 阻止屏幕返回（`disableBackButtonOverride:false `）。如果你不想发生这种情况，请将“disableBackButtonOverride”设置为“true”。       | property | No       | Android  |   No |
| customAnimationOnSwipe<sup>4.8.1</sup>         |  布尔值，表示滑动解除应触发“stackAnimation”提供的动画。默认为“false”。      | property | No       | iOS  |   No |
| fullScreenSwipeShadowEnabled<sup>4.8.1</sup>         | 布尔值，指示全屏解除手势在过渡期间是否在视图下有阴影。手势使用自定义过渡，因此默认情况下没有阴影。启用后，在转换过程中会添加一个自定义阴影视图，试图模仿默认iOS阴影。默认为“true”。       | property | No       | iOS  |   No |
| homeIndicatorHidden<sup>4.8.1</sup>         | 主页指示器是否应在此屏幕上隐藏。默认为“false”。       | property | No       | iOS  |   No |
| statusBarAnimation<sup>4.8.1</sup>         | 设置状态栏动画（类似于“StatusBar”组件）。需要在Info.plist文件中启用（或删除）“基于视图控制器的状态栏外观”。在Android上，此道具考虑了更改状态栏颜色的过渡.如果“无”提供，则不会有动画。      | property | No       | iOS  |   No |
| transitionDuration         | 更改iOS上“slide_from_bottom”、“fade_from_bottom”和“fade”和“simple_push”转换的持续时间（以毫秒为单位）。默认为“500”。“默认”和“翻转”过渡的持续时间是不可定制的。       | property | No       | iOS  |   No |
| hideKeyboardOnSwipe<sup>4.8.1</sup>         | 滑至上一屏幕时，键盘是否应隐藏。默认为“false”。       | property | No       | iOS  |   No |
| disableBackButtonMenu<sup>4.8.1</sup>         | 布尔值，指示是否在iOS>=14的longPress后退按钮上显示菜单。       | property | No       | iOS  |   No |
| backButtonDisplayMode<sup>4.8.1</sup>         |  枚举值表示**默认**后退按钮的显示模式。它适用于iOS>=14，仅在未设置“backTitleFontFamily”、“backTitle FontSize”、“disableBackButtonMenu”或“backTitle”时使用。否则，当按钮被定制时，在幕后我们使用iOS原生的`backButtonItem`，它覆盖了`backButtonDisplayMode`。      | property | No       | iOS  |   No |
| backButtonInCustomView<sup>4.8.1</sup>         | 是否显示带有自定义页眉左侧的后退按钮。       | property | No       | iOS  |   No |
| direction        | 控制堆栈应采用“rtl”还是“ltr”形式。        | property | No       | iOS Android |   No |
| topInsetEnabled<sup>4.8.1</sup>         | 一个标志，可以让你选择不插入标题。如果您使用不透明的状态栏，您可能希望将其设置为“false”。默认为“true”。       | property | No       | Android  |   No |

## 遗留问题
- [ ] formSheet页面暂使用普通页面，该页面使用的Context.openBindSheet系统方法存在绑定的js页面绑定的位置错乱，造成按钮事件会无法响应。需要系统修正后补充。  [issue#4](https://github.com/react-native-oh-library/react-native-harmony-screens/issues/4)

- [ ] RNSScreenFooter依赖formSheet。需要实现formSheet功能后再补充该功能。  [issue#28](https://github.com/react-native-oh-library/react-native-harmony-screens/issues/28)

- [ ] GestureDetectorProvider按原库的引用方式在77环境上引用不到，需要系统框架定位处理。  [issue#29](https://github.com/react-native-oh-library/react-native-harmony-screens/issues/29)

- [ ] 在Screen和其子组件中通过Option有设置不同属性时，在77环境ets侧接收到的属性有丢失。需要系统框架定位处理后。  [issue#30](https://github.com/react-native-oh-library/react-native-harmony-screens/issues/30)

- [ ] sheetInitialDetent 打开后，表单的棘爪索引应扩展到。formsheet功能的属性。 未实现
- [ ] sheetElevation 描述表单标高的整数值，影响表单顶部边缘的阴影。formsheet功能的属性。 未实现
- [ ] sheetAllowedDetents 描述表单可以放置的高度。formsheet功能的属性。 未实现
- [ ] sheetLargestUndimmedDetent 最大的表单棘爪，其下方视图不会变暗。formsheet功能的属性。 未实现
- [ ] sheetGrabberVisible 布尔值，指示工作表顶部是否显示抓取器。formsheet功能的属性。 未实现
- [ ] sheetCornerRadius 表单将尝试渲染的角半径。formsheet功能的属性。 未实现
- [ ] sheetExpandsWhenScrolledToEdge 滚动时，表单是否应扩展到更大的棘爪。formsheet功能的属性。 未实现
- [ ] onSheetDetentChanged 当当前屏幕处于“formSheet”演示状态并且其定位符已更改时调用的回调。formsheet功能的回调。 未实现

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/software-mansion/react-native-screens/blob/main/LICENSE) ，请自由地享受和参与开源。
