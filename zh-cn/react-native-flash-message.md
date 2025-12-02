> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-flash-message</code> </h1>
</p>

> [!Tip] [GitHub address](https://github.com/lucasferreira/react-native-flash-message)

请到三方库的 Releases发布地址查看配套的版本信息：

| 三方库版本 | 支持RN版本 |
| ----------| ---------- |
| 0.4.2     |  0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-flash-message@0.4.2
```

#### **yarn**

```bash
yarn add react-native-flash-message@0.4.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
// FlashMessage组件是为全局使用而构建的，因此您必须在主应用程序屏幕中实例化此组件一次，并始终将其作为最后插入的组件
import React from 'react';
import {SafeAreaView, View,} from 'react-native';
import FlashMessage from "react-native-flash-message";
function App() {
  return (
    <View style={{ backgroundColor: 'white' }}>
      <SafeAreaView>
      </SafeAreaView>
      <FlashMessage position="top"/>  
    </View>
  );
}
export default App;

```

```js
import {StyleSheet, Text, View, Image, TouchableOpacity} from 'react-native';
import {showMessage, hideMessage} from 'react-native-flash-message';

export function FlashMessageTest() {
  return (
    <View style={styles.container}>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          showMessage({
            message: 'show message',
            type: 'info',
            onPress: () => {
              hideMessage();
            },
            autoHide: false,
            renderAfterContent: e => {
              return (
                <View>
                  <Text>renderAfterContent</Text>
                </View>
              );
            },
          });
        }}>
        <Text>renderAfterContent</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    justifyContent: 'center',
    alignItems: 'center',
    padding: 10,
    margin: 25,
    borderRadius: 5,
    borderWidth: 3,
  },
  button: {
    padding: 10,
    margin: 5,
    backgroundColor: 'red',
    borderRadius: 5,
  },
});


```
## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 方法

> [!Tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!Tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [react-native-flash-message](https://github.com/lucasferreira/react-native-flash-message/blob/v0.4.0/README.md)

| Name                   | Description | Required | Platform | HarmonyOS Support |
| ---------------------- | ----------- | -------- | ----------------- | ----------------- |
| hideOnPress            | 控制闪存消息是否可以通过按下关闭      | NO        | iOS/Android               | YES               |
| onPress                | 闪存消息按下的onPress回调           | NO        | iOS/Android               | YES               |
| onLongPress            | 闪存消息按下的onLongPress回调           | NO        | iOS/Android               | YES               |
| animated               | 控制闪存消息是否以动画形式显示           | NO        | iOS/Android               | YES               |
| animationDuration      | 动画持续时间/速度           | NO        | iOS/Android               | YES               |
| autoHide               | 控制闪存消息是否可以在一段时间后自动隐藏           | NO        | iOS/Android               | YES               |
| duration               | 如果autoHide为true，闪存消息将显示多少毫秒           | NO        | iOS/Android               | YES               |
| hideStatusBar          | 控制闪存消息是否会自动隐藏原生状态栏。注意：在iOS上工作正常，并非所有Android版本都支持此功能。 | NO | iOS/Android   | YES   |
| statusBarHeight        | 使用此属性设置自定义状态栏高度，该高度将添加到闪存消息的顶部内边距计算中 | NO        | iOS/Android               | YES     |
| floating               | floating属性使消息从边缘分离，并对组件应用一些边框半径  | NO        | iOS/Android               | YES               |
| position               | position属性设置闪存消息的位置。预期选项："top"（默认）、"bottom"、"center"或带有{ top, left, right, bottom }位置的自定义对象           | NO        | iOS/Android               | YES               |
| icon                   | icon属性可以是一个返回新JSX元素以放置在图标位置的渲染函数，或者是闪存消息的图形图标定义。预期选项："none"（默认）、"auto"（由类型引导）、"success"、"info"、"warning"、"danger"、自定义图标（渲染函数）或带有图标类型/名称和位置（左或右）属性的自定义对象，例如：{ icon: "success", position: "right" }           | NO       | iOS/Android               | YES               |
| style                  | 在闪存消息容器中应用自定义样式对象 | NO       | iOS/Android               | YES               |
| textStyle              | 在闪存消息描述/文本标签中应用自定义样式对象   | NO       | iOS/Android               | YES               |
| titleStyle             | 在闪存消息标题文本标签中应用自定义样式对象           | NO       | iOS/Android               | YES               |
| titleProps              | 在闪存消息标题文本标签中设置自定义props对象          | NO       | iOS/Android               | YES               |
| textProps              | 在闪存消息所有文本组件中设置自定义props对象          | NO       | iOS/Android               | YES               |
| iconProps              | 设置自定义props对象以在renderFlashMessageIcon方法中作为第三个参数使用           | NO       | iOS/Android               | YES               |
| renderBeforeContent    | 在闪存消息标题之前渲染自定义JSX。          | NO        | iOS/Android               | YES               |
| renderCustomContent    | 在闪存消息标题下方渲染自定义JSX。           | NO        | iOS/Android               | YES               |
| renderAfterContent     | 在闪存消息的标题（或描述）之后渲染自定义JSX。           | NO        | iOS/Android               | YES               |
| renderFlashMessageIcon | 为内部消息图标设置自定义渲染函数           | NO        | iOS/Android               | YES               |
| transitionConfig       | 设置用于显示/隐藏动画插值的过渡配置函数           | NO        | iOS/Android               | YES               |
| canRegisterAsDefault   | 用于处理实例是否可以注册为默认/全局实例           | NO        | iOS/Android               | YES               |
| MessageComponent       | 设置用于显示所有消息的默认闪存消息渲染组件           | NO       | iOS/Android               | YES               |


## 遗留问题
- [ ] iOS 和 鸿蒙侧效果有差异，隐藏手机状态栏是通过RN框架的StatusBar组件中的StatusBar.setHidden()方法实现,具体效果有差异，暂未解决。原因：鸿蒙系统手机顶部系统非安全区域块范围底部与前置摄像头挖空区域范围底部高度不一致，在显示和隐藏状态栏的过程中，系统非安全区域范围高度会有（0,136（不同手机不同）两种变化），导致内容组件所在窗口大小顶部位置会在两种状态下分别与前置摄像头挖空区域底部或系统非安全区域底部对齐，造成抖动，状态栏的显隐状态和SystemAvoidView这种类型的非安全区域大小不是强关联的。与IOS不一致原因：IOS的顶部没有非安全区域，未做避让。

 
## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/lucasferreira/react-native-flash-message/blob/master/LICENSE) ，请自由地享受和参与开源。
