> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-animate-number</code> </h1>
</p>
<p align="center">
        <a href="https://github.com/wkh237/react-native-animate-number">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/wkh237/react-native-animate-number/tree/0.1.2)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本| 支持RN版本 |
| -------- | ----------|
| 0.1.2    | 0.72/0.77      |

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-animate-number@0.1.2
```

#### **yarn**

```bash
yarn add react-native-animate-number@0.1.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useState } from "react";
import { StyleSheet, Text, View, Button } from "react-native";
import AnimateNumber from "react-native-animate-number";

const App = () => {
  const [value, setValue] = useState(0);
  const onPress = () => {
    setValue(100);
  };
  const [finish, setFinish] = useState("");
  const [progress, setProgress] = useState("");
  const onProgress = () => {
    setProgress("动画正在更新...");
  };
  const onFinish = () => {
    setFinish("动画更新完成");
  };
  return (
    <View style={styles.container}>
      <View style={styles.button}>
        <Button title={"点击开始动画"} onPress={onPress} />
      </View>
      <Text style={styles.row}>
        <Text>linear:</Text>
        <AnimateNumber
          value={value}
          timing="linear"
          countBy={1}
          interval={150}
        />
      </Text>
      <Text style={styles.row}>
        <Text>easeOut:</Text>
        <AnimateNumber
          value={value}
          timing="easeOut"
          countBy={1}
          interval={150}
        />
      </Text>
      <Text style={styles.row}>
        <Text>easeIn:</Text>
        <AnimateNumber
          value={value}
          timing="easeIn"
          countBy={1}
          interval={150}
        />
      </Text>
      <Text style={styles.row}>
        <Text>steps:</Text>
        <AnimateNumber value={value} steps={5} interval={2000} />
      </Text>
      <Text style={styles.row}>
        <Text>Formate Example:</Text>
        <AnimateNumber
          value={value}
          countBy={1}
          interval={150}
          formatter={(val: any) => {
            return "$ " + parseFloat(val).toFixed(2);
          }}
        />
      </Text>
      <Text style={styles.row}>
        <Text>{progress}</Text>
      </Text>
      <Text style={styles.row}>
        <AnimateNumber
          value={30}
          countBy={5}
          interval={600}
          onProgress={onProgress}
          onFinish={onFinish}
        />
      </Text>
      <Text style={styles.row}>
        <Text>{finish}</Text>
      </Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    justifyContent: "center",
    flex: 1,
    alignItems: "center",
  },
  row: {
    fontSize: 20,
    fontWeight: "bold",
    flexDirection: "row",
    marginBottom: 20,
  },
  button: {
    marginBottom: 20,
  },
});

export default App;
```

## 约束与限制

### 兼容性

在以下版本验证通过

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112

## 属性

| Name         | Description                                                                                                                                                 | Type     | Required | Platform    | HarmonyOS Support |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| `value`      | AnimateNumber 组件的值。                                                                                                                      | number   | yes      | Android IOS | YES               |
| `countBy`    | 将此属性设置为强制组件值按此数值增加/减少。                                                                        | number   | No       | Android IOS | YES               |
| `interval`   | 每帧动画的基本间隔时间（单位：毫秒）。                                                                                                           | number   | No       | Android IOS | YES               |
| `steps`      | 设置动画的总帧数。例如，若间隔为14毫秒且步数为30帧，当采用线性缓动函数时，该动画将耗时14×30毫秒完成。 | number   | No       | Android IOS | YES               |
| `timing`     | 一个用于自定义 WebView 样式的样式对象.                                                                                               | number   | No       | Android IOS | YES               |
| `formatter`  | 自定义 CSS 内容将被添加到页面中。                                                                                               | string   | No       | Android IOS | YES               |
| `onProgress` | 高度或宽度的任意变更都将触发 onSizeUpdated 事件。                                                                                                  | function | No       | Android IOS | YES               |
| `onFinish`   | 布尔值，用于控制是否在 WebView 中显示水平滚动指示器。                                                               | function | No       | Android IOS | YES               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://www.mit-license.org/) ，请自由地享受和参与开源。
