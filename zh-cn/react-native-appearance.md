> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-appearance</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/expo/react-native-appearance">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/expo/react-native-appearance/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [Github 地址](https://github.com/expo/react-native-appearance)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-appearance@0.3.5
```

#### **yarn**

```bash
yarn add react-native-appearance@0.3.5
```

<!-- tabs:end -->

### 示例

下面的代码展示了如何使用Appearance库：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useState } from "react";
import { Button, View, Text, StyleSheet, useColorScheme } from 'react-native';
import { AppearanceHarmony } from 'react-native-appearance';

export default class App extends React.Component {

  // 当前显示模式
  const scheme = useColorScheme();
  const currentScheme = scheme ?? scheme!.toString();

  // 监听显示模式
  const [listenedScheme, setListenedScheme] = useState('');
  AppearanceHarmony.addChangeListener(({ colorScheme }) => {
    setListenedScheme(colorScheme ?? colorScheme!.toString());
  });

  // 获取显示模式
  const [gotScheme, setGotScheme] = useState('');
  const getAppearance = ()=> {
    const result = AppearanceHarmony.getColorScheme();
    setGotScheme(result ?? result!.toString());
  }

  // 修改显示模式
  const changeAppearance = ()=> {
    const result = AppearanceHarmony.getColorScheme();
    if (result == 'dark') {
      AppearanceHarmony.setColorScheme('light');
    } else if (result == 'light') {
      AppearanceHarmony.setColorScheme('dark');
    }
  }

  const styles = StyleSheet.create({
    container: {
      padding: 50,
      width: '100%',
      height: '100%',
      backgroundColor: currentScheme == 'dark' ? 'lightgray': 'white'
    },
    row: {
      paddingTop: 30
    }
  });

  render() {
    return (
      <View style={styles.container}>
          <Text style={styles.row}>当前显示模式：{currentScheme}</Text>
          <Text style={styles.row}>监听的显示模式：{listenedScheme}</Text>
          <Text style={styles.row}>获取的显示模式：{gotScheme}</Text>
          <View style={styles.row}><Button title="获取显示模式" onPress={()=>getAppearance()} /></View>
          <View style={styles.row}><Button title="修改显示模式" onPress={()=>changeAppearance()} /></View>
      </View>
    )
  }

}
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

本文档内容基于以下版本验证通过：

react-native-harmony：0.72.86; SDK：HarmonyOS 5.1.0.125; IDE：DevEco Studio 5.1.0.849; ROM：5.0.0.150;

react-native-harmony：0.77.18; SDK：HarmonyOS 5.1.0.125; IDE：DevEco Studio 5.1.0.849; ROM：5.0.0.150;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 函数

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `useColorScheme` | 获取当前显示模式。返回 ColorSchemeName 对象。 | `function` | No | All | yes |
| `getColorScheme` | 获取当前显示模式。返回 ColorSchemeName 对象。 | `function` | No | All | yes |
| `setColorScheme` | 设置显示模式。 | `function` | No | All | yes |
| `addChangeListener`| 监听系统显示模式变化。返回 ColorSchemeName 对象。 | `function` | No | All | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/expo/react-native-appearance/blob/master/LICENSE) ，请自由地享受和参与开源。


