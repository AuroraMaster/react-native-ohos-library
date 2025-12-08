> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@th3rdwave/react-navigation-bottom-sheet</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/th3rdwave/react-navigation-bottom-sheet">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/th3rdwave/react-navigation-bottom-sheet/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/th3rdwave/react-navigation-bottom-sheet)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @th3rdwave/react-navigation-bottom-sheet@0.3.2
```

#### **yarn**

```bash
yarn add @th3rdwave/react-navigation-bottom-sheet@0.3.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!TIP] 本示例依赖 react-native-gesture-handler 库，参照[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)进行引入。

```js
import * as React from 'react';
import { StyleSheet, Dimensions, View, Button, Text } from 'react-native';
import { GestureHandlerRootView } from 'react-native-gesture-handler';
import {
  BottomSheetBackdrop,
  BottomSheetBackdropProps,
} from '@gorhom/bottom-sheet';
import { NavigationContainer } from '@react-navigation/native';
import {
  BottomSheetScreenProps,
  createBottomSheetNavigator,
} from '@th3rdwave/react-navigation-bottom-sheet';


type BottomSheetParams = {
  Home: undefined;
  Sheet: { id: number };
  BigSheet: { id: number };
};

const BottomSheet = createBottomSheetNavigator<BottomSheetParams>();

function HomeScreen({
  navigation,
}: BottomSheetScreenProps<BottomSheetParams, 'Home'>) {
  return (
    <View style={styles.container}>
      <Text style={{ color: 'black' }}>Home Screen</Text>
      <View style={styles.spacer} />
      <Button
        title="Open sheet"
        onPress={() => {
          navigation.navigate('Sheet', { id: 1 });
        }}
      />
      <View style={styles.spacer} />
      <Button
        title="Open a big sheet"
        onPress={() => {
          navigation.navigate('BigSheet', { id: 1 });
        }}
      />
    </View>
  );
}

function SheetScreen({
  route,
  navigation,
}: BottomSheetScreenProps<BottomSheetParams, 'Sheet'>) {
  let timer: any = null

  React.useEffect(() => {
    return () => {
      clearTimeout(timer)
    }
  })

  return (
    <View style={[styles.container, styles.content]}>
      <Text>Sheet Screen {route.params.id}</Text>
      <View style={styles.spacer} />
      <Button
        title="Open new sheet"
        onPress={() => {
          navigation.navigate('Sheet', { id: route.params.id + 1 });
        }}
      />
      <View style={styles.spacer} />
      <Button
        title="Open new big sheet"
        onPress={() => {
          navigation.navigate('BigSheet', { id: route.params.id + 1 });
        }}
      />
      <View style={styles.spacer} />
      <Button
        title="Close this sheet"
        onPress={() => {
          navigation.goBack();
        }}
      />
      <View style={styles.spacer} />
      {route.name === ('BigSheet' as unknown) && (
        <>
          <Button
            title="Snap to top"
            onPress={() => {
              timer = setTimeout(() => {
                navigation.snapTo(1);
              })
            }}
          />
        </>
      )}
    </View>
  );
}

const renderBackdrop = (props: BottomSheetBackdropProps) => (
  <BottomSheetBackdrop {...props} appearsOnIndex={0} disappearsOnIndex={-1} />
);

function SimpleExample() {
  return (
    <NavigationContainer>
      <BottomSheet.Navigator
        screenOptions={{
          backdropComponent: renderBackdrop,
        }}
      >
        <BottomSheet.Screen name="Home" component={HomeScreen} />
        <BottomSheet.Screen
          name="Sheet"
          component={SheetScreen}
          getId={({ params }) => `sheet-${params.id}`}
        />
        <BottomSheet.Screen
          name="BigSheet"
          component={SheetScreen}
          options={{
            snapPoints: ['70%', '90%'],
          }}
          getId={({ params }) => `sheet-${params.id}`}
        />
      </BottomSheet.Navigator>
    </NavigationContainer>
  );
}

export function BottomExample() {
  return (
    <GestureHandlerRootView style={styles.container1}>
        <SimpleExample />
    </GestureHandlerRootView>
  );
}

const styles = StyleSheet.create({
  container1: {
    flex: 1,
  },
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  content: {
    marginVertical: 20,
  },
  spacer: {
    margin: 5,
  },
  bottom: {
    display: 'flex',
    flexDirection: 'row'
  }
});

```
## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-gesture-handler、@react-native-oh-tpl/react-native-reanimated、@react-native-oh-tpl/bottom-sheet的原生端代码，如已在鸿蒙工程中引入过这三个库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)、[@react-native-oh-tpl/react-native-reanimated 文档](/zh-cn/react-native-reanimated.md)、[@react-native-oh-tpl/bottom-sheet 文档](/zh-cn/gorhom-bottom-sheet.md)进行引入

## 约束与限制

### 兼容性


本文档内容基于以下版本验证通过：

1. RNOH: 0.72.29; SDK: HarmonyOS-NEXT-DB6 5.0.0.61 (API Version 12 Beta6); IDE: DevEco Studio 5.0.3.706; ROM: 3.0.0.61;
## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


### Navigation options

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| snapPoints  | 底部弹窗可吸附的位置，从低到高排序，支持数字或字符串数组。    | Array<string>  | YES | ALL      | YES |
| backgroundStyle  | 应用于背景组件的样式。    | ViewStyle  | NO | ALL      | YES |
| index  | 初始吸附位置索引，设为 -1 可默认关闭。    | number  | NO | ALL      | YES |
| detached  | 是否附着在底部。  | boolean  | NO | ALL      | YES |
| overDragResistanceFactor  | 控制过度拖拽时阻尼力度。  | number  | NO |   ALL    | YES |
| enableOverDrag  | 是否允许过度拖拽。  | boolean  | NO |   ALL    | YES |
| enablePanDownToClose  | 允许下拉手势关闭。  | boolean  | NO |ALL| YES |
| enableHandlePanningGesture  | 允许拖拽手柄交互。  | boolean  | NO |ALL| YES |
| enableContentPanningGesture  | 允许拖拽内容区交互。 | boolean  | NO |ALL| YES |
| enableDynamicSizing  | 启用内容区和可滚动内容的动态尺寸。  | boolean  | NO | ALL      | YES |
| animateOnMount  | 初始以关闭状态挂载，布局计算后自动吸附到初始位置。  | boolean  | NO | ALL      | YES |
| style  | 应用于弹窗容器的样式，可为 AnimatedStyle，常用于添加阴影。  | ViewStyle  | NO | ALL      | YES |
| handleStyle  | 应用于手柄的样式。 | ViewStyle   | NO | ALL      | YES |
| handleIndicatorStyle  | 应用于手柄指示条的样式。 | ViewStyle  | NO | ALL      | YES |
| handleHeight  | 手柄高度用于计算内部容器与弹窗布局；若已提供 handleComponent，库会自动测量，除非同时指定 handleHeight。| number  | NO | ALL      | NO |
| contentHeight  | 内容高度用于动态吸附点计算。| number  | NO | ALL      | YES |
| topInset  | 添加到底部弹窗容器的顶部内边距，通常来自 useHeaderHeight 或 useSafeArea.| number  | NO | ALL      | YES |
| bottomInset  | 添加到底部弹窗容器的底部内边距。| number  | NO | ALL      | YES |
| maxDynamicContentSize  | 动态内容的最大高度，限制弹窗高度不超过该值。| number  | NO |    ALL     | YES |
| keyboardBehavior  | 键盘出现时的行为。| 'extend' or 'fillParent' or 'interactive'  | NO |NO| NO |
| keyboardBlurBehavior  | 键盘收起时的行为。| 'none' or 'restore'  | NO |    NO   | NO |
| animationConfigs  | 用于自定义 Timing 或 Spring 动画配置| object  | NO |   ALL    | YES |
| handleComponent  | 自定义手柄组件。|React.FC\<BottomSheetHandleProps>  | NO | ALL      | YES |
| backdropComponent  | 自定义背景遮罩组件，默认 null；库提供 BottomSheetBackdrop 需手动传入。|React.FC\<BottomSheetBackgroundProps>  | NO | ALL      | YES |
| backgroundComponent  | 自定义背景组件。|React.FC\<BottomSheetBackgroundProps> | NO | ALL      | YES |
| footerComponent  | 自定义底部栏组件。|React.FC\<BottomSheetFooterProps>  | NO | ALL      | YES |


### Navigation helpers

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| snapTo  | 将当前弹窗吸附到指定索引。    | (index: number) => void  | NO | ALL      | YES |


## 遗留问题

## 其他
- keyboardBehavior属性暂不支持，与iOS表现一致。[issue#24](https://github.com/th3rdwave/react-navigation-bottom-sheet/issues/24)
- keyboardBlurBehavior属性暂不支持，与iOS表现一致。[issue#25](https://github.com/th3rdwave/react-navigation-bottom-sheet/issues/25)
- handleHeight属性暂不支持，与iOS表现一致。[issue#30](https://github.com/th3rdwave/react-navigation-bottom-sheet/issues/30)

## 开源协议

本项目基于 [The MIT License (MIT )](https://github.com/th3rdwave/react-navigation-bottom-sheet/blob/main/LICENSE) ，请自由地享受和参与开源。