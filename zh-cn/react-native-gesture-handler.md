> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-gesture-handler</code> </h1>
</p>

本项目基于 [react-native-gesture-handler](https://github.com/software-mansion/react-native-gesture-handler) 开发。

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-gesture-handler`，具体版本所属关系如下：

| Version                        | Package Name                                  | Repository                                                   | Release                                                      |Support RN version    |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------               |
| <= 2.14.17@deprecated | @react-native-oh-tpl/react-native-gesture-handler | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-gesture-handler) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-gesture-handler/releases) |0.72|
| 2.14.18                       | @react-native-ohos/react-native-gesture-handler       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-gesture-handler) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-gesture-handler/releases) |0.72|
|  2.23.2                         | @react-native-ohos/react-native-gesture-handler       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-gesture-handler) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-gesture-handler/releases) |0.77|

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-ohos/react-native-gesture-handler Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-gesture-handler/releases)。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-gesture-handler
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-gesture-handler
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from "react";
import { Animated, Dimensions } from "react-native";
import {
  GestureHandlerRootView,
  PanGestureHandler,
} from "react-native-gesture-handler";

const { width } = Dimensions.get("screen");
const circleRadius = 30;

class Circle extends Component {
  _touchX = new Animated.Value(width / 2 - circleRadius);

  _onPanGestureEvent = Animated.event([{ nativeEvent: { x: this._touchX } }], {
    useNativeDriver: true,
  });

  render() {
    return (
      <GestureHandlerRootView>
        <PanGestureHandler onGestureEvent={this._onPanGestureEvent}>
          <Animated.View
            style={{
              height: 150,
              justifyContent: "center",
            }}
          >
            <Animated.View
              style={[
                {
                  backgroundColor: "#42a5f5",
                  borderRadius: circleRadius,
                  height: circleRadius * 2,
                  width: circleRadius * 2,
                },
                {
                  transform: [
                    {
                      translateX: Animated.add(
                        this._touchX,
                        new Animated.Value(-circleRadius)
                      ),
                    },
                  ],
                },
              ]}
            />
          </Animated.View>
        </PanGestureHandler>
      </GestureHandlerRootView>
    );
  }
}

export default function App() {
  return <Circle />;
}
```

## 使用Codegen

Version > @react-native-ohos/react-native-gesture-handler@2.14.18，已适配codegen-lib生成桥接代码。

本库未带rc.x的版本号是已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-gesture-handler@2.14.18，已支持 Autolink，无需手动配置，目前只支持72框架。
Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

Version <= @react-native-oh-tpl/react-native-gesture-handler@2.14.17@deprecated 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

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

> [!TIP] 引入原生代码之前请确认IDE版本，5.0.3.810及其之后的版本需要在harmony工程中的hvigor-config.json5文件中新增如下配置以解决路径过长导致的编译报错问题

```json
"properties":{
  "ohos.nativeResolver":false
}
```
目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-ohos/react-native-gesture-handler": "file:../../node_modules/@react-native-ohos/react-native-gesture-handler/harmony/gesture_handler.har"
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

### 3.配置 CMakeLists 和引入 GestureHandlerPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-gesture-handler/src/main/cpp" ./gesture-handler)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_gesture_handler)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
+ #include "generated/RNOHGeneratedPackage.h"
+ #include "GestureHandlerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+     std::make_shared<RNOHGeneratedPackage>(ctx),
+     std::make_shared<GestureHandlerPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 Gesture Handler Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
+ import GestureHandlerPackage from '@react-native-ohos/react-native-gesture-handler';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new GestureHandlerPackage(ctx),
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

本文档内容基于以下版本验证通过：

1. RNOH：0.72.33; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

## Gestures

### Gesture detector

GestureDetector 是 Gesture Handler 库 2.x 版本的一个主要组件。

#### Gesture detector 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description                                                                                  | Type                             | Required | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- | -------- |
| gesture    | 一个包含配置与回调的手势对象。                                     | base gestures or any ComposedGesture | yes      | All      | yes      |

#### Gesture 的方法
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| method | Description                                                                                  | Type                             | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- |
| Gesture.Tap() | 使用默认配置且无回调创建一个 [TapGesture](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/tap-gesture) 实例。 | function() | All      | yes    |
| Gesture.Pan() | 使用默认配置且无回调创建一个 [PanGesture](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/pan-gesture) 实例。 | function() | All      | yes    |
| Gesture.Rotation() | 使用默认配置且无回调创建一个 [`RotationGesture`](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/rotation-gesture) 实例。 | function() | All      | yes    |
| Gesture.LongPress() | 使用默认配置且无回调创建一个 [`LongPressGesture`](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/long-press-gesture) 实例。 | function() | All      | yes    |
| Gesture.Manual() | 使用默认配置且无回调创建一个 [`ManualGesture`](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/manual-gesture) 实例。 | function() | All      | yes    |
| Gesture.Pinch() | 使用默认配置且无回调创建一个 [`PinchGesture`](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/pinch-gesture) 实例。 | function() | All      | yes    |
| Gesture.Fling() | 使用默认配置且无回调创建一个 [`FlingGesture`](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/fling-gesture) 实例。 | function() | All      | yes    |

## Components

### Touchables

Gesture Handler 库提供了一种基于原生按钮的 React Native touchable 组件的实现，它不依赖于 React Native 的 JS responder system。这些组件的实现遵循相同的 API，旨在替代 React Native 中的 touchable 组件,HarmonyOS 已全面支持。

- [Touchable Opacity](https://reactnative.dev/docs/touchableopacity)
- [Touchable Without Feedback](https://reactnative.dev/docs/touchablewithoutfeedback)
- [Touchable Highlight](https://reactnative.dev/docs/touchablehighlight)
- [Touchable Native Feedback](https://reactnative.dev/docs/touchablenativefeedback)

### Buttons

BaseButton 属性
| Name | Description                                                                                  | Type                             | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- |
| onActiveStateChange | 当按钮从非激活切换到激活或反向切换时触发。 | function | All   | yes   |
| onPress | 按钮被按下时触发。 | function | All   | yes   |
| onLongPress | 按钮按住至少 `delayLongPress` 毫秒后触发。 | function | All   | yes   |
| exclusive | 是否允许多个按钮同时被按下，默认值为 `true`。 | boolean | All   | yes   |
| delayLongPress | 触发 `onLongPress` 前的延迟（毫秒），默认 600。 | number | All   | yes   |

ReactButton 属性
| Name | Description                                                                                  | Type                             | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- |
| underlayColor | 按钮处于激活态时会被调暗的背景色。 | Color | All   | yes   |

### Drawer Layout

属性
| Name | Description                                                                                  | Type                             | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- |
| drawerType | 抽屉的展示类型。                                     | 'front'\|'back'\|'slide' | All | yes |
| edgewidth | 定义手势距离内容视图边缘多远时才会被激活。 | number | All   | yes   |
| hideStatusBar | 设为 `true` 时，抽屉被拉出或处于打开状态会通过 [StatusBar](https://reactnative.dev/docs/statusbar.html) API 隐藏系统状态栏。 | boolean | All   | yes   |
| statusbaranimation | 在 `hideStatusBar` 为 `true` 时，选择隐藏/显示状态栏使用的动画。 | 'fade'\|'slide'\|'none' | All   | no   |
| overlaycolor | 抽屉打开时覆盖在内容视图之上的半透明遮罩颜色。 | color | All   | yes   |
| rendernavigationview | 标准实现中已包含的必填参数，用于渲染导航视图。 | function | All   | yes   |
| ondrawerclose | 抽屉关闭时调用。 | function | All   | yes   |
| ondraweropen | 抽屉打开时调用。 | function | All   | yes   |
| ondrawerslide | 抽屉因触摸事件滑动打开时调用。 | function | All   | yes   |
| ondrawerstatechanged | 抽屉状态变化时调用。 | function | All   | yes   |
| children | 默认渲染并被抽屉包裹的子组件。 | component\| function | All   | yes   |

### Swipeable

属性
| Name | Description                                                                                  | Type                             | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- |
| friction | 视觉交互相对手势距离的延滞程度。 | number | All | yes |
| leftThreshold | 释放面板后，从左侧到达该距离就会动画到打开状态。 | number | All | yes |
| rightThreshold | 释放面板后，从右侧到达该距离就会动画到打开状态。 | number | All | yes |
| dragOffsetFromLeftEdge | 从左边缘开始拖动到被视为滑动所需的距离。 | number                   | All | yes |
| dragOffsetFromRightEdge | 从右边缘开始拖动到被视为滑动所需的距离。 | number | All | yes |
| overshootLeft | 是否允许可滑动面板被拉出超过左侧动作面板宽度。 | boolean | All | yes |
| overshootRight | 是否允许可滑动面板被拉出超过右侧动作面板宽度。 | boolean | All | yes |
| overshootFriction | 超出范围时视觉交互相对手势距离的延滞程度。 | number                   | All | yes |
| onSwipeableOpen | 动作面板打开时调用。 | function(direction: 'left' \| 'right', swipeable: Swipeable) | All | yes |
| onSwipeableClose | 动作面板关闭时调用。 | function(direction: 'left' \| 'right', swipeable: Swipeable) | All | yes |
| onSwipeableWillOpen | 动作面板开始动画打开（左/右）时调用。 | function((direction: 'left' \| 'right')) | All | yes |
| onSwipeableWillClose | 动作面板开始动画关闭时调用。 | function((direction: 'left' \| 'right')) | All | yes |
| renderLeftActions | 用于返回左侧动作面板的渲染方法，提供的插值输入区间可用于额外动画。 | function(progressAnimatedValue: AnimatedInterpolation,<br/>    dragAnimatedValue: AnimatedInterpolation,<br/>    swipeable: Swipeable) | All | yes |
| renderRightActions | 用于返回右侧动作面板的渲染方法（向左滑动时显露）。 | function(progressAnimatedValue: AnimatedInterpolation,<br/>    dragAnimatedValue: AnimatedInterpolation,<br/>    swipeable: Swipeable) | All | yes |
| containerStyle | 容器（Animated.View）的样式对象，例如覆盖 `overflow: 'hidden'`。 | StyleProp<ViewStyle> | All | yes |
| childrenContainerStyle | 子容器（Animated.View）的样式对象，例如应用 `flex: 1`。 | StyleProp<ViewStyle> | All | yes |


## Gesture handlers(legacy)

> [!WARNING] 建议使用新的 [gestures API](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/gesture)。旧的 API 已不再积极维护，也不会接收新功能。查看 [Introduction 中的 RNGH 2.0 章节](https://docs.swmansion.com/react-native-gesture-handler/docs/#rngh-20) 了解更多信息。

### Gesture handlers 通用属性
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| NAME                | Description                                                                                                                                   | TYPE                     | Required | Platform | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- | -------- | -------- | -------- |
| enabled                 | 指定该手势处理器是否应当分析触摸事件流。                                                            | boolean                      | no       | All      | yes      |
| hitSlop                 | 控制可用来开始识别手势的视图区域范围。                            | object                       | no       | All      | yes      |
| onGestureEvent          | 当处理器处于 ACTIVE 状态时，对后续触摸事件逐个触发的回调。                           | callback                     | no       | All      | yes      |
| onHandlerStateChange    | 当处理器状态变化时触发的回调。                                                           | callback                     | no       | All      | yes      |

### Gesture handlers 通用事件数据

以下是提供给 `onGestureEvent` 和 `onHandlerStateChange` 回调的通用事件数据:
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| NAME         | Description                                                             | TYPE | Platform | HarmonyOS Support |
| ---------------- | --------------------------------------------------------------------------- | ------ | -------- | -------- |
| state            | 处理器的当前状态。                                               | State  | All      | yes      |
| numberOfPointers | 当前放在屏幕上的指针（手指）数量。 | number | All      | yes      |

### PanGestureHandler

#### PanGestureHandler 属性
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| NAME                       | Description                                                                                                                                                                             | TYPE | Required | Platform | HarmonyOS Support |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | -------- | -------- |
| minDist                        | 手指（或多指）需要移动的最小距离，超过后处理器才会激活。                                                                                               | number  | no       | All      | yes      |
| minPointers                    | 处理器激活前需要放置的最少手指数量。                                                                                                              | number  | no       | All      | yes      |
| maxPointers                    | 当屏幕上放置到指定数量的手指且尚未激活时，将停止识别该手势。                                                             | number  | no       | All      | yes      |
| activeOffsetX                  | X 轴方向（点单位）内，不会触发处理器激活的移动区间。                                                                                                         | number  | no       | All      | yes      |
| activeOffsetY                  | Y 轴方向（点单位）内，不会触发处理器激活的移动区间。                                                                                                         | number  | no       | All      | yes      |

#### PanGestureHandler 事件数据

请到查看[基础 handler 类的通用事件数据](#gesture-handlers-通用事件数据)。以下是 PanGestureHandler 特有的事件数据。

`translationX`

手势过程中沿 X 轴累计的平移距离，单位为 point。

`translationY`

手势过程中沿 Y 轴累计的平移距离，单位为 point。

`velocityX`

当前沿 X 轴的平移速度，单位为 point/s。

`velocityY`

当前沿 Y 轴的平移速度，单位为 point/s。

`x`

指针（单指或多指的主指）相对于附加到处理器的视图的当前 X 坐标，单位为 point。

`y`

指针（单指或多指的主指）相对于附加到处理器的视图的当前 Y 坐标，单位为 point。

### TapGestureHandler

#### TapGestureHandler 属性
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| NAME      | Description                                                                                                                    | TYPE | Required | Platform | HarmonyOS Support |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | -------- |
| minPointers   | 处理器激活前需要放置的最少手指数量。                                           | number | no       | All      | yes      |
| maxDurationMs | 手指触摸后必须在多快时间内抬起的最大时长（毫秒）。                            | number | no       | All      | yes      |
| maxDelayMs    | 在需要多次点击时，两次点击之间允许经过的最大时间（毫秒）。                            | number | no       | All      | yes      |
| maxDeltaX     | 点击手势期间手指在 X 轴允许移动的最大距离（point）。 | number | no       | All      | yes      |
| maxDeltaY     | 点击手势期间手指在 Y 轴允许移动的最大距离（point）。 | number | no       | All      | yes      |
| maxDist       | 点击手势期间手指允许移动的最大距离（point）。                  | number | no       | All      | yes      |

#### TapGestureHandler 事件数据

请到查看[基础 handler 类的通用事件数据](#gesture-handlers-通用事件数据)。以下是 TapGestureHandler 特有的事件数据。

`x`

指针（单指或多指的主指）相对于附加到处理器的视图的当前 X 坐标，单位为 point。

`y`

指针（单指或多指的主指）相对于附加到处理器的视图的当前 Y 坐标，单位为 point。

`absoluteX`

指针（单指或多指的主指）相对于窗口的当前 X 坐标，单位为 point。若手势会导致视图变换，推荐使用 absoluteX 而不是 x。

`absoluteY`

指针（单指或多指的主指）相对于窗口的当前 Y 坐标，单位为 point。若手势会导致视图变换，推荐使用 absoluteY 而不是 y。

## 遗留问题

- [ ] statusbaranimation属性由于Arkts bar 只有淡出淡入动画和RN框架状态栏动画不支持，该功能暂不支持，问题: [issue#55](https://github.com/react-native-oh-library/react-native-harmony-gesture-handler/issues/55)

## 其他


## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-linear-gradient/blob/harmony/LICENSE) ，请自由地享受和参与开源。
