> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-typography</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/hectahertz/react-native-typography">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/hectahertz/react-native-typography/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-typography)

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.4.1      | [react-native-oh-tpl/react-native-typography Releases](https://github.com/react-native-oh-library/react-native-typography/releases) | 0.72       |
| 1.5.0      | [@react-native-ohos/react-native-typography Releases]()      | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-typography
# 0.77
npm install @react-native-ohos/react-native-typography
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-typography
# 0.77
yarn add @react-native-ohos/react-native-typography
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变

```js
import { View, Text } from "react-native";
import React from "react";
import { iOSUIKit, material, systemWeights } from "react-native-typography";

export function TypographyExample1() {
  return (
    <View style={{ backgroundColor: "white" }}>
      <Text style={iOSUIKit.largeTitleEmphasized}>Hello iOS UI Kit!</Text>
      <Text style={material.title}>Title</Text>
      <Text style={systemWeights.light}>Title</Text>
    </View>
  );
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                | Description                                                                                                                                                                                                                                                                                                                                                                  | Type   | Required | Platform | HarmonyOS Support |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | ----------------- |
| material            | 包含[Material Design 指南](https://material.io/guidelines/style/typography.html#typography-styles)中定义的所有样式。定义大小、粗细和颜色。                                                                                                                                                                                                  | object | no       | All      | yes               |
| materialDense       | 	material 的 Dense 脚本                                                                                                                                                                                                                                                                                                                                                     | object | no       | All      | yes               |
| materialTall        | material 的 Tall 脚本                                                                                                                                                                                                                                                                                                                                                      | object | no       | All      | yes               |
| human               | 定义于[Human Interface Guidelines](https://developer.apple.com/ios/human-interface-guidelines/visual-design/typography/)。定义大小、粗细和颜色。                                                                                                                                                                                                            | object | no       | All      | yes               |
| humanDense          | 	human 的 Dense 脚本                                                                                                                                                                                                                                                                                                                                                       | object | no       | All      | yes               |
| humanTall           | human 的 Tall 脚本                                                                                                                                                                                                                                                                                                                                                         | object | no       | All      | yes               |
| iOSUIKit            | 	提取自[官方 Apple Sketch 文件](https://developer.apple.com/design/resources/)这些是属于 iOS UIKit 类别的文本样式，用于构建 iOS 应用的 UI 组件。它们建立在 Human Interface 样式的基础上，自定义了一些属性，如粗细或字母间距。                                      | object | no       | iOS      | yes               |
| iOSUIKitDense       | iOSUIKit 的 Dense 脚本                                                                                                                                                                                                                                                                                                                                                     | object | no       | iOS      | yes               |
| iOSUIKitTall        | iOSUIKit 的 Tall 脚本 scripts                                                                                                                                                                                                                                                                                                                                                      | object | no       | iOS      | yes               |
| systemWeights       | 在 React Native 中，字体粗细有时由 fontFamily 和 fontWeight 成对组成，但并非总是如此！这取决于字体类型，有时仅由 fontFamily 定义。使用这些辅助工具，您无需担心这些不一致性。要将它们与集合样式（或您自己的样式）结合使用，只需展开它们即可，因为它们是普通对象。 | object | no       | All      | yes               |
| systemDenseWeights  | systemWeights 的 Dense 脚本                                                                                                                                                                                                                                                                                                                                                | object | no       | All      | yes               |
| systemTallWeights   | systemWeights 的 Tall 脚本                                                                                                                                                                                                                                                                                                                                                | object | no       | All      | yes               |
| sanFranciscoWeights | San Francisco 字体                                                                                                                                                                                                                                                                                                                                                       | object | no       | iOS      | yes               |
| robotoWeights       | 这些字重**仅适用于 Android**，因为它们直接引用了原生 Roboto 字体。                                                                                                                                                                                                                                                                      | object | no       | Android      | yes               |
| webWeights          | 这些字重**仅适用于网页**，并渲染[react-native-web](https://github.com/necolas/react-native-web)的系统字体堆栈。                                                                                                                                                                                                                             | object | no       | Web      | yes               |
| iOSColors           | iOS颜色                                                                                                                                                                                                                                                                                                                                                                   | object | no       | iOS      | yes               |
| materialColors      | 	Material 颜色                                                                                                                                                                                                                                                                                                                                                             | object | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/hectahertz/react-native-typography/blob/master/LICENSE) ，请自由地享受和参与开源。
