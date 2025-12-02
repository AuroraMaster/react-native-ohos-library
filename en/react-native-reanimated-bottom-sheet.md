> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet)

The repository of this third-party library Github and supports direct download from npm. The new package name is: @react-native-ohos/reanimated-bottom-sheet. The specific version ownership relationship is as follows:

| Version      | Package Name      | Repository | Release | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |  ---------- |  ---------- |
| 1.0.0 | @react-native-oh-tpl/reanimated-bottom-sheet | [Github](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet)|[Github Releases](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/releases)|0.72       |
| 1.1.0 | @react-native-ohos/reanimated-bottom-sheet         | [Github](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/tree/br_rnoh0.77) |[Github Releases]() | 0.77       |

## Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```jsx
import React from "react";
import { View, Button, Text, Dimensions } from "react-native";
import { GestureHandlerRootView } from "react-native-gesture-handler";
import BottomSheet from "reanimated-bottom-sheet";

export default function () {
  const WINDOW_HEIGHT = Dimensions.get("window").height;
  const sheetRef = React.useRef(null);
  const renderContent = () => (
    <View
      style={{
        padding: 16,
      }}
    >
      <Text>this is content</Text>
    </View>
  );

  const renderHeader = () => (
    <View
      style={{
        padding: 16,
      }}
    >
      <Text>title</Text>
    </View>
  );

  return (
    <GestureHandlerRootView style={{ height: WINDOW_HEIGHT }}>
      <View
        style={{
          height: WINDOW_HEIGHT,
          backgroundColor: "papayawhip",
          alignItems: "center",
          justifyContent: "center",
        }}
      >
        <View style={{ flex: 1, gap: 10, justifyContent: "center" }}>
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
        renderContent={renderContent}
      />
    </GestureHandlerRootView>
  );
}
```

## Link

This repository depends on the following libraries, please refer to the corresponding documentation:

RN 0.72
- [@react-native-oh-tpl/react-native-gesture-handler](/en/react-native-gesture-handler.md)
- [@react-native-oh-tpl/react-native-reanimated](/en/react-native-reanimated.md)
- [@react-native-oh-tpl/bottom-sheet](/en/gorhom-bottom-sheet.md)

RN 0.77
- [@react-native-ohos/react-native-gesture-handler](/en/react-native-gesture-handler.md)
- [@react-native-ohos/react-native-reanimated](/en/react-native-reanimated.md)
- [@react-native-ohos/bottom-sheet](/en/gorhom-bottom-sheet.md)

The HarmonyOS implementation of this library depends on the native code from react-native-reanimated、react-native-gesture-handler. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [react-native-reanimated](/en/react-native-reanimated.md)、[react-native-gesture-handler](/en/react-native-gesture-handler.md) to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1、RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); IDE: DevEco Studio 5.1.1.830; ROM: 6.0.0.112 SP12;  
2、RNOH: 0.77.18; SDK: HarmonyOS-5.1.1.208(API19); IDE: DevEco Studio 5.1.1.830; ROM: 6.0.0.112 SP12; 

## Properties

For details, see [react-native-reanimated-bottom-sheet](https://github.com/osdnk/react-native-reanimated-bottom-sheet)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.。

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                             | Description                                                                                                                                                                                                                                                                | Type                        | Required | Platform | HarmonyOS Support |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------- | -------- | -------- | ----------------- |
| snapPoints                       | E.g. [300, 200, 0]. Points for snapping of bottom sheet coomponent. They define distance from bottom of the screen. Might be number or percent (as string e.g. '20%') for points or percents of screen height from bottom. Note: Array values must be in descending order. | array<string\|number>       | yes      | all      | yes               |
| initialSnap                      | Determines initial snap point of bottom sheet. The value is the index from snapPoints.                                                                                                                                                                                     | number                      | no       | all      | yes               |
| renderContent                    | Method for rendering scrollable content of bottom sheet.                                                                                                                                                                                                                   | React.ReactNode             | no       | all      | yes               |
| renderHeader                     | Method for rendering non-scrollable header of bottom sheet.                                                                                                                                                                                                                | React.ReactNode             | no       | all      | yes               |
| enabledGestureInteraction        | Defines if bottom sheet could be scrollable by gesture.                                                                                                                                                                                                                    | boolean                     | no       | all      | yes               |
| enabledHeaderGestureInteraction  | Defines if bottom sheet header could be scrollable by gesture.                                                                                                                                                                                                             | boolean                     | no       | all      | yes               |
| enabledContentGestureInteraction | Defines if bottom sheet content could be scrollable by gesture.                                                                                                                                                                                                            | boolean                     | no       | all      | yes               |
| enabledContentTapInteraction     | Defines whether bottom sheet content could be tapped. Note: If you use Touchable\* components inside your renderContent, you'll have to switch this to false to make handlers like onPress work. (See this comment.)                                                       | boolean                     | no       | all      | no                |
| enabledManualSnapping            | If false blocks snapping using snapTo method.                                                                                                                                                                                                                              | boolean                     | no       | no       | no                |
| enabledBottomClamp               | If true block movement is clamped from bottom to minimal snapPoint.                                                                                                                                                                                                        | boolean                     | no       | all      | yes               |
| enabledBottomInitialAnimation    | If true sheet will grows up from bottom to initial snapPoint.                                                                                                                                                                                                              | boolean                     | no       | all      | yes               |
| enabledInnerScrolling            | Defines whether it's possible to scroll inner content of bottom sheet.                                                                                                                                                                                                     | boolean                     | no       | all      | yes               |
| callbackNode                     | reanimated node which holds position of bottom sheet, where 0 it the highest snap point and 1 is the lowest.                                                                                                                                                               | number                     | no       | all      | yes               |
| contentPosition                  | reanimated node which holds position of bottom sheet's content (in dp)                                                                                                                                                                                                     | reanimated node             | no       | all      | yes               |
| headerPosition                   | reanimated node which holds position of bottom sheet's header (in dp)                                                                                                                                                                                                      | reanimated node             | no       | all      | no                |
| overdragResistanceFactor         | `Defines how violently sheet has to stopped while overdragging. 0 means no overdrag                                                                                                                                                                                        | number                      | no       | all      | yes               |
| springConfig                     | Overrides config for spring animation                                                                                                                                                                                                                                      | object                      | no       | all      | yes               |
| innerGestureHandlerRefs          | Refs for gesture handlers used for building bottom sheet. The array consists fo three refs. The first for PanGH used for inner content scrolling. The second for PanGH used for header. The third for TapGH used for stopping scrolling the content.                       | array                       | no       | all      | no                |
| simultaneousHandlers             | OAccepts a react ref object or an array of refs to handler components.                                                                                                                                                                                                     | Array<React.RefObject<any>> | no       | all      | no               |
| onOpenStart                      | Accepts a function to be called when the bottom sheet starts to open.                                                                                                                                                                                                      | function                    | no       | all      | yes                |
| onOpenEnd                        | Accepts a function to be called when the bottom sheet is almost fully openned.                                                                                                                                                                                             | function                    | no       | all      | yes               |
| onCloseStart                     | Accepts a function to be called when the bottom sheet starts to close.                                                                                                                                                                                                     | function                    | no       | all      | yes               |
| onCloseEnd                       | Accepts a function to be called when the bottom sheet is almost closing.                                                                                                                                                                                                   | function                    | no       | all      | yes               |
| callbackThreshold                | Accepts a float value from 0 to 1 indicating the percentage (of the gesture movement) when the callbacks are gonna be called.                                                                                                                                              | number                      | no       | all      | no                |
| borderRadius                     | Border radius of content wrapper (excluding header).                                                                                                                                                                                                                       | number                      | no       | all      | yes               |

## Known Issues

- [ ] enabledContentTapInteraction 暂不支持。 [issues#2](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/issues/2)
- [ ] simultaneousHandlers 暂不支持。 [issues#3](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/issues/3)
- [ ] innerGestureHandlerRefs 暂不支持。 [issues#4](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/issues/4)
- [ ] callbackThreshold 暂不支持。[issues#6](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/issues/6)
- [ ] headerPosition 暂不支持。[issues#7](https://github.com/react-native-oh-library/react-native-reanimated-bottom-sheet/issues/7)

## Others

- 本库基于[@gorhom/bottom-sheet](https://github.com/react-native-oh-library/react-native-bottom-sheet)实现，若想实现完全可配置选项的高性能交互式 bottomSheet，建议优先使用[@gorhom/bottom-sheet](https://github.com/react-native-oh-library/react-native-bottom-sheet)。
- enabledManualSnapping 原库未实现该属性。

## License

This project is licensed under [The MIT License (MIT)](https://github.com/osdnk/react-native-reanimated-bottom-sheet/blob/master/LICENSE.md).
