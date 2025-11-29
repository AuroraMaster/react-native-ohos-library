> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-translucent-modal</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/23mf/react-native-translucent-modal">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/23mf/react-native-translucent-modal/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-translucent-modal)

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.1.0      | [@react-native-oh-tpl/react-native-translucent-modalReleases](https://github.com/react-native-oh-library/react-native-translucent-modal/releases) | 0.72       |
| 1.2.0      | [@react-native-ohos/react-native-translucent-modal Releases]() | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-translucent-modal

# 0.77
npm install @react-native-ohos/react-native-translucent-modal
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-translucent-modal

# 0.77
yarn add @react-native-ohos/react-native-translucent-modal
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { View, TouchableWithoutFeedback, Image, Button, StyleSheet } from "react-native-harmony";
// @ts-expect-error
import Modal from "react-native-translucent-modal";

const STYLES = StyleSheet.create({
    wrapper: {
        flex: 1,
    },
    imageBackground: {
        width: 300,
        height: 200,
    }
});

export const E_ReactNativeTranslucentModal: React.FC = (): JSX.Element => {

    const [transparent, setTransparent] = useState(false)
    const [visible, setVisible] = useState(false)
    const [animationType, setAnimationType] = useState('none')

    return <View style={STYLES.wrapper}>
        <Modal transparent={transparent} animationType={animationType}
            visible={visible} onRequestClose={() => setVisible(!visible)}>
            <TouchableWithoutFeedback onPress={() => setVisible(false)}>
             {/* 注意：1、此图片组件为示例，需要根据自己的项目需求，去引入对应组件；
                2、示例图片地址需要根据自己的项目情况去引入 */}
                <Image source={{ uri: "https://hbimg.huabanimg.com/ed258f740ab675e3b3a0b6e7abc44eb7bd832c523396b-cJL1G9_fw658"}} style={STYLES.imageBackground} />
            </TouchableWithoutFeedback>
        </Modal>
        <Button title="显示Modal" onPress={() => setVisible(true)}></Button>
        <Button title="设置transparent为true" onPress={() => setTransparent(true)}></Button>
        <Button title="设置animationType为'slide'" onPress={() => setAnimationType('slide')}></Button>
        <Button title="设置animationType为'fade'" onPress={() => setAnimationType('fade')}></Button>
    </View>;
}

```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

> [!TIP] react-native提供的Modal组件，在HarmonyOS、iOS平台一样可以实现状态栏沉浸式效果。

| Name                          | Description                                         | Type     | Required | Platform | HarmonyOS Support |
| ----------------------------- | --------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| `animationType`               | 模态框的动画类型。                            | string   | No      | All      | yes               |
| `transparent`                 | 模态框背景是否透明。 | boolean  | No      | All      | yes               |
| `visible`                     | 控制模态框是否显示。            | boolean  | No      | All      | yes               |
| `onRequestClose?: () => void` | 当模态框请求关闭时调用。                | function | No      | ALL      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/23mf/react-native-translucent-modal/blob/master/LICENSE.md) ，请自由地享受和参与开源。
