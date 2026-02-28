> 模板版本：v0.4.0

<p align="center">
  <h1 align="center"> <code>react-native-reanimated</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-reanimated">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/software-mansion/react-native-reanimated/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

本项目基于 [原库react-native-reanimated](https://github.com/software-mansion/react-native-reanimated) 开发。

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：@react-native-ohos/react-native-reanimatedt 版本所属关系如下：


|三方库名称| 三方库版本 | 发布信息 | 支持RN版本 |Autolink|编译API版本|社区基线版本|npm地址|
|-------|-------|-----| ---------- |---------- |---------- |---------- |---------- |
|@react-native-ohos/react-native-reanimated| ~4.0.0 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-reanimated/releases)               | 0.82       |否|API12+|4.2.1 |[Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-reanimated)|
|@react-native-ohos/react-native-reanimated| ~3.18.1 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-reanimated/releases)               | 0.77       |否|API12+|3.18.0 |[Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-reanimated)|
|@react-native-ohos/react-native-reanimated| ~3.6.5 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-reanimated/releases)               | 0.72       |是|API12+|3.6.0 |[Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-reanimated)|
|@react-native-oh-tpl/react-native-reanimated| <= 3.6.4@deprecated | [ Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-harmony-reanimated/releases) | 0.72       | 否|API12+| 3.6.0 |[Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/react-native-reanimated)|


## 1、安装与使用

> [!TIP] 注意：
`react-native-reanimated version >= 4.0.0`, `worklets` 已单独独立成库，需要单独引入，参照[@react-native-ohos/react-native-worklets文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-worklets.md)。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# RN 0.72
npm install react-native-reanimated@3.6.0
npm install @react-native-ohos/react-native-reanimated

# RN 0.77
npm install react-native-reanimated@3.18.0
npm install @react-native-ohos/react-native-reanimated

# RN 0.82
npm install react-native-reanimated@4.2.1
npm install @react-native-ohos/react-native-reanimated
```

#### **yarn**

```bash
# RN 0.72
yarn add react-native-reanimated@3.6.0
yarn add @react-native-ohos/react-native-reanimated

# RN 0.77
yarn add react-native-reanimated@3.18.0
yarn add @react-native-ohos/react-native-reanimated

# RN 0.82
yarn add react-native-reanimated@4.2.1
yarn add @react-native-ohos/react-native-reanimated
```
<!-- tabs:end -->

#### 插件配置

添加插件到 `babel.config.js`:

> [!TIP] 为什么需要添加这个？Reanimated Babel 插件会自动转换特殊的 JavaScript 函数（称为 worklet），以便它们可以被传递并在 UI 线程上运行。

```js
  module.exports = {
    presets: [
      ... // don't add it here :)
    ],
    plugins: [
      ...
      // version < 4.0.0
      'react-native-reanimated/plugin',

      // version >= 4.0.0
      'react-native-worklets/plugin',
    ],
  };
```

清除 Metro 的缓存（推荐）:

<!-- tabs:start -->

#### **npm**

```bash
npm start --reset-cache
```

#### **yarn**

```bash
yarn start --reset-cache
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { Button, View } from "react-native";
import Animated, { useSharedValue, withSpring } from "react-native-reanimated";

export default function App() {
  const width = useSharedValue(100);

  const handlePress = () => {
    width.value = withSpring(width.value + 50);
  };

  return (
    <View style={{ flex: 1, alignItems: "center" }}>
      <Animated.View
        style={{
          width,
          height: 100,
          backgroundColor: "violet",
        }}
      />
      <Button onPress={handlePress} title="Click me" />
    </View>
  );
}
```

## 2、Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~4.0.0                              |  No              |  0.82     |
| ~3.18.1                               |  No              |  0.77     |
| ~3.6.5                              |  Yes             |  0.72     |
| <= 3.6.4@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。

> [!TIP] version >= 4.0.0。
该版本 HarmonyOS 侧实现依赖 `@react-native-ohos/react-native-worklets` 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。
如未引入请参照 [@react-native-ohos/react-native-worklets文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-worklets.md)进行引入。

<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 2.1. Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony",
    // version >= 4.0.0
    "@react-native-ohos/react-native-worklets": "file:../node_modules/@react-native-ohos/react-native-worklets/harmony/worklets.har"
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
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-ohos/react-native-reanimated": "file:../../node_modules/@react-native-ohos/react-native-reanimated/harmony/reanimated.har",
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 2.3. 配置 CMakeLists 和引入 ReanimatedPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

# version >= 4.0.0 若开启对应SVG的Feature flags，需配置如下：
+ add_compile_definitions(REANIMATED_FEATURE_FLAGS='[EXPERIMENTAL_CSS_ANIMATIONS_FOR_SVG_COMPONENTS:true]')

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-reanimated/src/main/cpp" ./reanimated)

# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_reanimated)

# RNOH_BEGIN: manual_package_linking_2
```
> [!Tip] 注意：上面NODE_MODULES定义，为源库的安装路径，用户可以根据安装源库的路径定义NODE_MODULES

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ReanimatedPackage.h"
using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ReanimatedPackage>(ctx)
    };
}
```

### 2.4. 在 ArkTs 侧引入 ReanimatedPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { ReanimatedPackage} from '@react-native-ohos/react-native-reanimated/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ReanimatedPackage(ctx),
  ];
}
```

</details>

### 2.5. 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1.兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
4. RNOH: 0.82.7;  SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1.260; ROM: 6.0.0.130 SP15;

### 3.2.权限要求 (如需使用传感器需要添加对应的传感器权限)

> [!Tip] 使用传感器的功能，需要使用>=4.0.0的版本,该功能只在RN 82版本上生效

在 `entry` 目录下的 `module.json5` 中添加权限
```
"requestPermissions": [
+  {
+    "name": "ohos.permission.ACCELEROMETER",  // 加速传感器权限名称
+    "reason": "$string:accele_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"inuse"
+    }
+  },
+  {
+    "name": "ohos.permission.GYROSCOPE", // 陀螺仪传感器权限名称
+    "reason": "$string:gyr_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"inuse"
+    }
+  },
]

```
在 entry 目录下添加申请以上权限的原因
打开 `entry/src/main/resources/base/element/string.json`，添加：
```
{
  "string": [
+    {
+      "name": "accele_reason",
+      "value": "使用加速度传感器"
+    },
+    {
+      "name": "gyr_reason",
+      "value": "使用陀螺仪传感器"
+    },
  ]
}
```

## 4. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                                                                                                                                                                                                                | Type     | Required | Platform | HarmonyOS Support |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |----------| -------- | -------- | ----------------- |
| `withTiming`       | withTiming lets you create an animation based on duration and easing..                                                                                                                                                     | function | No       | All      | yes               |
| `withSpring`       | withSpring lets you create spring-based animations.                                                                                                                                                                        | function | No       | All      | yes               |
| `withDecay`        | withDecay lets you create animations that mimic objects in motion with friction. The animation will start with the provided velocity and slow down over time according to the given deceleration rate until it stops.      | function | No       | All      | yes               |
| `withRepeat`       | withRepeat is an animation modifier that lets you repeat an animation given number of times or run it indefinitely.                                                                                                        | function | No       | All      | yes               |
| `useSharedValue`   | useSharedValue lets you define shared values in your components.                                                                                                                                                           | function | No       | All      | yes               |
| `useAnimatedStyle` | useAnimatedStyle lets you create a styles object, similar to StyleSheet styles, which can be animated using shared values.                                                                                                 | function | No       | All      | yes               |
| `useAnimatedRef`   | useAnimatedRef lets you get a reference of a view. Used alongside measure, scrollTo, and useScrollViewOffset functions.                                                                                                    | function | No       | All      | yes               |
| `useDerivedValue`  | useDerivedValue lets you create new shared values based on existing ones while keeping them reactive.                                                                                                                      | function | No       | All      | yes               |
| `cancelAnimation`  | cancelAnimation lets you cancel a running animation paired to a shared value.                                                                                                                                              | function | No       | All      | yes               |
| `runOnJS`<sup>deprecated from 4.0.0</sup>           | runOnJS lets you asynchronously run non-workletized functions that could not otherwise run on the UI thread. This applies to most external libraries as they do not have their functions marked with "worklet"; directive. | function | No       | All      | yes               |
| `runOnUI`<sup>deprecated from 4.0.0</sup>            | runOnUI lets you asynchronously run workletized functions on the UI thread.                                                                                                                                                | function | No       | All      | yes               |
| `measure`          | measure lets you synchronously get the dimensions and position of a view on the screen, all on the UI thread.                                                                                                              | function | No       | All      | yes               |
| `Easing`           | easing set motion trajectory                                                                                                                                                                                               | function | No       | All      | yes               |
| `useAnimatedKeyboard`           | useAnimatedKeyboard lets you create animations based on state and height of the virtual keyboard.                                                                                                             | function | No       | All      | yes               |
| `useComposedEventHandler`<sup>3.18.0+</sup> | This is a hook that lets you compose useEvent-based event handlers (such as useAnimatedScrollHandler or your own custom ones) into a single, combined event handler. | function | No       | All      | yes               |
| `makeMutable`<sup>3.18.0+</sup> | makeMutable is a function internally used by the useSharedValue hook to create a shared value | function | No       | All      | yes               |
| `ReducedMotionConfig`<sup>3.18.0+</sup> | change behavior in response to the device's reduced motion accessibility setting. | function | No       | All      | yes               |
| `useAnimatedGestureHandler`<sup>deprecated from 3.18.0</sup> | lets you create animations based on gesture handlers. | function | No | All | No |
| `useScrollViewOffset` <sup> deprecated from 4.0.0 </sup> | lets you to create animations based on the offset of a ScrollView.<br /><br />3.6.0:useScrollViewOffset(aref: RefObject<Animated.ScrollView>) => [SharedValue\<number\>];<br />3.18.0:useScrollViewOffset(animatedRef: AnimatedRef\<AnimatedScrollView\>, providedOffset?: SharedValue\<number\>): SharedValue\<number\>; | function | No | All | yes |
| `useScrollOffset` <sup> 4.0.0+ </sup> | lets you to create animations based on the offset of a scrollable component (e.g. ScrollView, FlatList, FlashList) | function | No | All | yes |
| `createAnimatedComponent ` |  lets you create an Animated version of any React Native component | function | No | All | yes |
| `getStaticFeatureFlag` <sup> 4.0.0+ </sup> | A function for obtaining static functionality flags (feature flags) | function | No | All | yes |
| `setDynamicFeatureFlag` <sup> 4.0.0+ </sup> | A function for dynamically setting function flags | function | No | All | yes |
| `reanimatedVersion` <sup> 4.0.0+ </sup> | Obtain the version number of the animation library | function | No | All | yes |
| `useAnimatedProps` | It is a custom Hook in the React Native Reanimated library, used to create animatable component properties | function | No | All | yes |

## 5. 属性

**WithSpringConfig**

| Name                    | Description                                                  | Type             | Required | Platform        | HarmonyOS  Support |
| ----------------------- | ------------------------------------------------------------ | ---------------- | -------- | --------------- | ------------------ |
| clamp<sup>3.18.0+</sup> | Limit of the scope of movement. If your spring would exceed this limit, then `dampingRatio` will be reduced (to make the spring less bouncy) | [number, number] | No       | Android and iOS | yes                |

**SharedValue**

| Name                  | Description                                                  | Type     | Required | Platform        | HarmonyOS  Support |
| --------------------- | ------------------------------------------------------------ | -------- | -------- | --------------- | ------------------ |
| get<sup>3.18.0+</sup> | Returns current value                                        | function | No       | Android and iOS | yes                |
| set<sup>3.18.0+</sup> | Updates stored value (supports direct value or updater function) | function | No       | Android and iOS | yes                |
| addListener           | Registers value change listener<br /><br />3.6.0:addListener:(listenerID: number, listener: (value: any) => void) => void;<br />3.18.0:addListener:(listenerID: number, listener: (value: Value) => void) => void; | function | No       | Android and iOS | yes                |
| modify                | Applies transformation to current value<br /><br />3.6.0:modify:(modifier?: (value: any) => any, forceUpdate?: boolean) => void;<br />3.18.0:modify:(modifier?: \<T extends Value\>(value: T) => T, forceUpdate?: boolean) => void; | Object   | No       | Android and iOS | yes                |

**DerivedValue**

| Name                                 | Description                 | Type     | Required | Platform        | HarmonyOS  Support |
| ------------------------------------ | --------------------------- | -------- | -------- | --------------- | ------------------ |
| set<sup>deprecated from 3.18.0</sup> | Derived values are readonly | function | No       | Android and iOS | No                 |

**CurrentLayoutAnimationsValues**

| Name                                  | Description           | Type   | Required | Platform        | HarmonyOS  Support |
| ------------------------------------- | --------------------- | ------ | -------- | --------------- | ------------------ |
| currentBorderRadius<sup>3.18.0+</sup> | Border radius of view | number | No       | Android and iOS | No                 |

**EntryAnimationsValues**

| Name                                 | Description           | Type   | Required | Platform        | HarmonyOS  Support |
| ------------------------------------ | --------------------- | ------ | -------- | --------------- | ------------------ |
| targetBorderRadius<sup>3.18.0+</sup> | Border radius of view | number | No       | Android and iOS | No                 |

**itemLayoutAnimation**

| Name                                  | Description                               | Type            | Required | Platform        | HarmonyOS  Support |
| ------------------------------------- | ----------------------------------------- | --------------- | -------- | --------------- | ------------------ |
| itemLayoutAnimation<sup>3.18.0+</sup> | Defines layout transitions for list items | LayoutAnimation | No       | Android and iOS | yes                |


**CSS Transitions** <sup>4.0.0+</sup>
| Name                                  | Description                               | Type            | Required | Platform        | HarmonyOS  Support |
| ------------------------------------- | ----------------------------------------- | --------------- | -------- | --------------- | ------------------ |
| transitionProperty | lets you specify the name or names of styles properties to transition. | object  | No       | Android and iOS | yes       |
| transitionDuration | lets you specify the length of time the transition lasts. |  object |No | Android and iOS | yes       |
| transitionDelay | lets you specify the length of time to wait before transition starts. | object | No       | Android and iOS | yes       |
| transitionTimingFunction |  lets you adjust how intermediate values are calculated during the transition. | object | No | Android and iOS | yes  |
| transitionBehavior |  lets you determine whether the transition is applied to discrete properties. | object | No | Android and iOS | yes  |


**CSS Animations** <sup>4.0.0+</sup>
| Name                                  | Description                               | Type            | Required | Platform        | HarmonyOS  Support |
| ------------------------------------- | ----------------------------------------- | --------------- | -------- | --------------- | ------------------ |
| animationName  |  lets you specify keyframes for the animation. | object  | No       | Android and iOS | yes       |
| animationDuration | lets you specify the length of time the transition lasts. | object  |No    | Android and iOS | yes       |
| animationDelay | lets you specify the length of time to wait before animation starts. | object | No       | Android and iOS | yes       |
| animationTimingFunction |  lets you adjust how intermediate values are calculated during the transition. | object | No | Android and iOS | yes  |
| animationDirection  |  lets you specify which direction the animation should run. | object | No | Android and iOS | yes  |
| animationIterationCount  |  lets you repeat an animation given number of times or run it indefinitely. | object | No | Android and iOS | yes  |
| animationFillMode   |  lets you specify how the computed styles will be persisted before the animation runs and after it finishes. | object | No | Android and iOS | yes  |
| animationPlayState   |  lets you play and pause the animation. | object | No | Android and iOS | yes  |

**Common object**
| Name                                  | Description                               | Type            | Required | Platform        | HarmonyOS  Support |
| ------- | --------------------- | --------------- | -------- | --------------- | ------------------ |
| `GentleSpringConfig ` <sup>4.0.0+</sup> |  It is a predefined spring animation configuration, which creates a smooth and gentle spring effect. | Object | No | All | yes |
| `GentleSpringConfigWithDuration ` <sup>4.0.0+</sup> |  It is another form of GentleSpringConfig. It uses the parameters of duration and dampingRatio to define the spring animation. | Object | No | All | yes |
| `Reanimated3DefaultSpringConfig ` <sup>4.0.0+</sup> |  It will generate an animation that is highly elastic and has obvious oscillations. | Object | No | All | yes |
| `Reanimated3DefaultSpringConfigWithDuration ` <sup>4.0.0+</sup> | A flexible animation will be generated. | Object | No | All | yes |
| `SnappySpringConfig ` <sup>4.0.0+</sup> | The configuration defines the "Snappy" (agile) spring animation. | Object | No | All | yes |
| `SnappySpringConfigWithDuration ` <sup>4.0.0+</sup> | The configuration defines the "Snappy" (quick) spring animation. | Object | No | All | yes |
| `WigglySpringConfig ` <sup>4.0.0+</sup> | The configuration defines the "Wiggly" (swinging) spring animation, which will produce a distinct swinging/bouncing effect. | Object | No | All | yes |
| `WigglySpringConfigWithDuration ` <sup>4.0.0+</sup> | The configuration defines the "Wiggly" (swaying) spring animation, which completes the animation within 550ms and will have a distinct oscillation effect (underdamping) | Object | No | All | yes |
| `EasingFunctionFactory`  | A type definition in the library, serving as a factory function for creating easing functions | object | No | All | yes |
| `EntryOrExitLayoutType` | A combined type used to define the type of entering or exiting animation | object | No | All | yes |
| `DynamicColorIOS` | designed to be used within Reanimated. It's a way to define colors that automatically adapt to light and dark mode on iOS | object | No |  iOS | no |

## 6. 遗留问题

## 7. 其他

## 8. 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/software-mansion/react-native-reanimated/blob/main/LICENSE) ，请自由地享受和参与开源。