> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-snap-carousel</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/meliorence/react-native-snap-carousel">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20||%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/meliorence/react-native-snap-carousel/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-snap-carousel)

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本   | 发布信息                                                     | 支持RN版本 |
|-------| ------------------------------------------------------------ | ---------- |
| 3.9.1 | [@react-native-oh-tpl/react-native-snap-carousel Releases](https://github.com/react-native-oh-library/react-native-snap-carousel/releases) | 0.72       |
| 3.10.0 | [@react-native-ohos/react-native-snap-carousel Releases]() | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-snap-carousel
	
# 0.77
npm install @react-native-ohos/react-native-snap-carousel
```

#### **yarn**

```bash
# 0.72
npm add @react-native-oh-tpl/react-native-snap-carousel
	
# 0.77
yarn add @react-native-ohos/react-native-snap-carousel
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { View, Text, Image, StyleSheet } from "react-native";
import Carousel from "react-native-snap-carousel";

export default function SnapCarouselExample(): JSX.Element {
  const ENTRIES1 = [
    {
      title: "Beautiful and dramatic Antelope Canyon",
      subtitle: "Lorem ipsum dolor sit amet et nuncat mergitur",
      url: "https://www-file.huawei.com/-/media/corp2020/images/tech4all/cases1/12/white-headed-langur-en-1.png?la=zh",
    },
    {
      title: "Earlier this morning, NYC",
      subtitle: "Lorem ipsum dolor sit amet",
      url: "https://www-file.huawei.com/-/media/corp2020/images/tech4all/cases1/12/white-headed-langur-en-2.jpg?la=zh",
    },
    {
      title: "White Pocket Sunset",
      subtitle: "Lorem ipsum dolor sit amet et nuncat ",
      url: "https://www-file.huawei.com/-/media/corp2020/images/tech4all/cases1/12/white-headed-langur-en-1.png?la=zh",
    },
    {
      title: "Acrocorinth, Greece",
      subtitle: "Lorem ipsum dolor sit amet et nuncat mergitur",
      url: "https://www-file.huawei.com/-/media/corp2020/images/tech4all/cases1/12/white-headed-langur-en-2.jpg?la=zh",
    },
    {
      title: "The lone tree, majestic landscape of New Zealand",
      subtitle: "Lorem ipsum dolor sit amet",
      url: "https://www-file.huawei.com/-/media/corp2020/images/tech4all/cases1/12/white-headed-langur-en-1.png?la=zh",
    },
    {
      title: "Middle Earth, Germany",
      subtitle: "Lorem ipsum dolor sit amet",
      url: "https://www-file.huawei.com/-/media/corp2020/images/tech4all/cases1/12/white-headed-langur-en-2.jpg?la=zh",
    },
  ];

  const _renderItem = ({ item, index }: any) => {
    return (
      <View>
        <Image source={{ uri: item.url }} style={styles.image} />
      </View>
    );
  };

  return (
    <View>
      <Carousel
        data={ENTRIES1}
        renderItem={_renderItem}
        sliderWidth={300}
        itemWidth={250}
        containerCustomStyle={styles.carouselContainer}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  carouselContainer: {
    height: 200,
    width: "100%",
    marginBottom: 20,
  },
  image: {
    resizeMode: 'cover',
    borderTopLeftRadius: 8,
    borderTopRightRadius: 8,
    width: 250,
    height: 300
  }
});
```
## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Type                       | Required                                               | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------- | ----------------------------------------------------- | -------- | ----------------- |
| `data`                        | 要循环播放的项目数组                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Array                      | yes                                              | iOS/Android      | yes               |
| `renderItem`                  | 从数据中获取一个项目并将其渲染到列表中。该函数接收一个参数  `{item, index}` (参见[用法](https://github.com/meliorence/react-native-snap-carousel#usage))并且必须返回一个 React 元素                                                                                                                                                                                                                                                                    | Function                   | yes                                              | iOS/Android      | yes               |
| `itemWidth`                   | 轮播图项目的宽度（以像素为单位），**所有项目必须相同**                                                                                                                                                                                                                                                                                                                                                                                                                  | Number                     | yes                      | iOS/Android      | yes               |
| `sliderWidth`                 | 轮播图本身的宽度（以像素为单位）                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Number                     | yes                      | iOS/Android      | yes               |
| `itemHeight`                  | 轮播图项目的高度（以像素为单位）， **所有项目必须相同**                                                                                                                                                                                                                                                                                                                                                                                                                 | Number                     | yes                       | iOS/Android      | yes               |
| `sliderHeight`                | 轮播图本身的高度（以像素为单位）                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Number                     |  yes                        | iOS/Android      | yes               |
| `loop`                        | E启用无限循环模式。**:w:warning: 如果 enableSnap 设置为 false，则此功能将不起作用。**                                                                                                                                                                                                                                                                                                                                                                                            | Boolean                    | no                                               | iOS/Android      | yes               |
| `loopClonesPerSide`           | 在原始项目每侧附加的克隆数量。**当快速滑动时**，用户最终需要暂停片刻，然后才能重新定位滚动（当到达项目集末尾时会发生这种情况）。通过增加此数值，用户将能够在停止之前滚动更多幻灯片；但您也会在内存中加载更多项目。这是在最佳用户体验和性能之间的权衡                                  | Number                     | no                                                   | iOS/Android      | yes               |
| `autoplay`                    | 	在挂载时触发自动播放。如果您启用自动播放，我们建议您将 enableMomentum 设置为 false（默认值）并将 lockScrollWhileSnapping 设置为 true；这将稍微提升用户体验                                                                                                                                                                                                                                                                                        | Boolean                    | no                                               | iOS/Android      | yes               |
| `autoplayDelay`               | 启动自动播放前和释放触摸后的延迟时间                                                                                                                                                                                                                                                                                                                                                                                                                      | Number                     | no                                                | iOS/Android      | yes               |
| `autoplayInterval`            | 导航到下一个项目之前的延迟时间（毫秒                                                                                                                                                                                                                                                                                                                                                                                                                                              | Number                     | no                                                | iOS/Android      | yes               |
| `layout`                      | 定义项目的渲染和动画方式。可能的值为 'default'、'stack' 和 'tinder'。:warning: **将此属性设置为 'stack' 或 'tinder' 将激活 useScrollView [以防止 FlatList 出现渲染错误](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/CUSTOM_INTERPOLATIONS.md#caveats)。因此，如果您有大型数据集，这些布局将不适用，因为所有项目都将提前渲染。** | String                     | no                                           | iOS/Android      | yes               |
| `containerCustomStyle`        | ScrollView 全局包装器的可选样式                                                                                                                                                                                                                                                                                                                                                                                                                                            | View Style Object          | no                                                 | iOS/Android      | yes               |
| `contentContainerCustomStyle` | ScrollView 项目容器的可选样式                                                                                                                                                                                                                                                                                                                                                                                                                                           | View Style Object          | no                                               | iOS/Android      | yes               |
| `inactiveSlideOpacity`        | 应用于非活动幻灯片的透明度效果值                                                                                                                                                                                                                                                                                                                                                                                                                                     | Number                     | no                                                 | iOS/Android      | yes               |
| `inactiveSlideScale`          | 应用于非活动幻灯片的"缩放"变换值                                                                                                                                                                                                                                                                                                                                                                                                                                 | Number                     | no                                                 | iOS/Android      | yes               |
| `inactiveSlideShift`                        | 	应用于非活动幻灯片的"平移"变换值（参见 #204 或"自定义插值"文档获取使用示例）。此属性在默认布局以外的布局中将不起作用on                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Number                      | no                                           | iOS/Android      | yes               |
| `layoutCardOffset`            | 用于增加或减少"堆叠"和"探戈"布局中的默认卡片偏移量                                                                                                                                                                                                                                                                                                                                                                                                 | Number                     | no | iOS/Android      | yes               |
| `slideStyle`                  | 每个项目容器的可选样式（即缩放和透明度被动画化的那个容器）                                                                                                                                                                                                                                                                                                                                                                                                   | Animated View Style Object | no                                               | iOS/Android      | yes               |
| `scrollInterpolator`                  | 用于定义自定义插值。请参阅[专门文档](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/CUSTOM_INTERPOLATIONS.md#summary)                                                                                                                                                                                                                                                                                                                                                                                                   | Function | no                                                  | iOS/Android      | yes              |
| `slideInterpolatedStyle`                  | 用于定义自定义插值。请参阅[专门文档](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/CUSTOM_INTERPOLATIONS.md#summary)                                                                                                                                                                                                                                                                                                                                                                                                   | Function | no                                                 | iOS/Android      | yes          |
| `activeAnimationOptions`                  | 自定义动画选项。请注意，默认情况下将启用 useNativeDriver，并且透明度的缓动将始终保持线性。**将此属性设置为 null 以外的值将触发自定义动画，并完全改变项目的动画方式：** 与其基于滚动值插值透明度和缩放（默认行为），不如在项目变为活动状态时立即播放您提供的自定义动画。 **T这意味着您不能将 layout、scrollInterpolator 或 slideInterpolatedStyle 属性与 activeAnimationOptions 一起使用。**                                                                                                                                                                                                                                                                                                                                                                                          | Object | no                                                  | iOS/Android      | yes               |
| `activeAnimationType`                  | 自定义 [动画类型：](https://reactnative.dev/docs/animated.html#configuring-animations)'decay'、'spring' 或 'timing'。请注意，这只会应用于缩放动画，因为透明度的动画类型将始终设置为 timing（没有人希望透明度"弹跳"）                                                                                                                                                                                ``````````````                                                                                                                                                                                                            | String | no                                                  | iOS/Android      | yes               |
| `activeSlideAlignment`                  | 确定活动幻灯片相对于轮播图的对齐方式。可能的值为：'start'、'center' 和 'end'。 **不建议将此属性与 layout 属性一起使用。**                                                                                                                                                                                                                                                                                                                                                                                             | String | no                                                 | iOS/Android      | yes               |
| `activeSlideOffset`                  | 从滑块中心开始，滚动到活动状态之前的最小幻灯片距离                                                                                                                                                                                                                                                                                                                                                                                       | Number | no                                               | iOS/Android      | yes               |
| `apparitionDelay`                  | FlatList 的初始化非常混乱，会出现许多不必要的闪烁和幻灯片移动。此属性控制在挂载时隐藏轮播图的延迟时间。 **警告：在 Android 上使用它可能导致[渲染问题](https://github.com/meliorence/react-native-snap-carousel/issues/236) (即图像不显示)。** 如果您决定使用它，请务必彻底测试                                                                                                                                                                                                                                                                                                                                                                                       | Number | no                                                | iOS/Android      | yes               |
| `callbackOffsetMargin`                  | 滚动事件可能触发得不够频繁，无法获得精确的测量值，因此无法提供可靠的回调。这通常是Android问题，可能与您使用的React Native版本有关 （参见[“不可靠的回调”](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/KNOWN_ISSUES.md#unreliable-callbacks)）。为了解决这个问题，您可以定义一个小的边距来增加"最佳位置"的宽度。默认值应该能覆盖大多数情况， **但是如果您遇到回调丢失的情况，您可能需要增加这个值。**                                                                                                                                                                                                                                                                                                                                                                                      | Number | no                                               | iOS/Android      | yes               |
| `enableMomentum`                  | 参见 [momentum](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/TIPS_AND_TRICKS.md#momentum)                                                                                                                                                                                                                                                                                                                                                                             | Boolean | no                                                  | iOS/Android      | yes              |
| `enableSnap`                  | 如果启用，释放触摸后将滚动到最近/活动项的中心                                                                                                                                                                                                                                                                                                                                                                             | Boolean | no                                               | iOS/Android      | yes               |
| `firstItem`                  | 要显示的第一个项目的索引。⚠️ **如果该属性似乎不起作用，请确保使用继承的属性`[getItemLayout](https://reactnative.dev/docs/flatlist#getitemlayout)` 和 `[initialScrollIndex](https://reactnative.dev/docs/flatlist#initialscrollindex)`。**                                                                                                                                                                                                                                                                                                                                                     | Number | no                                              | iOS/Android      | yes               |
| `hasParallaxImages`                  | 轮播图是否包含 <ParallaxImage /> 组件。需要传递特定数据给子组件时使用。                                                                                                                                                                                                                                                                                                                                                   | Boolean | no                                                 | iOS/Android      | yes               |
| `lockScrollTimeoutDuration`                  | 此属性与 lockScrollWhileSnapping 配合使用。当滚动被锁定时，会创建一个计时器，以便在常规回调处理出现问题时释放滚动。**通常情况下，您不需要使用此属性。**                                                                                                                                                                                                                                                                                                                                                | Number | no                                                 | iOS/Android      | yes               |
| `lockScrollWhileSnapping`                  | 在轮播图切换到某个位置时，防止用户再次滑动。这样可以防止一些次要问题（如滚动时意外点击项目、在切换过程中点击轮播图导致滚动动画停止、在Android上快速反向短距离滑动时的卡顿行为）。唯一的缺点是启用此属性会妨碍用户在项目之间快速滑动，因为滑动之间需要短暂的停顿。 **请注意，如果 enableMomentum 设置为 true，此属性将不会产生任何效果，因为它会阻碍自然和预期的行为。**                                                                                                                                                                                                                                                                                                                                           | Boolean | no                                               | iOS/Android      | yes               |
| `scrollEnabled`                  | 当设置为 false 时，视图无法通过触摸交互进行滚动([继承属性](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/PROPS_METHODS_AND_GETTERS.md#inherited-props))                                                                                                                                                                                                                                                                                                                                         | Boolean | no                                                | iOS/Android      | yes               |
| `shouldOptimizeUpdates`                  | 是否实现 shouldComponentUpdate 策略以最小化更新                                                                                                                                                                                                                                                                                                                                      | Boolean | no                                                 | iOS/Android      | yes               |
| `swipeThreshold`                  | 	触发快照的滑动 deltaX 值                                                                                                                                                                                                                                                                                                                                   | Number | no                                             | iOS/Android      | yes               |
| `useScrollView`                  | 是否使用 ScrollView 组件而不是默认的 FlatList 组件。优点是可以避免 FlatList 可能引起的渲染问题，并提供与 React Native 0.43 之前版本的兼容性。主要缺点是您将无法从 FlatList 的高级优化中获益，也无法使用 VirtualizedList 或 FlatList 的特定属性。 **W我们建议仅在幻灯片数量较少的情况下启用此选项，并在生产模式下彻底测试性能**. 从 3.7.6 版本开始，此属性还接受自定义滚动组件(see #498 for more info).                                                                                                                                                                                                                                                                                                                                    | Boolean | no                                                | iOS/Android      | yes               |
| `vertical`                  | 垂直布局幻灯片而不是水平布局                                                                                                                                                                                                                                                                                                                                  | Boolean | no                                             | iOS/Android      | yes               |


## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Prop                             | Description                                                                        | Type     | Required     | Platform | HarmonyOS Support |
| -------------------------------- | ---------------------------------------------------------------------------------- | -------- | ----------- | ------- | ----------------- |
| `onLayout(event)`                | 暴露的 View 回调函数；在组件挂载和布局变化时调用                      | Function | `no` | All     | yes               |
| `onScroll(event)`                | 暴露的 ScrollView 回调函数；在滚动过程中触发                               | Function | `no` | All     | yes               |
| `onBeforeSnapToItem(slideIndex)` | 在确定新激活项之后、跳转之前触发的回调函数 | Function | `no` | All     | yes               |
| `onSnapToItem(slideIndex)`       | 在跳转到某个项之后触发的回调函数                                           | Function | `no` | All     | yes               |

## 遗留问题
- [ ] enableMomentum属性在ios设备上效果不明显，Harmony上效果使用正常: [issue#1](https://github.com/react-native-oh-library/react-native-snap-carousel/issues/4)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-snap-carousel/blob/sig/LICENSE) ，请自由地享受和参与开源。