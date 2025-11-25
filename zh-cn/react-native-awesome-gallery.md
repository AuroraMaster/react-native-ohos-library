> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-awesome-gallery</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Flair-Dev/react-native-awesome-gallery">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/pavelbabenko/react-native-awesome-gallery/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/Flair-Dev/react-native-awesome-gallery)

请到三方库的 Releases 发布地址查看配套的版本信息：
| 三方库版本 | 支持RN版本 |
| ---------- | ---------- |
| 0.4.2      | 0.72/0.77  |

## 安装与使用

进入到工程目录并输入以下命令

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-awesome-gallery@0.4.2
```

#### **yarn**

```bash
yarn add react-native-awesome-gallery@0.4.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```ts
import React from 'react';
import {View, SafeAreaView} from 'react-native';
import Gallery from 'react-native-awesome-gallery';

const getRandomSize = function () {
  const min = 400;
  const max = 800;
  return Math.floor(Math.random() * (max - min + 1)) + min;
};

const images = new Array(10)
  .fill(0)
  .map(() => `https://picsum.photos/${getRandomSize()}/${getRandomSize()}`);

export default function App() {
  return (
    <View style={{flex: 1}}>
      <SafeAreaView></SafeAreaView>
      <View style={{height: '100%', width: '100%'}}>
        <Gallery data={images} swipeEnabled={true} />
      </View>
    </View>
  );
}
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-gesture-handler、@react-native-oh-tpl/react-native-reanimated 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)、[@react-native-oh-tpl/react-native-reanimated 文档](/zh-cn/react-native-reanimated.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.28; SDK: HarmonyOS-NEXT-DB5 5.0.0.60; IDE: DevEco Studio  5.0.3.655; ROM: 3.0.0.36;

2. RNOH: 0.72.29; SDK: HarmonyOS-NEXT-DB6 5.0.0.61; IDE: DevEco Studio  5.0.3.706; ROM: 5.0.0.60;

3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

   

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name              | Description                     | Type           | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------- | -------------- | -------- | ----------- | ----------------- |
| data        | 要渲染的条目数组       | T[] | Yes       | iOS/Android | Yes               |
| renderItem       | 用于渲染自定义图片组件（如 FastImage）的回调函数。注意：图片加载完成后必须调用 setImageDimensions({width, height}) 参数         | (renderItemInfo: {item: T, index: number, setImageDimensions: Function}) => React.ReactElement | No       | iOS/Android | Yes               |
| keyExtractor | 为条目提供唯一 key 的回调函数  | (item: T, index: number) => string or number | No       | iOS/Android | Yes               |
| initialIndex     | 初始显示的图片索引 | number        | No       | iOS/Android | Yes               |               |
| numToRender     | 画廊中同时渲染的条目数量 | number        | No       | iOS/Android | Yes               |
| emptySpaceWidth     | 条目之间的留白宽度 | number        | No       | iOS/Android | Yes               |
| doubleTapScale     | 双击时应用的图片缩放比例 | number        | No       | iOS/Android | No               |
| doubleTapInterval     | 单击与双击之间的毫秒间隔 | number        | No       | iOS/Android | No               |
| maxScale     | 用户通过手势可设置的最大缩放值 | number        | No       | iOS/Android | Yes               |
| pinchEnabled     | 是否启用捏合手势 | boolean        | No       | iOS/Android | Yes               |
| swipeEnabled     | 是否启用平移手势 | boolean        | No       | iOS/Android | Yes               |
| doubleTapEnabled     | 是否启用双击 | boolean        | No       | iOS/Android | No               |
| disableTransitionOnScaledImage     | 当缩放比例大于 1 时禁用前后图片的切换 | boolean        | No       | iOS/Android | Yes               |
| hideAdjacentImagesOnScaledImage     | 当缩放比例大于 1 时隐藏前后相邻图片 | boolean        | No       | iOS/Android | Yes               |
| disableVerticalSwipe     | 当缩放比例等于 1 时禁用垂直滑动 | boolean        | No       | iOS/Android | Yes               |
| disableSwipeUp     | 当缩放比例等于 1 时禁用上滑手势 | boolean        | No       | iOS/Android | Yes               |
| loop     | 允许用户循环滑动，data.length 大于 1 时生效 | boolean        | No       | iOS/Android | Yes               |
| onScaleChange     | 当缩放值变化时触发 | (scale: number) => void        | No       | iOS/Android | Yes               |
| onScaleChangeRange     | 指定触发 onScaleChange 的缩放区间 | {start: number, end: number}        | No       | iOS/Android | Yes               |
| containerDimensions     | 包裹画廊的容器 View 尺寸对象 | {width: number, height: number}        | No       | iOS/Android | Yes               |
| style     | 是否启用双击 | Style of container        | No       | iOS/Android | Yes               |

## 事件

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                                        | Type             | Required | Platform    | HarmonyOS Support |
| ------------------ | -------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| onSwipeToClose()         | 当用户向上/向下滑动至顶部或底部时触发                                  | function         | No       | iOS/Android | Yes               |
| onTranslationYChange(translationY: number, shouldClose: boolean) | "worklet"; 当用户垂直滑动以关闭画廊时触发                         | function         | No       | iOS/Android | No               |
| onTap()          | 当用户点击图片时触发                                | function | No       | iOS/Android | Yes               |
| onIndexChange     | 当当前激活项的索引变化时触发 | function        | No       | iOS/Android | Yes
| onDoubleTap(toScale: number)        | 当用户双击图片时触发                                 | function         | No       | iOS/Android | No               |
| onLongPress()              | 检测到长按时触发                                         | function           | No       | iOS/Android | Yes               |
| onScaleStart(scale: number)         | 捏合手势开始时触发                             | function            | No       | iOS/Android | Yes               |
| onScaleEnd(scale: number) | 捏合手势结束时触发，可用于在缩放 > maxScale 或 < 1 时添加触感反馈                    | function            | No       | iOS/Android | Yes               |
| onPanStart()           | 平移手势开始时触发                                    | function            | No       | iOS/Android | Yes               |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                                        | Type             | Required | Platform    | HarmonyOS Support |
| ------------------ | -------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| setIndex        | 设置当前激活的索引                                  | (newIndex: number, animated?: boolean) => void         | No       | iOS/Android | Yes               |
| reset | 重置缩放与位移                         | (animated?: boolean) => void         | No       | iOS/Android | Yes               |

## 遗留问题
- [ ] onTranslationYChange事件设置后，拖动图片会发生异常，iOS 和 Android平台均有该问题: [issue#84](https://github.com/pavelbabenko/react-native-awesome-gallery/issues/84)
- [x] react-native-gesture-handler库Gesture.Tap()事件无法获取正确的当前坐标和手指数，导致doubleTapScale、doubleTapInterval、doubleTapEnabled、onDoubleTap不生效: [issue#21](https://github.com/react-native-oh-library/react-native-harmony-gesture-handler/issues/21)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/pavelbabenko/react-native-awesome-gallery/blob/main/LICENSE) ，请自由地享受和参与开源。