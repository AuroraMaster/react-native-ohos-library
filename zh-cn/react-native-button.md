> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-button</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ide/react-native-button">       
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ide/react-native-button/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/ide/react-native-button)

| 三方库版本                 | 支持RN版本                 |
| ------------------------- | -------------------------- |
| 3.1.0               |  0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-button@3.1.0 --save
```

#### **yarn**

```bash
yarn add react-native-button@3.1.0 --save
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 * @flow
 */

import React, { Component } from 'react';
import Button from 'react-native-button';
import {
    View, Text
} from 'react-native';

export default class ExampleComponent extends Component {
    constructor(props, context) {
        super(props, context);
        this.state = {
            isDisabled: false
        }
    }
    _handlePress() {
        this.setState({
            isDisabled: true
        });
        console.log('Now, button disabled');
    }
    render() {
        const { isDisabled } = this.state;
        return (
            <View style={{ marginTop: 50 }}>
                <Button
                    allowFontScaling={false}
                    accessibilityLabel="Learn more about this purple button"
                    style={{ fontSize: 20, color: 'yellow' }}
                    styleDisabled={{ color: 'white' }}
                    disabled={isDisabled}
                    containerStyle={{ padding: 10, height: 45, overflow: 'hidden', borderRadius: 4, backgroundColor: 'aqua' }}
                    disabledContainerStyle={{ backgroundColor: 'pink' }}
                    onPress={() => this._handlePress()}>
                    Hello World
                </Button>
            </View>
        );
    }
};
```



## 约束与限制

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.77.17; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description                                                                                            | Type     | default | Required | Platform | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- | ----------------- |
| `accessibilityLabel` | 当用户选择相关元素时，VoiceOver将读取此字符串 | String |  | No     | All      | yes               |
| `allowFontScaling` | 指定字体是否应缩放以遵循文本大小无障碍设置 | Bool |  | No     | All      | yes               |
| `Disabled` | 禁用按钮                | Bool | false   | No       | All      | yes               |
| `Style` | 按钮的样式                                       | View Style Prop | ｛｝ | No       | All      | yes               |
| `styleDisabled` | 禁用状态下按钮的样式 | View Style Prop | ｛｝ | No       | All      | yes               |
| `containerStyle` | 容器的样式 | View Style Prop | ｛｝ | No       | All      | yes               |
| `disabledContainerStyle` | 按钮禁用状态下容器的样式 | View Style Prop | ｛｝ | No       | All      | yes               |
| `childGroupStyle` | 子视图的样式               | View Style Prop | ｛｝ | No       | All      | yes               |
| `androidBackground` | 安卓设备的背景                      | Background Prop Type |  | No       | Android | no             |
| `onPress`   | 用户点击按钮时要调用的处理函数 |         | No       | All      | yes              |

## 遗留问题

-[ ] allowFontScaling属性无效，文本字体不跟随系统字体的修改而变化。[issue#99](https://github.com/ide/react-native-button/issues/99)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ide/react-native-button/blob/main/LICENSE) ，请自由地享受和参与开源。
