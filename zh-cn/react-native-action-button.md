> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-action-button</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mastermoo/react-native-action-button">
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
     <a href="https://github.com/mastermoo/react-native-action-button/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/mastermoo/react-native-action-button)

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 支持RN版本 |
| ---------- | ---------- |
| 2.8.5    | 0.72/0.77    |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-action-button@2.8.5
```

#### **yarn**

```bash
yarn add react-native-action-button@2.8.5
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, { Component } from "react";
import { StyleSheet, View,Text } from "react-native";
import ActionButton from "react-native-action-button";

export class App extends Component {
  render() {
    return (
      <View style={{ flex: 1, backgroundColor: "#f3f3f3" }}>
        <ActionButton buttonColor="rgba(231,76,60,1)">
          <ActionButton.Item
            buttonColor="#9b59b6"
            title="New Task"
            onPress={() => console.log("notes tapped!")}
          >
            <Text>1</Text>
          </ActionButton.Item>
          <ActionButton.Item
            buttonColor="#3498db"
            title="Notifications"
            onPress={() => {}}
          >
             <Text>2</Text>
          </ActionButton.Item>
          <ActionButton.Item
            buttonColor="#1abc9c"
            title="All Tasks"
            onPress={() => {}}
          >
             <Text>3</Text>
          </ActionButton.Item>
        </ActionButton>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  actionButtonIcon: {
    fontSize: 20,
    height: 22,
    color: "#000",
  },
});
```
## 约束与限制

## 兼容性

在以下版本验证通过

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;
3. RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25;
4. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
5. RNOH: 0.77.18; SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                      |  Description                                                                                                                                                                                                                                             | Type     | Required | Platform |  HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |----------| -------- |
| resetToken                | 用于在重新渲染周期中重置内部组件状态（展开/折叠）。同步组件状态。                                                                                                                           | any      | No       | All      | Yes      |
| size                      | 用于改变按钮的大小                                                                                                                                                                                                         | number   | No       | All        | Yes      |
| active                    | 操作按钮是否可见                                                                                                                                                                                                                     | boolean  | No       | All        | Yes      |
| position                  | 可选值之一：left、center 和 right                                                                                                                                                                                                                     | string   | No       | All        | Yes      |
| autoInactive              | 当按下 ActionButton.Item 时自动隐藏 ActionButtons。                                                                                                                                                                                        | boolean  | No       | All        | Yes      |
| hideShadow                | 用于隐藏默认的 elevation 和 boxShadow                                                                                                                                                                                              | boolean  | No       | All        | Yes      |
| spacing                   | ActionButton.Items 之间的间距                                                                                                                                                                                                            | number   | No       | All        | Yes      |
| offsetX                   | 距离屏幕左侧/右侧的偏移量                                                                                                                                                                                                     | number   | No       | All        | Yes      |
| offsetY                   | 距离屏幕底部/顶部的偏移量                                                                                                                                                                                                          | number   | No       | All        | Yes      |
| buttonText                | 用于在按钮上设置不同的文本                                                                                                                                                                                                    | string   | No       | All        | Yes      |
| degrees                   | 旋转图标的角度                                                                                                                                                                                                            | number   | No       | All        | Yes      |
| shadowStyle               | 您想要传递给操作按钮的自定义阴影样式                                                                                                                                                                                                     | style    | No       | All        | Yes      |
| bgColor                   | ActionButtons 可见时的背景颜色                                                                                                                                                                                                   | string   | No       | All        | Yes      |
| bgOpacity                 | 设置背景颜色的透明度                                                                                                                                                                                                      | number   | No       | All        | Yes      |
| buttonTextStyle           | 用于设置按钮文本的文本样式                                                                                                                                                                                                | style    | No       | All        | Yes      |
| verticalOrientation       | 操作按钮应展开的方向。可选值之一：up 或 down                                                                                                                                                                                        | string   | No       | All        | Yes      |
| backgroundTappable        | 使 ActionButton 处于活动状态时背景可点击                                                                                                                                                                                          | boolean  | No       | All        | Yes      |
| activeOpacity             | TouchableOpacity 的 activeOpacity 属性                                                                                                                                                                                                           | number   | No       | All        | Yes      |
| renderIcon                | 用于渲染 ActionButton 图标组件的函数。它会传递一个布尔值 active，当 FAB 展开时为 true，折叠时为 false，允许您在 ActionButton Items 展开时显示不同的图标。 | function | No       | All        | Yes      |
| onPress                   | 当点击 ActionButton 时触发                                                                                                                                                                                                                | function | No       | All        | Yes      |
| useNativeFeedback         | Android：是否使用 TouchableNativeFeedback                                                                                                                                                                                                 | boolean  | No       | Android  | No       |
| fixNativeFeedbackRadius   | Android：激活此选项以修复 TouchableNativeFeedback 的涟漪 UI 问题                                                                                                                                                                          | boolean  | No       | Android  | No       |
| nativeFeedbackRippleColor | Android：为 TouchableNativeFeedback 的涟漪效果传递颜色                                                                                                                                                                           | string   | No       | Android  | No       |

### ActionButton.Item:

| Name                      |  Description                                                                                                                                                                                                                                             | Type     | Required | Platform |  HarmonyOS Support |
| ------------------------- | -------------------------------------------------------------------------- | -------- | -------- |----------| -------- |
| size                      | 用于改变按钮的大小                                  | number   | No       | All      | Yes      |
| buttonColor               | 按钮的背景颜色                                             | string   | No       | All      | Yes      |
| title                     | 按钮旁边显示的标题。当未定义时标题不会被隐藏 | string   | No       | All      | Yes      |
| textStyle                 | 用于设置按钮项文本的文本样式                    | style    | No       | All      | Yes      |
| shadowStyle               | 您想要传递给操作按钮项的自定义阴影样式         | style    | No       | All      | Yes      |
| textContainerStyle        | 用于设置按钮项文本容器的文本样式          | style    | No       | All      | Yes      |
| spaceBetween              | 用于设置按钮和文本容器之间的间距        | number   | No       | All      | Yes      |
| hideLabelShadow           | 用于隐藏按钮标签的默认 elevation 和 boxShadow        | boolean  | No       | All      | Yes      |
| activeOpacity             | TouchableOpacity 的 activeOpacity 属性                                    | number   | No       | All      | Yes      |
| onPress                   | 必需的函数，在点击按钮时触发                        | function | No       | All      | Yes      |
| useNativeFeedback         | Android：是否使用 TouchableNativeFeedback                          | boolean  | No       | Android  | No       |
| fixNativeFeedbackRadius   | Android：激活此选项以修复 TouchableNativeFeedback 的涟漪 UI 问题   | boolean  | No       | Android  | No       |
| nativeFeedbackRippleColor | Android：为 TouchableNativeFeedback 的涟漪效果传递颜色    | string   | No       | Android  | No       |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/mastermoo/react-native-action-button/blob/master/LICENSE) ，请自由地享受和参与开源。
