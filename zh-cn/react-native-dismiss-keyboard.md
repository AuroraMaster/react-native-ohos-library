> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-dismiss-keyboard</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/DanielMSchmidt/react-native-dismiss-keyboard">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/DanielMSchmidt/react-native-dismiss-keyboard/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/DanielMSchmidt/react-native-dismiss-keyboard)

| 三方库版本                 | 支持RN版本                 |
| ------------------------- | -------------------------- |
| 1.0.0                 |  0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：


<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-dismiss-keyboard@1.0.0
```

#### **yarn**

```bash
yarn add react-native-dismiss-keyboard@1.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from 'react';
import {
    AppRegistry,
    StyleSheet,
    TextInput,
    View,
    Text,
    Keyboard
} from 'react-native';

export default class ReactNativeDismissKeyboardExample extends Component {

    keyboardDidShowListener = null;
    keyboardDidHideListener = null;
    state = { KeyboardShown: false };

    constructor(props) {
        super(props);
        this.keyboardDidShowListener = null;
        this.keyboardDidHideListener = null;
        this.state = { KeyboardShown: false };
    }

    //键盘弹出事件响应
    keyboardDidShowHandler(event) {
        this.setState({ KeyboardShown: true });
        console.log(event.endCoordinates.height);
    }

    //键盘隐藏事件响应
    keyboardDidHideHandler(event) {
        this.setState({ KeyboardShown: false });
    }

    //强制隐藏键盘
    dissmissKeyboard() {
        Keyboard.dismiss();
        console.log("输入框当前焦点状态：" + this.refs.bottomInput.isFocused());
    }

    render() {
        return (
            <View style={[styles.container]}>
                <View style={[styles.flexDirection, styles.inputHeight]}>
                    <TextInput style={styles.textInputStyle} ref="bottomInput" />
                    <Text style={styles.buttonStyle}
                        onPress={this.dissmissKeyboard.bind(this)}>
                        收起键盘
                    </Text>
                </View>
            </View>
        )
    }
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        paddingTop: 15,
        backgroundColor: '#ffffff'
    },
    flexDirection: {
        flexDirection: 'row'
    },
    inputHeight: {
        height: 35,
        alignItems: 'center'
    },
    textInputStyle: {
        flex: 1,
        height: 35,
        fontSize: 18,
        borderWidth: 1,
        borderColor: '#4CAF50',
        borderRadius: 8,
        marginRight: 8
    },
    buttonStyle: {
        fontSize: 20,
        color: 'white',
        width: 100,
        textAlign: 'center',
        backgroundColor: '#4CA300'
    },
});
```
## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 电脑ROM。

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1 B.0.18、IDE：DevEco Studio 5.0.3.200; ROM：2.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Prop   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `addListener`  | 注册一个用于监听和处理原生键盘通知事件的 JavaScript 函数。 | function  | no     | All  | yes      |
| `dismiss`  | 收起弹出的键盘，并使当前文本框失去焦点。 | function  |  no     | All   | yes      |
| `scheduleLayoutAnimation`  |用于同步 TextInput（或其他键盘附着视图）尺寸或位置的变化与键盘移动保持一致。| function | no     | All | yes      |
| `isVisible`  | 表示键盘当前是否显示。| bool      |  no     | All   | yes      |
| `metrics`  | 如果软键盘已显示，则返回软键盘的大小。| function      |  no     | All   | yes      |

## 遗留问题

## 其他

## 开源协议
本项目基于 [The MIT License (MIT)](https://github.com/DanielMSchmidt/react-native-dismiss-keyboard/blob/master/LICENSE) ，请自由地享受和参与开源。