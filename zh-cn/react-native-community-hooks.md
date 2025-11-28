> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-community-hooks</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-community/hooks">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-community/hooks/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-community/hooks)

## 安装与使用

| 三方库版本 | 支持RN版本 |
| ---------- | ---------- |
| 3.0.0      | 0.72       |
| 3.1.0      | 0.77       |

进入到工程目录并输入以下命令：

<!-- tabs:start -->

####  npm

```bash
# 0.72
npm install @react-native-community/hooks@3.0.0

# 0.77
npm install @react-native-community/hooks@3.1.0
```


#### yarn

```bash
# 0.72
yarn add @react-native-community/hooks@3.0.0

# 0.77
yarn add @react-native-community/hooks@3.1.0
```


<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```jsx

import React, { useState } from 'react';
import {
    Text,
    View,
    ScrollView,
    StyleSheet,
    RefreshControl
} from 'react-native';

import {  useAppState, useLayout, useKeyboard, useDeviceOrientation, useRefresh, useInteractionManager } from '@react-native-community/hooks'
export const HooksUnTester = () => {
    const [backText, setBackText] = useState('')
    const [refreshText, setRefreshText] = useState('下拉刷新')
    const fetch = () => {
        return new Promise((resolve) => setTimeout(() => { resolve(setRefreshText('刷新成功')) }, 500))
    }
    const { isRefreshing, onRefresh } = useRefresh(fetch);
    return (
        <View style={{ flex: 1 }}>
            <ScrollView refreshControl={
                <RefreshControl
                    refreshing={isRefreshing}
                    onRefresh={onRefresh}
                />
            }>
                {/* hooks-useRefresh-demo */}
                <View style={styles.testSuite}>
                    <Text style={styles.titles}>useRefresh</Text>
                    <View style={styles.textCase}>
                        <Text> {refreshText} </Text>
                    </View>
                </View>
                {/* hooks-useDeviceOrientation-demo */}
                <View style={styles.testSuite}>
                    <Text style={styles.titles}>useDeviceOrientation</Text>
                    <View style={styles.textCase}>
                        <Text>判断是横屏(landscape)还是纵屏(portrait)：{useDeviceOrientation()} </Text>
                    </View>
                </View>
            </ScrollView>
        </View>
    );
}
const styles = StyleSheet.create({
    useBackHandlerBtn: {
        borderRadius: 6,
        height: 36,
        display: 'flex',
        justifyContent: 'center',
        alignItems: 'center',
        margin: 10,
        backgroundColor: 'rgb(61, 176, 236)',
    },
    TextInput: {
        height: 40,
        borderColor: '#fff',
        borderWidth: 1,
        borderRadius: 4,
        width: '90%',
        backgroundColor: '#fff'
    },
    testSuite: { backgroundColor: "#fff", margin: 10 },
    titles: {
        marginLeft: 6,
        fontWeight: '600'
    },
    textCase: {
        margin: 5,
    },
    btnText: { fontWeight: 'bold', color: '#fff', fontSize: 20 },
    container: { flex: 1 },
    ball: {
        width: 100,
        height: 100,
        backgroundColor: "salmon",
        borderRadius: 100,
    },
});


```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1.RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;
2.RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3.RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## API

> [!Tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!Tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name | Description | Type | Required | Platform | HarmonyOS Support |
|---|---|---|---|---|---|
| useAccessibilityInfo | 检查设备的某些配置是否已启用。详见 useAccessibilityInfo Api | Function | False | Android / iOS | Yes |
| useAppState | 告知应用当前是在前台还是后台。 | Function | False | Android / iOS | Yes |
| useBackHandler | 用于监听设备上的返回按钮事件。您可以调用自己的函数来处理返回行为。 | Function | False | Android / iOS | Yes |
| useImageDimensions | 用于监听设备上的返回按钮事件。您可以调用自己的函数来处理返回行为。 | Function | False | Android / iOS | Yes |
| useKeyboard | 返回键盘是否弹出及其宽度和高度。 | Function | False | Android / iOS | Yes |
| useInteractionManager | 在所有交互或动画完成后，安排执行一些较为耗时的任务。 | Function | False | Android / iOS | Yes |
| useDeviceOrientation | 检查设备处于横屏还是竖屏模式。 | Function | False | Android / iOS | Yes |
| useLayout | 返回一个元素的 x 轴和 y 轴坐标，以及其宽度和高度。 | Function | False | Android / iOS | Yes |
| useRefresh | 下拉刷新。 | Function | False | Android / iOS | Yes |


**useAccessibilityInfo 方法返回值**
| Name | Description | Platform | HarmonyOS Support |
|---|---|---|---|
| isBoldTextEnabled | 粗体文本是否已启用。 | iOS | Yes |
| isScreenReaderEnabled | 屏幕阅读功能是否已启用。 | Android / iOS | Yes |
| isGrayscaleEnabled | 灰度模式是否已启用。 | iOS | No |
| isInvertColorsEnabled | 颜色反转是否已启用。 | iOS | No |
| isReduceMotionEnabled | 减弱动态效果（动画）是否已启用。 | Android / iOS | No |
| isReduceTransparencyEnabled | 降低透明度是否已启用。 | iOS | No |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The ISC License (ISC)](https://github.com/react-native-community/hooks/blob/main/LICENSE) ，请自由地享受和参与开源。