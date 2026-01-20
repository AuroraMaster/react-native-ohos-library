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

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为:`@react-native-ohos/bottom-sheet`，具体版本所属关系如下:

| Version                        | Package Name       | Repository          |  Release            |Supported RN Version  |
| ------------------------------ | ----------------   | ------------------- | ------------------- | -------------------- |
| 4.6.4  | @react-native-oh-tpl/bottom-sheet | [Github](https://github.com/react-native-oh-library/react-native-bottom-sheet) | [Github Releases](https://github.com/react-native-oh-library/react-native-bottom-sheet/releases) | 0.72 |
| 5.1.7 | @react-native-ohos/bottom-sheet   |[Github](https://github.com/react-native-oh-library/react-native-bottom-sheet) | [Github Releases](https://github.com/react-native-oh-library/react-native-bottom-sheet/releases) | 0.77 |

## 安装与使用

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

<!-- tabs:start -->

####  npm

```bash
# 0.72
npm install @react-native-oh-tpl/bottom-sheet

# 0.77
npm install @react-native-ohos/bottom-sheet
```

#### yarn

```bash
# 0.72
yarn add @react-native-oh-tpl/bottom-sheet

# 0.77
yarn add @react-native-ohos/bottom-sheet
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```jsx
// bottom-sheet组件
import React, { useCallback, useRef, useMemo } from "react";
import { StyleSheet, View, Text, Button } from "react-native";
import BottomSheet, { BottomSheetView } from "@gorhom/bottom-sheet";
import { GestureHandlerRootView } from 'react-native-gesture-handler';

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
    <GestureHandlerRootView style={styles.container}>
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
    </GestureHandlerRootView>
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
import { GestureHandlerRootView } from 'react-native-gesture-handler';

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
  <GestureHandlerRootView style={{ flex: 1 }}>
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
  </GestureHandlerRootView>
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

## Link

本库鸿蒙侧实现依赖react-native-reanimated和react-native-gesture-handler的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[react-native-reanimated 文档](/zh-cn/react-native-reanimated.md)、[react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)进行引入

## 约束与限制

### 兼容性

该库基于react-native-bottom-sheet进行适配，要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过:

1. RNOH: 0.72.29; SDK:HarmonyOS-Next-DB1 5.0.0.61; IDE:DevEco Studio 5.0.3.706; ROM:5.0.0.61;
2. RNOH: 0.72.96; SDK:HarmonyOS 5.1.1 Release SDK; IDE:DevEco Studio 5.1.1.840; ROM:6.0.0;
3. RNOH: 0.77.18; SDK:HarmonyOS 5.1.1 Release SDK; IDE:DevEco Studio 5.1.1.840; ROM:6.0.0;

## 属性

> [!Tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!Tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
### Bottom Sheet

#### Configuration
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| index    | 初始吸附索引。你也可以提供 -1 来使底部表单初始处于关闭状态。 | number | No       | Android / iOS | Yes           |
| snapPoints    | 底部表单吸附的点，点应从底部到顶部排序。接受数字、字符串或混合类型的数组。 | Array<number\|string>\|  SharedValue<Array<string \| number>> | Yes       | Android / iOS | Yes           |
| overDragResistanceFactor  |  定义在过度拖动时必须如何强制停止表单。  | number | No       | Android / iOS | Yes           |
| detached  |  定义底部表单YesNo附着在底部。  | boolean | No       | Android / iOS | Yes           |
| enableContentPanningGesture  |  启用内容拖动手势交互。  | boolean | No       | Android / iOS | Yes           |
| enableHandlePanningGesture  |  启用手柄拖动手势交互。  | boolean | No       | Android / iOS | Yes           |
| enableOverDrag  |  启用表单的过度拖动。  | boolean | No       | Android / iOS | Yes           |
| enablePanDownToClose  |  启用向下拖动手势以关闭表单。  | boolean | No       | Android / iOS | Yes           |
| enableDynamicSizing  |  为内容视图和可滚动内容尺寸启用动态调整大小。  | boolean | No       | Android / iOS | Yes           |
| animateOnMount  |  这将初始时以关闭状态挂载表单，当挂载并计算布局后，它将吸附到初始吸附点索引。  | boolean | No       | Android / iOS | Yes           |
| overrideReduceMotion<sup>5.1.7+</sup> | 覆盖用户的减少动画辅助功能设置。 | ReduceMotion.System \| ReduceMotion.Always \| ReduceMotion.Never | No | Android / iOS | Yes |
#### Styles
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| style  |  应用于表单容器的视图样式，也可以Yes AnimatedStyle。这有助于向表单添加阴影。  | ViewStyle \| AnimatedStyle | No       | Android / iOS | Yes           |
| backgroundStyle  |  应用于背景组件的视图样式。  | ViewStyle | No       | Android / iOS | Yes           |
| handleStyle  |  应用于手柄指示器组件的视图样式。  | ViewStyle | No       | Android / iOS | Yes           |
| handleIndicatorStyle  |  应用于手柄指示器组件的视图样式。  | ViewStyle | No       | Android / iOS | Yes           |
#### Layout Configuration
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| handleHeight  |  手柄高度有助于计算内部容器和表单布局。如果提供了 handleComponent，库将在内部计算其布局，除非也提供了 handleHeight。  | number | No       | Android / iOS | Yes           |
| containerHeight  |  容器高度有助于计算内部表单布局。如果未提供 containerHeight，库将在内部计算它，但这会导致额外的重新渲染。  | number | No       | Android / iOS | Yes           |
| containerOffset  |  容器偏移量有助于准确检测容器偏移量。  | Animated.SharedValue\<Insets> | No       | Android / iOS | Yes           |
| topInset  |  要添加到底部表单容器的顶部插入距离，通常来自 @react-navigation/stack 的钩子 useHeaderHeight 或来自 react-native-safe-area-context 的钩子 useSafeArea。  | number | No       | Android / iOS | Yes           |
| bottomInset  |  要添加到底部表单容器的底部插入距离。  | number | No       | Android / iOS | Yes           |
| maxDynamicContentSize  |  最大动态内容尺寸高度，用于限制底部表单高度不超过提供的尺寸。  | number | No       | Android / iOS | Yes           |
#### Keyboard Configuration
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| keyboardBehavior  | 定义键盘出现行为；`extend:` 将表单扩展到其最大吸附点；`fillParent:` 将表单扩展以填充父视图；`interactive: ` 根据键盘大小偏移表单。  | 'extend' \| 'fillParent' \| 'interactive' | No       | Android / iOS | Yes           |
| keyboardBlurBehavior  | 定义键盘失焦行为；none: 不执行任何操作；restore: 恢复表单位置  | 'none' \| 'restore' | No       | Android / iOS | Yes           |
| android_keyboardInputMode  | 仅定义 Android 的键盘输入模式。  | 'adjustPan' \| 'adjustResize' | No       | Android  | No           |
| enableBlurKeyboardOnGesture<sup>5.1.7+</sup> | 当用户开始拖动底部表单时启用模糊化键盘。 | boolean | No | Android / iOS | Yes |
#### Animation Configuration
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| animationConfigs  | 动画配置。  | function | No       | Android/iOS  | Yes           |
#### Gesture Configuration
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| waitFor  | -  | React.Ref \| React.Ref[] | No       | Android/iOS  | Yes           |
| simultaneousHandlers  | -  | React.Ref \| React.Ref[] | No       | Android/iOS  | Yes           |
| activeOffsetX  | -  | number[] | No       | Android/iOS  | Yes           |
| activeOffsetY  | -  | number[] | No       | Android/iOS  | Yes           |
| failOffsetX  | -  | number[] | No       | Android/iOS  | Yes           |
| failOffsetY  | -  | number[] | No       | Android/iOS  | Yes           |
| gestureEventsHandlersHook  | 用于提供拖动手势事件处理程序的自定义钩子，这将允许对拖动手势进行高级和自定义处理。  | GestureEventsHandlersHookType | No       | Android/iOS  | Yes           |

#### Animated Nodes
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| animatedIndex  | 用作内部索引节点回调的动画值。  | Animated.SharedValue\<number> | No       | Android/iOS  | Yes           |
| animatedPosition  | 用作内部位置节点回调的动画值。  | Animated.SharedValue\<number> | No       | Android/iOS  | Yes           |

#### Callbacks
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| onChange  | 当表单位置改变时的回调。  | function | No       | Android/iOS  | Yes           |
| onAnimate  | 当表单即将动画到新位置时的回调。  | function | No       | Android/iOS  | Yes           |

#### Components
| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| handleComponent  | 作为表单手柄放置的组件。  | React.FC\<BottomSheetHandleProps> | No       | Android/iOS  | Yes           |
| backdropComponent  | 作为表单背景幕放置的组件，默认设置为 null，但库也提供了背景幕的默认实现 BottomSheetBackdrop，不过你需要手动提供它。  | React.FC\<BottomSheetBackgroundProps> | No       | Android/iOS  | Yes           |
| backgroundComponent  | 作为表单背景放置的组件。  | React.FC\<BottomSheetBackgroundProps> | No       | Android/iOS  | Yes           |
| footerComponent  | 作为表单页脚放置的组件。  | React.FC\<BottomSheetFooterProps> | No       | Android/iOS  | Yes           |
| children  | 作为表单内容放置的可滚动节点或 React 节点。  | () => React.ReactNode \| React.ReactNode[] \| React.ReactNode | No       | Android/iOS  | Yes           |
### Bottom Sheet Modal
> [!提示]底部表单模态框继承了所有 [底部表单属性](https://ui.gorhom.dev/components/bottom-sheet/props)，除了 animateOnMount 和 containerHeight，并且它还引入了自己的属性

| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| name  | 模态框名称，用于后续识别模态框。  | string | No       | Android/iOS  | Yes           |
| stackBehavior  | 定义模态框挂载时的堆栈行为。  | 'push' \| 'replace' | No       | Android/iOS  | Yes           |
| enableDismissOnClose  | 在模态框关闭时将其解除，这将卸载模态框。  | boolean | No       | Android/iOS  | Yes           |
| onDismiss  | 当模态框被解除（卸载）时的回调。  | function | No       | Android/iOS  | Yes           |
| containerComponent  | 作为底部表单容器放置的组件，当使用来自 React Native Screens 的 FullWindowOverlay 时，这用于将底部表单放置在应用程序的最顶层。  | React.ReactNode | No       | Android/iOS  | Yes           |
## 遗留问题 
- [ ] BottomSheetFlatList组件手势滑动存在冲突 [issue#6](https://github.com/react-native-oh-library/react-native-bottom-sheet/issues/6) 
## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](hhttps://github.com/gorhom/react-native-bottom-sheet/blob/master/LICENSE) ，请自由地享受和参与开源。
