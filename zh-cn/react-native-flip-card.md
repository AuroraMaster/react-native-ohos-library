> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-flip-card</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/moschan/react-native-flip-card">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/moschan/react-native-flip-card/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/moschan/react-native-flip-card)

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 支持RN版本  |
| ----------| ---------- |
| 3.5.7   | 0.72/0.77 |

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm i react-native-flip-card@3.5.7
```

#### **yarn**

```bash
yarn add react-native-flip-card@3.5.7
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import FlipCard from "react-native-flip-card";
import {
  Text,
  View,
  StyleSheet,
  ScrollView,
  TouchableOpacity,
} from "react-native";

export const FlipCardExample = () => {
  const styles = StyleSheet.create({
    container: {
      flex: 1,
      justifyContent: "center",
      alignItems: "center",
      backgroundColor: "#F5FCFF",
    },
    welcome: {
      fontSize: 20,
      textAlign: "center",
      margin: 10,
      marginTop: 20,
    },
    instructions: {
      textAlign: "center",
      color: "#333333",
      marginBottom: 5,
    },
    card: {
      width: 200,
      marginTop: 20,
    },
    face: {
      flex: 1,
      backgroundColor: "#2ecc71",
      justifyContent: "center",
      alignItems: "center",
    },
    back: {
      flex: 1,
      backgroundColor: "#f1c40f",
      justifyContent: "center",
      alignItems: "center",
    },
    button: {
      width: 100,
      height: 30,
      marginTop: 30,
      paddingTop: 6,
      paddingBottom: 6,
      borderRadius: 3,
      borderWidth: 1,
      backgroundColor: "#007AFF",
      borderColor: "transparent",
    },
    buttonText: {
      color: "#fff",
      textAlign: "center",
    },
    img: {
      flex: 1,
      height: 64,
    },
  });
  const [flip, setFlip] = useState(false);
  var CARDS = [1, 2, 3, 4, 5, 6, 7, 8, 9];
  const MyFlipCard = ({ val }) => {
    return (
      <View style={{ margin: 3 }}>
        <FlipCard style={styles.card}>
          <View style={styles.face}>
            <Text>Card {val}</Text>
          </View>
          <View style={styles.back}>
            <Text>The back side</Text>
          </View>
        </FlipCard>
      </View>
    );
  };
  const createCard = (val, i) => <MyFlipCard key={i} val={val} />;

  return (
    <View style={styles.container}>
      <ScrollView>
        <Text style={styles.welcome}>Flip Card Example</Text>
        <View>
          <Text style={styles.welcome}>Minimal</Text>
          <FlipCard style={{ marginBottom: 5 }}>
            <View style={styles.face}>
              <Text>The Face</Text>
            </View>
            <View style={styles.back}>
              <Text>The Back</Text>
            </View>
          </FlipCard>

          <Text style={styles.welcome}>Customized</Text>
          <FlipCard
            flip={flip}
            friction={3}
            perspective={500}
            flipHorizontal={true}
            flipVertical={false}
            clickable={true}
            style={styles.card}
            alignHeight={true}
            onFlipStart={(isFlipStart) => {
              console.log("isFlipStart", isFlipStart);
            }}
            useNativeDriver={true}
          >
            <View style={styles.face}>
              <Text>The Face</Text>
            </View>
            <View style={styles.back}>
              <Text style={{ fontSize: 50 }}> The Back </Text>
            </View>
          </FlipCard>
          <FlipCard
            flip={flip}
            friction={10}
            perspective={4000}
            flipHorizontal={false}
            flipVertical={true}
            clickable={true}
            style={styles.card}
            alignHeight={true}
            onFlipEnd={(isFlipEnd) => {
              console.log("isFlipEnd", isFlipEnd);
            }}
          >
            <View style={styles.face}>
              <Text>The Face</Text>
            </View>
            <View style={styles.back}>
              <Text>T</Text>
              <Text>h</Text>
              <Text>e</Text>
              <Text></Text>
              <Text>B</Text>
              <Text>a</Text>
              <Text>c</Text>
              <Text>k</Text>
            </View>
          </FlipCard>
        </View>
        <View>
          <TouchableOpacity
            style={styles.button}
            onPress={() => {
              setFlip({ flip: !flip });
            }}
          >
            <Text style={styles.buttonText}>Flip</Text>
          </TouchableOpacity>
        </View>
        <View>{CARDS.map(createCard)}</View>
      </ScrollView>
    </View>
  );
};
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.26; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE：DevEco Studio 5.0.3.300SP2; ROM:3.0.0.24;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.77.18; SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;

## 属性

### FlipCard

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。
>
> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

该库为 UI 组件库，通过配置属性标签，实现对应的功能。

| Name            | Type     | Description                                                                                                                     | Default | Required | Platform    | HarmonyOS Support |
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| flip            | boolean  | 如果您想更改默认显示面，可以将此参数设置为true。如果您要动态更改显示面，可以传递布尔变量。 | false   | no       | iOS/Android | yes               |
| clickable       | boolean  | 如果您想禁用卡片点击，可以将此参数设置为false。                                                      | true    | no       | iOS/Android | yes               |
| friction        | number   | 卡片动画的摩擦系数                                                                                                 | 6       | no       | iOS/Android | yes               |
| perspective     | number   | 应用于翻转变换的透视效果量                                                                 | 1000    | no       | iOS/Android | no               |
| flipHorizontal  | boolean  | 如果设置为true，卡片将水平翻转。                                                                                    | false   | no       | iOS/Android | yes               |
| flipVertical    | boolean  | 如果设置为false，卡片不会垂直翻转。如果同时将flipHorizontal和flipVertical设置为true，卡片将沿对角线翻转。| true    | no       | iOS/Android | yes               |
| onFlipStart     | function | 当卡片开始翻转动画时，会调用onFlipStart函数并传递参数。                                                       | NA      | no       | iOS/Android | yes               |
| onFlipEnd       | function | 当卡片完成翻转动画时，会调用onFlipEnd函数并传递参数。                                                      | NA      | no       | iOS/Android | yes               |
| alignHeight     | boolean  | 如果将alignHeight参数设置为true，卡片将保持较大一面的高度。                                               | false   | no       | iOS/Android | yes               |
| alignWidth      | boolean  | 如果将alignWidth参数设置为true，卡片将保持较大一面的宽度。                                                     | false   | no       | iOS/Android | yes               |
| useNativeDriver | boolean  | 如果将useNativeDriver参数设置为true，卡片动画将使用原生驱动。                                | true    | no       | iOS/Android | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/moschan/react-native-flip-card/blob/master/LICENSE) ，请自由地享受和参与开源。
