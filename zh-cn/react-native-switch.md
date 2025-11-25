> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-switch</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/shahen94/react-native-switch">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/shahen94/react-native-switch/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/shahen94/react-native-switch)

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本                 | 支持RN版本 |
| ------------------------- | -------------------------- |
| 1.5.1 | 0.72/0.77 |

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-switch@1.5.1
```

#### **yarn**

```bash
yarn add react-native-switch@1.5.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { Switch } from "react-native-switch";
import {SafeAreaView, StyleSheet,Button, Text, View, Alert} from 'react-native';


export function SwitchDemo(){
  const [isEnabled, setIsEnabled] = useState(false);
  const toggleSwitch = (val:boolean) => {setIsEnabled(val) };
  
  return(
    <View  style={styles.container}>
      <Text style={{fontSize:32}}>Welcome to React Native !</Text>
      <Switch
        value={isEnabled}
        onValueChange={(val) => toggleSwitch((val))}
        disabled={false}
        activeText={'On'}
        inActiveText={'Off'}
        circleSize={30}
        barHeight={30}
        circleBorderWidth={3}
        backgroundActive={'green'}
        backgroundInactive={'gray'}
        circleActiveColor={'#30a566'}
        circleInActiveColor={'#fff'}
        renderInsideCircle={() => ''} // custom component to render inside the Switch circle (Text, Image, etc.)
        changeValueImmediately={true} // if rendering inside circle, change state immediately or wait for animation to complete
        innerCircleStyle={{ alignItems: "center", justifyContent: "center" }} // style for inner animated circle for what you (may) be rendering inside the circle
        outerCircleStyle={{ }} // style for outer animated circle
        renderActiveText={true}
        renderInActiveText={true}
        switchLeftPx={2} // denominator for logic when sliding to TRUE position. Higher number = more space from RIGHT of the circle to END of the slider
        switchRightPx={2} // denominator for logic when sliding to FALSE position. Higher number = more space from LEFT of the circle to BEGINNING of the slider
        switchWidthMultiplier={3} // multiplied by the `circleSize` prop to calculate total width of the Switch
        switchBorderRadius={50} // Sets the border Radius of the switch slider. If unset, it remains the circleSize.
      />
      <Text style={{color:'gray',fontSize:20,marginBottom:10}}>To get started,edit index.harmony.js</Text>
      <Text style={{color:'gray',fontSize:20}}>Press Cmd +R to reload,</Text>
      <Text style={{color:'gray',fontSize:20}}>Cmd+D or shake for dev menu</Text>
    </View>
    )
  }
  const styles = StyleSheet.create({
    container: {
      flex: 1,
      alignItems: "center",
      justifyContent: "center",
      backgroundColor:"#fff",
      
    }
  });
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.29;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 Yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|        Name        |                         Description                          |        Type         | Required |  Platform   | HarmonyOS Support |
| :----------------: | :----------------------------------------------------------: | :-----------------: | :------: | :---------: | :---------------: |
|     onValueChange      |     值改变时回调 (value: `boolean`)    | function |    No    | Android/IOS |        Yes        |
|       disabled        |          是否禁用开关         |       boolean       |    No    | Android/IOS |        Yes        |
|      activeText       | 开关打开时显示的文本 |   string  |    No    | Android/IOS |        Yes        |
|     inActiveText      |         开关关闭时显示的文本    |      string      |    No    | Android/IOS |        Yes        |
|     backgroundActive      | 开关打开时的背景色 |      string      |    No    | Android/IOS |        Yes        |
|      backgroundInactive      | 开关关闭时的背景色 |   string   |    No    | Android/IOS |        Yes        |
|      value       | 开关的当前值 |  boolean   |    No    | Android/IOS |        Yes        |
|      circleActiveColor       | 开关打开时圆形滑块的颜色 |      string       |    No    | Android/IOS |        Yes        |
|    circleInActiveColor     | 开关关闭时圆形滑块的颜色 |      string       |    No    | Android/IOS |        Yes        |
|       circleSize        | 圆形滑块的尺寸 |  number  |    No    | Android/IOS |        Yes        |
|     circleBorderWidth     | 圆形滑块的边框宽度 |      number |    No    | Android/IOS |        Yes        |
|     circleBorderActiveColor     | 开关打开时圆形滑块的边框颜色 |      string |    No    | Android/IOS |        Yes        |
|     circleBorderInactiveColor      | 开关关闭时圆形滑块的边框颜色 |       string       |    No    | Android/IOS |        Yes        |
| activeTextStyle | 打开状态文本的样式 | StyleProp`<TextStyle> ` | No | Android/IOS | Yes |
| inactiveTextStyle | 关闭状态文本的样式 | StyleProp`<TextStyle> ` | No | Android/IOS | Yes |
| containerStyle | 开关容器的样式 | StyleProp`<ViewStyle> ` | No | Android/IOS | Yes |
| barHeight | 开关滑槽的高度（不包含边框） | number | No | Android/IOS | Yes |
| renderInsideCircle | 自定义渲染在圆形滑块内部的组件 | function | No | Android/IOS | Yes |
| changeValueImmediately | 当在圆形滑块内渲染自定义内容时，是立即改变状态还是等待动画完成 | boolean | No | Android/IOS | Yes |
| innerCircleStyle | 内部圆形动画视图的样式（用于您可能在圆形内部渲染的内容） | No | Android/IOS | Yes |
| outerCircleStyle | 外部圆形动画视图的样式 | StyleProp`<ViewStyle>` | StyleProp`<ViewStyle> ` | No | Android/IOS | Yes |
| renderActiveText | 是否显示打开状态的文本  | boolean | No | Android/IOS | Yes |
| renderInActiveText | 是否显示关闭状态的文本 | boolean | No | Android/IOS | Yes |
| switchLeftPx | 滑块滑动到打开(TRUE)位置时的逻辑分母。数值越大，圆形滑块右侧到滑槽末端的空间越大 | number | No | Android/IOS | Yes |
| switchRightPx | 与 `circleSize` 相乘来计算开关总宽度的参数之一 | number | No | Android/IOS | Yes |
| switchWidthMultiplier | 与 `circleSize` 相乘来计算开关总宽度的乘数 | number | No | Android/IOS | Yes |
| switchBorderRadius | 设置开关滑槽的边框圆角半径。如果未设置，则保持与 `circleSize` 一致 | number | No | Android/IOS | Yes |
| testID | 用于自动化测试的开关标识符 | string | No | Android/IOS | Yes |
## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/shahen94/react-native-switch/blob/master/LICENSE) ，请自由地享受和参与开源。
