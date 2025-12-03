> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-keyboard-aware-scroll-view</code> </h1>
</p>

请到三方库的 Releases 发布地址查看配套的版本信息：

| Version                        | Package Name                             | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -----------
| <= 0.9.5@deprecated | @react-native-oh-tpl/react-native-keyboard-aware-scroll-view  | [Github@deprecated](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view) | [Github Releases@deprecated](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/releases) | 0.72       |
| 0.9.5                        | @react-native-ohos/react-native-keyboard-aware-scroll-view | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-keyboard-aware-scroll-view) | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-keyboard-aware-scroll-view/releases) | 0.72       |
| 0.10.0                        | @react-native-ohos/react-native-keyboard-aware-scroll-view | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-keyboard-aware-scroll-view) | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-keyboard-aware-scroll-view/releases) | 0.77       |

## 安装与使用


进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-keyboard-aware-scroll-view
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-keyboard-aware-scroll-view
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useState, useRef } from "react";
import ReactNative, { TextInput, StyleSheet, Button, View, Text } from "react-native";
import { KeyboardAwareScrollView } from "react-native-keyboard-aware-scroll-view";

const Labels = ['Username', 'Password', 'Firstname', 'Lastname', 'Address', 'Phone', 'Email', 'QQ', 'WeChat', 'Webo'];

export const ReactNativeKeyboardAwareScrollView: React.FC = (): JSX.Element => {

    const [resetScrollToCoords, setResetScrollToCoords] = useState({ x: 20, y: 20 });
    const [enableAutomaticScroll, setEnableAutomaticScroll] = useState(true);
    const [extraHeight, setExtraHeight] = useState(50);
    const [extraScrollHeight, setExtraScrollHeight] = useState(60);
    const [enableResetScrollToCoords, setEnableResetScrollToCoords] = useState(true);

    return <KeyboardAwareScrollView
        style={styles.scroll}
       resetScrollToCoords={resetScrollToCoords}
        enableAutomaticScroll={enableAutomaticScroll}
        extraHeight={extraHeight}
        extraScrollHeight={extraScrollHeight}
        enableResetScrollToCoords={enableResetScrollToCoords}
    >
        {
            Labels.map(item => {
                return <View key={item}>
                    <Text>{item}:</Text>
                    <TextInput style={styles.input} placeholder="请输入" />
                </View>;
            })
        }
    </KeyboardAwareScrollView>;
};

const styles = StyleSheet.create({
    scroll: {
        backgroundColor: '#f0f0f0'
    },
    input: {
        width: 300,
        marginLeft: 20,
        borderWidth: 2,
        borderColor: "black",
        height: 40,
        borderRadius: 10,
        fontSize: 26,
        paddingLeft: 6,
        marginTop: 10,
        marginBottom: 10,
    },
});
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：
1. RNOH：0.72.29; SDK：HarmonyOS NEXT Developer Beta6 SDK; IDE: DevEco Studio 5.0.3.706; ROM：3.0.0.65;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release; IDE: DevEco Studio 6.0.0.858; ROM：6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [react-native-keyboard-aware-scroll-view 源库地址](https://github.com/APSL/react-native-keyboard-aware-scroll-view)

| Name                      | Description                                                                                    | Type                                                                                                                                                             | Required | Platform | HarmonyOS Support |
| ------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| viewIsInsideTabBar        | 添加一个额外的偏移量，代表 `TabBarIOS` 的高度                                           | boolean                                                                                                                                                          | NO       | iOS      | YES                |
| resetScrollToCoords       | 当键盘隐藏时用于重置滚动的坐标                                                               | Object: {x: number, y: number}                                                                                                                                   | NO       | All      | YES               |
| enableAutomaticScroll     | 当焦点在 `TextInput` 中时将滚动位置，默认启用                                           | boolean                                                                                                                                                          | NO       | All      | YES               |
| extraHeight               | 在焦点设置在 `TextInput` 时添加额外偏移                                                   | number                                                                                                                                                           | NO       | All      | YES               |
| extraScrollHeight         | 添加额外偏移到键盘。如果要在键盘上方放置元素很有用                                       | number                                                                                                                                                           | NO       | All      | YES               |
| enableResetScrollToCoords | 让用户启用或禁用自动 resetScrollToCoords                                                   | boolean                                                                                                                                                          | NO       | All      | YES               |
| keyboardOpeningTime       | 设置滚动到新位置之前的延迟时间，默认为 250                                               | number                                                                                                                                                           | NO       | iOS      | YES                |
| onKeyboardWillShow          | 键盘即将出现时执行的操作                                                                   | (event?) => void                                                                                                                                                 | NO       | iOS      | NO                |
| onKeyboardDidShow           | 键盘出现时执行的操作                                                                       | (event?) => void                                                                                                                                                 | NO       | All      | YES               |
| onKeyboardWillHide          | 键盘即将隐藏时执行的操作                                                                   | (event?) => void                                                                                                                                                 | NO       | iOS      | NO                |
| onKeyboardDidHide           | 键盘隐藏时执行的操作                                                                       | (event?) => void                                                                                                                                                 | NO       | All      | YES               |
| onKeyboardWillChangeFrame   | 键盘状态即将更改时执行的操作                                                               | (event?) => void                                                                                                                                                 | NO       | iOS      | NO                |
| onKeyboardDidChangeFrame    | 键盘状态改变时执行的操作                                                                   | (event?) => void                                                                                                                                                 | NO       | iOS      | NO                |
| scrollToPosition          | 滚动到特定位置，可带有或不带动画                                                           | (x: number, y: number, animated: bool = true) => void                                                                                                            | NO       | All      | YES               |
| scrollToEnd               | 滚动到末尾，可带有或不带动画                                                               | (animated?: bool = true) => void                                                                                                                                 | NO       | All      | YES               |
| scrollIntoView            | 将 KeyboardAwareScrollView 内的元素滚动到视图中                                            | (element: React.Element<\*>, options: { getScrollPosition: ?(parentLayout, childLayout, contentOffset) => { x: number, y: number, animated: boolean } }) => void | NO       | All      | YES                |

## 遗留问题

- [ ] RN0.72.28版本新架构暂未支持UIManager.viewIsDescendantOf() API，该API功能为：判断组件节点嵌套关系，并在callback中返回boolean类型参数: [issue#12](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/issues/12)
- [ ] 键盘抬起部分生命周期未HarmonyOS化，功能不受影响 问题:[issue#17](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/issues/17)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/APSL/react-native-keyboard-aware-scroll-view/blob/master/LICENSE) ，请自由地享受和参与开源。
