> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@gorhom/bottom-sheet</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/gorhom/react-native-bottom-sheet">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/gorhom/react-native-bottom-sheet/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-bottom-sheet)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/bottom-sheet Releases](https://github.com/react-native-oh-library/react-native-bottom-sheet/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/bottom-sheet
```

#### yarn

```bash
yarn add @react-native-oh-tpl/bottom-sheet
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```jsx
// bottom-sheet组件
import React, { useCallback, useRef, useMemo } from "react";
import { StyleSheet, View, Text, Button } from "react-native";
import BottomSheet, { BottomSheetView } from "@gorhom/bottom-sheet";

const App = () => {
  // hooks
  const sheetRef = useRef<BottomSheet>(null);

  // variables
  const snapPoints = useMemo(() => ["25%", "50%", "90%"], []);

  // callbacks
  const handleSheetChange = useCallback((index) => {
    console.log("handleSheetChange", index);
  }, []);
  const handleSnapPress = useCallback((index) => {
    sheetRef.current?.snapToIndex(index);
  }, []);
  const handleClosePress = useCallback(() => {
    sheetRef.current?.close();
  }, []);

  // render
  return (
    <View style={styles.container}>
      <Button title="Snap To 90%" onPress={() => handleSnapPress(2)} />
      <Button title="Snap To 50%" onPress={() => handleSnapPress(1)} />
      <Button title="Snap To 25%" onPress={() => handleSnapPress(0)} />
      <Button title="Close" onPress={() => handleClosePress()} />
      <BottomSheet
        ref={sheetRef}
        snapPoints={snapPoints}
        onChange={handleSheetChange}
      >
        <BottomSheetView>
          <Text>Awesome 🔥</Text>
        </BottomSheetView>
      </BottomSheet>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: 200,
  },
});

export default App;
```
```jsx
// bottom-sheet-modal组件
import React, { useCallback, useMemo, useRef } from 'react';
import { View, Text, StyleSheet, Button } from 'react-native';
import {
  BottomSheetModal,
  BottomSheetView,
  BottomSheetModalProvider,
} from '@gorhom/bottom-sheet';

const App = () => {
  // ref
  const bottomSheetModalRef = useRef<BottomSheetModal>(null);

  // variables
  const snapPoints = useMemo(() => ['25%', '50%'], []);

  // callbacks
  const handlePresentModalPress = useCallback(() => {
    bottomSheetModalRef.current?.present();
  }, []);
  const handleSheetChanges = useCallback((index: number) => {
    console.log('handleSheetChanges', index);
  }, []);

  // renders
  return (
    <BottomSheetModalProvider>
      <View style={styles.container}>
        <Button
          onPress={handlePresentModalPress}
          title="Present Modal"
          color="black"
        />
        <BottomSheetModal
          ref={bottomSheetModalRef}
          index={1}
          snapPoints={snapPoints}
          onChange={handleSheetChanges}
        >
          <BottomSheetView style={styles.contentContainer}>
            <Text>Awesome 🎉</Text>
          </BottomSheetView>
        </BottomSheetModal>
      </View>
    </BottomSheetModalProvider>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 24,
    justifyContent: 'center',
    backgroundColor: 'grey',
  },
  contentContainer: {
    flex: 1,
    alignItems: 'center',
  },
});

export default App;
```
## 使用codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-reanimated和@react-native-oh-tpl/react-native-gesture-handler的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-reanimated 文档](/zh-cn/react-native-reanimated.md)、[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1.RNOH: 0.72.29; SDK：HarmonyOS-Next-DB1 5.0.0.61; IDE：DevEco Studio 5.0.3.706; ROM：5.0.0.61;

## 属性

> [!Tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!Tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
### Bottom Sheet
#### Configuration
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| index    | Initial snap index. You also could provide -1 to initiate bottom sheet in closed state. | number | No       | Android / iOS | Yes           |
| snapPoints    | Points for the bottom sheet to snap to, points should be sorted from bottom to top. It accepts array of number, string or mix. | Array<number\|string>\|  SharedValue<Array<string \| number>> | Yes       | Android / iOS | Yes           |
| overDragResistanceFactor  |  Defines how violently sheet has to be stopped while over dragging.  | number | No       | Android / iOS | Yes           |
| detached  |  Defines whether the bottom sheet is attached to the bottom or no.  | boolean | No       | Android / iOS | Yes           |
| enableContentPanningGesture  |  Enable content panning gesture interaction.  | boolean | No       | Android / iOS | Yes           |
| enableHandlePanningGesture  |  Enable handle panning gesture interaction.  | boolean | No       | Android / iOS | Yes           |
| enableOverDrag  |  Enable over drag for the sheet.  | boolean | No       | Android / iOS | Yes           |
| enablePanDownToClose  |  Enable pan down gesture to close the sheet.  | boolean | No       | Android / iOS | Yes           |
| enableDynamicSizing  |  Enable dynamic sizing for content view and scrollable content size.  | boolean | No       | Android / iOS | Yes           |
| animateOnMount  |  This will initially mount the sheet closed and when it's mounted and calculated the layout, it will snap to initial snap point index.  | boolean | No       | Android / iOS | Yes           |
#### Styles
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| style  |  View style to be applied at the sheet container, it also could be an AnimatedStyle. This is helpful to add shadow to the sheet.  | ViewStyle \| AnimatedStyle | No       | Android / iOS | Yes           |
| backgroundStyle  |  View style to be applied to the background component.  | ViewStyle | No       | Android / iOS | Yes           |
| handleStyle  |  View style to be applied to the handle indicator component.  | ViewStyle | No       | Android / iOS | Yes           |
| handleIndicatorStyle  |  View style to be applied to the handle indicator component.  | ViewStyle | No       | Android / iOS | Yes           |
#### Layout Configuration
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| handleHeight  |  Handle height helps to calculate the internal container and sheet layouts. If handleComponent is provided, the library internally will calculate its layout, unless handleHeight is provided too.  | number | No       | Android / iOS | Yes           |
| containerHeight  |  Container height helps to calculate the internal sheet layouts. If containerHeight not provided, the library internally will calculate it, however this will cause an extra re-rendering.  | number | No       | Android / iOS | Yes           |
| contentHeight  |  Content height helps dynamic snap points calculation.  | number \| Animated.SharedValue\<number> | No       | Android / iOS | Yes           |
| containerOffset  |  Container offset helps to accurately detect container offsets.  | Animated.SharedValue\<Insets> | No       | Android / iOS | Yes           |
| topInset  |  Top inset to be added to the bottom sheet container, usually it comes from @react-navigation/stack hook useHeaderHeight or from react-native-safe-area-context hook useSafeArea.  | number | No       | Android / iOS | Yes           |
| bottomInset  |  Bottom inset to be added to the bottom sheet container.  | number | No       | Android / iOS | Yes           |
| maxDynamicContentSize  |  Max dynamic content size height to limit the bottom sheet height from exceeding a provided size.  | number | No       | Android / iOS | Yes           |
#### Keyboard Configuration
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| keyboardBehavior  | Defines the keyboard appearance behavior;`extend:` extend the sheet to its maximum snap point;`fillParent:` extend the sheet to fill the parent view;`interactive: `offset the sheet by the size of the keyboard.  | 'extend' \| 'fillParent' \| 'interactive' | No       | Android / iOS | Yes           |
| keyboardBlurBehavior  | Defines the keyboard blur behavior;none: do nothing;restore: restore sheet position  | 'none' \| 'restore' | No       | Android / iOS | Yes           |
| android_keyboardInputMode  | Defines keyboard input mode for Android only.  | 'adjustPan' \| 'adjustResize' | No       | Android  | No           |
#### Animation Configuration
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| animationConfigs  | Animation configs.  | function | No       | Android/iOS  | Yes           |
#### Gesture Configuration
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| waitFor  | -  | React.Ref \| React.Ref[] | No       | Android/iOS  | Yes           |
| simultaneousHandlers  | -  | React.Ref \| React.Ref[] | No       | Android/iOS  | Yes           |
| activeOffsetX  | -  | number[] | No       | Android/iOS  | Yes           |
| activeOffsetY  | -  | number[] | No       | Android/iOS  | Yes           |
| failOffsetX  | -  | number[] | No       | Android/iOS  | Yes           |
| failOffsetY  | -  | number[] | No       | Android/iOS  | Yes           |
| gestureEventsHandlersHook  | Custom hook to provide pan gesture events handler, which will allow advance and customize handling for pan gesture.  | GestureEventsHandlersHookType | No       | Android/iOS  | Yes           |

#### Animated Nodes
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| animatedIndex  | Animated value to be used as a callback for the index node internally.  | Animated.SharedValue\<number> | No       | Android/iOS  | Yes           |
| animatedPosition  | Animated value to be used as a callback for the position node internally.  | Animated.SharedValue\<number> | No       | Android/iOS  | Yes           |

#### Callbacks
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| onChange  | Callback when the sheet position changed.  | function | No       | Android/iOS  | Yes           |
| onAnimate  | Callback when the sheet about to animate to a new position.  | function | No       | Android/iOS  | Yes           |

#### Components
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| handleComponent  | Component to be placed as a sheet handle.  | React.FC\<BottomSheetHandleProps> | No       | Android/iOS  | Yes           |
| backdropComponent  | Component to be placed as a sheet backdrop, by default is set to null, however the library also provide a default implementation BottomSheetBackdrop of a backdrop but you will need to provide it manually.  | React.FC\<BottomSheetBackgroundProps> | No       | Android/iOS  | Yes           |
| backgroundComponent  | Component to be placed as a sheet background.  | React.FC\<BottomSheetBackgroundProps> | No       | Android/iOS  | Yes           |
| footerComponent  | Component to be placed as a sheet footer.  | React.FC\<BottomSheetFooterProps> | No       | Android/iOS  | Yes           |
| children  | Scrollable node or react node to be places as a sheet content.  | () => React.ReactNode \| React.ReactNode[] \| React.ReactNode | No       | Android/iOS  | Yes           |
### Bottom Sheet Modal
> [!Tip]Bottom Sheet Modal inherits all [Bottom Sheet props](https://ui.gorhom.dev/components/bottom-sheet/props) except for animateOnMount & containerHeight and also it introduces its own props

| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| name  | Modal name to help identify the modal for later on.  | string | No       | Android/iOS  | Yes           |
| stackBehavior  | Defines the stack behavior when modal mounts.  | 'push' \| 'replace' | No       | Android/iOS  | Yes           |
| enableDismissOnClose  | Dismiss the modal when it is closed, this will unmount the modal.  | boolean | No       | Android/iOS  | Yes           |
| onDismiss  | Callback when the modal dismissed (unmounted).  | function | No       | Android/iOS  | Yes           |
| containerComponent  | Component to be placed as a bottom sheet container, this is to place the bottom sheet at the very top layer of your application when using FullWindowOverlay from React Native Screens.  | React.ReactNode | No       | Android/iOS  | Yes           |
## 遗留问题 
- [ ] BottomSheetFlatList组件手势滑动存在冲突 [issue#6](https://github.com/react-native-oh-library/react-native-bottom-sheet/issues/6) 
## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](hhttps://github.com/gorhom/react-native-bottom-sheet/blob/master/LICENSE) ，请自由地享受和参与开源。
