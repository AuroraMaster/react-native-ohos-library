> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>rn-placeholder</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mfrachet/rn-placeholder">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mfrachet/rn-placeholder/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 支持RN版本  |
| ----------| ---------- |
| 3.0.3    | 0.72/0.77 |


## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install rn-placeholder@3.0.3 --legacy-peer-deps
```

#### **yarn**

```bash
yarn add  rn-placeholder@3.0.3 --legacy-peer-deps
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import {
  Placeholder,
  PlaceholderMedia,
  PlaceholderLine,
  Fade,
} from "rn-placeholder";

const App = () => (
  <Placeholder
    Animation={Fade}
    Left={PlaceholderMedia}
    Right={PlaceholderMedia}
  >
    <PlaceholderLine width={80} />
    <PlaceholderLine />
    <PlaceholderLine width={30} />
  </Placeholder>
);
export default App;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1) ; IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25;
2. RNOH: 0.77.18; SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [rn-placeholder 源库地址](https://github.com/mfrachet/rn-placeholder)

**组件 Placeholder**

它是所有其他组件的外层包装。单独使用并不会产生有趣的效果；需要在其中放入一些行或媒体来发挥作用。它接受 React Native View 的全部属性，另外还包含：

| Name      | Description                                         | Type          | Required | Platform | HarmonyOS Support |
| --------- | --------------------------------------------------- | ------------- | -------- | -------- | ----------------- |
| Animation | 一个可选组件，用于为占位符添加动画效果 | Animations    | no       | All      | Yes               |
| Left      | 一个可选组件，显示在左侧        | ComponentType | no       | All      | Yes               |
| Right     | 一个可选组件，显示在右侧       | ComponentType | no       | All      | Yes               |

**_Animations_**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| --------- | -------------------------------------------------- | ------------- | -------- | -------- | -------- |
| Fade | 这是基础动画，会在指定的时间间隔让占位内容逐渐清晰| ComponentType | no | All | Yes |
| ShineOverlay | 这会向占位符应用一个从左到右的 tiny 覆盖层。效果不错，但仅在不自定义样式时有效：仅在白色背景上显示灰色线|ComponentType| no | All | Yes |
| Shine | 这个 shine 动画试图通过仅动画占位符的不同部分来克服 ShineOverlay 动画的覆盖层问题 | ComponentType | no | All | Yes |
| Loader | 这是一个基于每个平台标准加载器（ActivityIndicator）的简单占位符动画| ComponentType | no | All | Yes |
| Progressive | 一个渐进加载动画效果 | ComponentType | no | All | Yes |
| Tweaking existing animations | 可以通过传递附加属性来调整特定动画。然而请记住，重要的是要将属性从 Animation 渲染函数中传播出来。否则会出现异常行为| ComponentType | no | All | Yes |

**组件 PlaceholderLine**

PlaceholderLine 是占位符的两种基础且可视的组件之一。

| Name     | Description                                                            | Type    | Required | Platform | HarmonyOS Support |
| -------- | ---------------------------------------------------------------------- | ------- | -------- | -------- | ----------------- |
| height   | 行高，默认值为 12	                                      | number  | no       | All      | Yes               |
| color    | 颜色，默认值为 #efefef                                   | string  | no       | All      | Yes               |
| width    | 行宽，默认值为 100(%)	                                | number  | no       | All      | Yes               |
| noMargin | 是否带有底部边距，默认值为 false | boolean | no       | All      | Yes               |
| style    | 自定义底层 View 组件的样式	                   | object  | no       | All      | Yes               |

**组件 PlaceholderMedia**

PlaceholderMedia 是占位符的两种基础且可视的组件中的另一个。它也可以像下面这样单独作为占位使用：

| Name    | Description                                              | Type    | Required | Platform | HarmonyOS Support |
| ------- | -------------------------------------------------------- | ------- | -------- | -------- | ----------------- |
| size    | 媒体大小（高度 / 宽度），默认值为 40           | number  | no       | All      | Yes               |
| isRound | 定义媒体是否为圆角， 默认值为 false | boolean | no       | All      | Yes               |
| color   | 媒体颜色，默认值为 #efefef                      | string  | no       | All      | Yes               |
| style   | 自定义底层 View 组件的样式     | object  | no       | All      | Yes               |

## 遗留问题
## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mfrachet/rn-placeholder/blob/master/LICENSE.md) ，请自由地享受和参与开源。