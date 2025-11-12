> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-marquee</code> </h1>
</p>

本项目基于 [react-native-marquee@0.5.0](https://github.com/kyo504/react-native-marquee/tree/v0.5.0) 开发。

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.5.0      | [@react-native-oh-tpl/react-native-marquee Releases](https://github.com/react-native-oh-library/react-native-marquee/releases) | 0.72       |
| 0.5.1      | [@react-native-ohos/react-native-marquee Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-marquee/releases)     | 0.77       |

## 1. 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# V0.5.0
npm install @react-native-oh-tpl/react-native-marquee

# V0.5.1
npm install @react-native-ohos/react-native-marquee
```

#### **yarn**

```bash
# V0.5.0
yarn add @react-native-oh-tpl/react-native-marquee

# V0.5.1
yarn add @react-native-ohos/react-native-marquee
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, { Component } from "react";
import { StyleSheet, View } from "react-native";
import MarqueeText from "react-native-marquee";

export default class MarqueeTextSample extends Component {
  render() {
    return (
      <View style={styles.container}>
        <MarqueeText
          style={{ fontSize: 24 }}
          speed={1}
          marqueeOnStart={true}
          loop={true}
          delay={1000}
        >
          Lorem Ipsum is simply dummy text of the printing and typesetting
          industry and typesetting industry.
        </MarqueeText>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
  },
});
```

## 2. 约束与限制

### 2.1 兼容性

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.5.0      | [@react-native-oh-tpl/react-native-marquee Releases](https://github.com/react-native-oh-library/react-native-marquee/releases) | 0.72       |
| 0.5.1      | [@react-native-ohos/react-native-marquee Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-marquee/releases)     | 0.77       |


## 3. 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ----------------- | -------- | -------- | ------- | ------------------------------------------------------------ | -------- 
| marqueeOnStart    | 是否在渲染后立即启动字幕动画的标志                           | boolean  | no | All      | yes               |
| speed             | 以像素/秒计算的速度                                          | number   | no | All      | yes               |
| loop              | 是否循环字幕动画的标志                                       | boolean  | no | All      | yes               |
| delay             | 渲染后延迟动画的持续时间，以毫秒为单位                       | number   | no | All      | yes               |
| onMarqueeComplete | 字幕完成动画并停止时的回调                                   | function | no | All      | yes               |
| consecutive       | 一个标志，用于启用模仿HTML字幕元素默认行为的连续模式。如果循环为false，则不生效 | boolean  | no | All      | yes               |

## 4. 方法

这些方法是可选的，你可以使用 isOpen 属性代替。

| Name     | Description     | Type   | Required | Platform | HarmonyOS Support |
| ---------| --------------- | -------- | -------- | -------- | ----------------- |
| start    | Start animation | Function | no       | All      | yes               |
| stop     | Stop animation  | Function | no       | All      | yes               |

## 5. 遗留问题

## 6. 其他

## 7. 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/kyo504/react-native-marquee/blob/master/LICENSE) ，请自由地享受和参与开源。

