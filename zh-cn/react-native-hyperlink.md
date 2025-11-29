模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-hyperlink</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/obipawan/react-native-hyperlink">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/obipawan/react-native-hyperlink/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/obipawan/react-native-hyperlink)

| 三方库版本 | 支持RN版本 |
| :--- | :--- |
| 0.0.22| 0.72/0.77 |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-hyperlink@0.0.22
```

#### **yarn**

```bash
yarn add react-native-hyperlink@0.0.22
```

使用时,还需在项目下的module.json5处配置querySchemes

```diff
{
  "module": {
    ...
+   "querySchemes": ["maps","http","https","customDomain"],
  }
}
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { View, Text } from "react-native";
import Hyperlink from "react-native-hyperlink";

export default function App() {
  return (
    <Hyperlink
      linkDefault
      injectViewProps={(url) => ({
        testID: url === "http://link.com" ? "id1" : "id2",
        style:
          url === "https://link.com" ? { color: "red" } : { color: "blue" },
        //any other props you wish to pass to the component
      })}
    >
      <Text>
        You can pass props to clickable components matched by url.
        <Text>This url looks red https://link.com</Text> and this url looks blue
        https://link2.com{" "}
      </Text>
    </Hyperlink>
  );
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25 (API Version 12 Canary4); IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.29;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name            | Description                                                                 | Type                     | Required | Platform | HarmonyOS Support |
| --------------- | --------------------------------------------------------------------------- | ------------------------ | -------- | -------- | ----------------- |
| linkify         | linkify-it 对象，用于自定义模式                                             | object                   | no       | all      | yes               |
| linkStyle       | 设置可点击文本的高亮样式                                                    | object                   | no       | all      | yes               |
| linkText        | 用于替换被解析文本的字符串或函数                                            | string   &#124; function | no       | all      | yes               |
| onPress         | 点击可点击文本时的回调函数，以解析后的文本作为参数                          | function                 | no       | all      | yes               |
| onLongPress     | 长按可点击文本时的回调函数，以解析后的文本作为参数                          | function                 | no       | all      | yes               |
| linkDefault     | 处理 onPress 的平台特定默认回退行为。使用 Linking。默认禁用                 | boolean                  | no       | all      | yes               |
| injectViewProps | 以 URL 为参数的函数，用于向可点击组件注入属性                               | function                 | no       | all      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/obipawan/react-native-hyperlink/blob/master/LICENSE) ，请自由地享受和参与开源。