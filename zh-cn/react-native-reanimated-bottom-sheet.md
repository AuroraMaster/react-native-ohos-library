> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>reanimated-bottom-sheet</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/osdnk/react-native-reanimated-bottom-sheet">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/osdnk/react-native-reanimated-bottom-sheet/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
         <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet)

该第三方库的仓库Github上，且支持直接从 npm 下载，新的包名为：@react-native-ohos/reanimated-bottom-sheet，具体版本所属关系如下：

| 三方库版本 | 包名                              | 仓库地址 | 发布(Release) | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |  ---------- |  ---------- |
| 1.0.0 | @react-native-oh-tpl/reanimated-bottom-sheet | [Github](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet)|[Github Releases](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/releases)|0.72       |
| 1.1.0 | @react-native-ohos/reanimated-bottom-sheet         | [Github](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/tree/br_rnoh0.77) |[Github Releases]() | 0.77       |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/reanimated-bottom-sheet

# 0.77
npm install @react-native-ohos/reanimated-bottom-sheet
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/reanimated-bottom-sheet

# 0.77
yarn add @react-native-ohos/reanimated-bottom-sheet
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import React from "react";
import { View, Button, Text,Dimensions } from "react-native";
import { GestureHandlerRootView } from 'react-native-gesture-handler';
import BottomSheet from "reanimated-bottom-sheet";


export default function () {
  const WINDOW_HEIGHT = Dimensions.get('window').height;
  const sheetRef = React.useRef(null);
  const renderContent = () => (
    <View
      style={{
        padding: 16,
      }}>
      <Text>this is content</Text>
    </View>
  );

  const renderHeader = () => (
    <View
      style={{
        padding: 16,
      }}>
      <Text>title</Text>
    </View>
  )

  return (
    <GestureHandlerRootView style={{ height:WINDOW_HEIGHT, }}>
      <View
        style={{
          height:WINDOW_HEIGHT,
          backgroundColor: 'papayawhip',
          alignItems: 'center',
          justifyContent: 'center',
        }}>
        <View style={{ flex: 1, gap: 10, justifyContent: 'center' }}>
          <Button
            title="sheetRef?.current.snapTo(2)"
            onPress={() => sheetRef?.current.snapTo(2)}
          />
          <Button
            title="sheetRef?.current.snapTo(1)"
            onPress={() => sheetRef?.current.snapTo(1)}
          />
          <Button
            title="sheetRef?.current.snapTo(0)"
            onPress={() => sheetRef?.current.snapTo(0)}
          />
        </View>
      </View>
      <BottomSheet
        ref={sheetRef}
        snapPoints={[200, 100, 0]}
        initialSnap={0}
        renderHeader={renderHeader}
        renderContent={renderContent} />
    </GestureHandlerRootView>
  )
}

```

## Link

本库依赖以下三方库，请查看对应文档：

RN 0.72
+ [@react-native-oh-tpl/react-native-gesture-handler](/zh-cn/react-native-gesture-handler.md)
+ [@react-native-oh-tpl/react-native-reanimated](/zh-cn/react-native-reanimated.md)
+ [@react-native-oh-tpl/bottom-sheet](/zh-cn/gorhom-bottom-sheet.md)

RN 0.77
+ [@react-native-ohos/react-native-gesture-handler](/zh-cn/react-native-gesture-handler.md)
+ [@react-native-ohos/react-native-reanimated](/zh-cn/react-native-reanimated.md)
+ [@react-native-ohos/bottom-sheet](/zh-cn/gorhom-bottom-sheet.md)

本库 HarmonyOS 侧实现依赖上述的react-native-reanimated、react-native-gesture-handler的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[react-native-reanimated 文档](/zh-cn/react-native-reanimated.md)、[react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1、RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); IDE: DevEco Studio 5.1.1.830; ROM: 6.0.0.112 SP12;  
2、RNOH: 0.77.18; SDK: HarmonyOS-5.1.1.208(API19); IDE: DevEco Studio 5.1.1.830; ROM: 6.0.0.112 SP12;

## 属性

详情见[react-native-reanimated-bottom-sheet](https://github.com/osdnk/react-native-reanimated-bottom-sheet)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| snapPoints | E.g. [300, 200, 0]. Points for snapping of bottom sheet coomponent. They define distance from bottom of the screen. Might be number or percent (as string e.g. '20%') for points or percents of screen height from bottom. Note: Array values must be in descending order. | array<string\|number> | yes | all | yes 
| initialSnap | Determines initial snap point of bottom sheet. The value is the index from snapPoints. | number | no | all | yes
| renderContent | Method for rendering scrollable content of bottom sheet.| React.ReactNode | no | all | yes
| renderHeader | Method for rendering non-scrollable header of bottom sheet. | React.ReactNode | no | all | yes
|enabledGestureInteraction | Defines if bottom sheet could be scrollable by gesture. | boolean | no | all | yes
| enabledHeaderGestureInteraction | Defines if bottom sheet header could be scrollable by gesture.| boolean | no | all | yes
|enabledContentGestureInteraction|Defines if bottom sheet content could be scrollable by gesture.| boolean | no | all | yes
| enabledContentTapInteraction | Defines whether bottom sheet content could be tapped. Note: If you use Touchable* components inside your renderContent, you'll have to switch this to false to make handlers like onPress work. (See this comment.) | boolean | no | all | no
| enabledManualSnapping | If false blocks snapping using snapTo method. | boolean | no | no | no
| enabledBottomClamp | If true block movement is clamped from bottom to minimal snapPoint. | boolean | no | all | yes
| enabledBottomInitialAnimation | If true sheet will grows up from bottom to initial snapPoint.| boolean | no | all | yes
| enabledInnerScrolling | Defines whether it's possible to scroll inner content of bottom sheet. | boolean | no | all | yes
| callbackNode | reanimated node which holds position of bottom sheet, where 0 it the highest snap point and 1 is the lowest.  | number | no | all | yes
| contentPosition | reanimated node which holds position of bottom sheet's content (in dp) | reanimated node | no | all | yes
| headerPosition | reanimated node which holds position of bottom sheet's header (in dp) | reanimated node | no | all | no
| overdragResistanceFactor | `Defines how violently sheet has to stopped while overdragging. 0 means no overdrag |  number | no | all | yes
| springConfig | Overrides config for spring animation | object | no | all | yes
| innerGestureHandlerRefs | Refs for gesture handlers used for building bottom sheet. The array consists fo three refs. The first for PanGH used for inner content scrolling. The second for PanGH used for header. The third for TapGH used for stopping scrolling the content. |  array | no | all | no
| simultaneousHandlers | OAccepts a react ref object or an array of refs to handler components. | Array<React.RefObject<any>> | no | all | no
| onOpenStart |Accepts a function to be called when the bottom sheet starts to open.| function | no | all | yes
| onOpenEnd | Accepts a function to be called when the bottom sheet is almost fully openned. | function | no | all | yes
| onCloseStart | Accepts a function to be called when the bottom sheet starts to close. | function | no | all | yes
| onCloseEnd | Accepts a function to be called when the bottom sheet is almost closing. | function | no | all | yes
| callbackThreshold | Accepts a float value from 0 to 1 indicating the percentage (of the gesture movement) when the callbacks are gonna be called. | number | no | all | no
| borderRadius | Border radius of content wrapper (excluding header). | number | no | all | yes


## 遗留问题

- [ ] enabledContentTapInteraction 暂不支持。 [issues#2](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/issues/2)
- [ ] simultaneousHandlers 暂不支持。 [issues#3](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/issues/3)
- [ ] innerGestureHandlerRefs 暂不支持。 [issues#4](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/issues/4)
- [ ] callbackThreshold 暂不支持。[issues#6](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/issues/6)
- [ ] headerPosition 暂不支持。[issues#7](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/issues/7)

## 其他
- 本库基于[@gorhom/bottom-sheet](https://github.com/react-native-oh-library/react-native-bottom-sheet)实现，若想实现完全可配置选项的高性能交互式bottomSheet，建议优先使用[@gorhom/bottom-sheet](https://github.com/react-native-oh-library/react-native-bottom-sheet)。
- enabledManualSnapping原库未实现该属性。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/osdnk/react-native-reanimated-bottom-sheet/blob/master/LICENSE.md) ，请自由地享受和参与开源。
