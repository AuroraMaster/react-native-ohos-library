> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-confirmation-code-field</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/retyui/react-native-confirmation-code-field">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/retyui/react-native-confirmation-code-field/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/retyui/react-native-confirmation-code-field)

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 支持RN版本 |
| ---------- | ---------- |
| 7.3.2      | 0.72       |
| 8.0.0      | 0.77       |

## 安装与使用

进入到工程目录并输入以下命令：

#### **npm**

```bash
# 0.72
npm install react-native-confirmation-code-field@7.3.2

# 0.77
npm install react-native-confirmation-code-field@8.0.0
```

#### **yarn**

```bash
# 0.72
yarn add react-native-confirmation-code-field@7.3.2

# 0.77
yarn add react-native-confirmation-code-field@8.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { SafeAreaView, Text, StyleSheet } from "react-native";

import {
  CodeField,
  Cursor,
  useBlurOnFulfill,
  useClearByFocusCell,
} from "react-native-confirmation-code-field";

const styles = StyleSheet.create({
  root: { flex: 1, padding: 20 },
  title: { textAlign: "center", fontSize: 30 },
  codeFieldRoot: { marginTop: 20 },
  cell: {
    width: 40,
    height: 40,
    lineHeight: 38,
    fontSize: 24,
    borderWidth: 2,
    borderColor: "#00000030",
    textAlign: "center",
  },
  focusCell: {
    borderColor: "#000",
  },
});

const CELL_COUNT = 6;

const App = () => {
  const [value, setValue] = useState("");
  const ref = useBlurOnFulfill({ value, cellCount: CELL_COUNT });
  const [props, getCellOnLayoutHandler] = useClearByFocusCell({
    value,
    setValue,
  });

  return (
    <SafeAreaView style={styles.root}>
      <Text style={styles.title}>Verification</Text>
      <CodeField
        ref={ref}
        {...props}
        // Use `caretHidden={false}` when users can't paste a text value, because context menu doesn't appear
        value={value}
        onChangeText={setValue}
        cellCount={CELL_COUNT}
        rootStyle={styles.codeFieldRoot}
        keyboardType="number-pad"
        textContentType="oneTimeCode"
        renderCell={({ index, symbol, isFocused }) => (
          <Text
            key={index}
            style={[styles.cell, isFocused && styles.focusCell]}
            onLayout={getCellOnLayoutHandler(index)}
          >
            {symbol || (isFocused ? <Cursor /> : null)}
          </Text>
        )}
      />
    </SafeAreaView>
  );
};

export default App;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该组件在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该组件；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name        | Description                                                                                                                                                                                          | Type      | Platform | HarmonyOS Support |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | -------- | ----------------- |
| `CodeField` | 这是一个基础组件，用于渲染根组件（默认为View），其中包含由renderCell()返回的单元格以及一个不可见且覆盖所有单元格的<TextInput/> | component | All      | yes               |
| `Cursor`    | 这是一个辅助组件，用于在<Cell/>组件中模拟光标闪烁动画                                                                                                               | component | All      | yes               |

## CodeField属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name              | Description                                                                                                                | Type                     | Required | Platform | HarmonyOS Support |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------- | ------------------------ | -------- | -------- | ----------------- |
| `cellCount`       | 输入框中的字符数量（可选，默认值：4）                                                                       | number                   | yes      | All      | yes               |
| `renderCell?`     | 渲染单元格所需的必要函数，将使用以下选项调用：{index: number, symbol: string, isFocused: boolean} | ReactElement             | No       | All      | yes               |
| `RootComponent?`  | 如果您想要更改根组件，例如使用动画 RootComponent={Animated.View}（可选，默认为View）      | ComponentType<any>       | No       | All      | yes               |
| `InputComponent?` | 如果您想要提供一个可以接收相同属性的自定义TextInput组件（可选，默认为TextInput）          | ComponentType<any>       | No       | All      | yes               |
| `rootStyle?`      | 根组件的样式（可选）                                                                                       | StyleProp<RootComponent> | No       | All      | yes               |
| `RootProps?`      | 将应用于根组件的任何属性 <RootComponent style={rootStyle} {...RootProps} />                          | Object                   | No       | All      | yes               |
| `textInputStyle?` | 不可见<TextInput/>的样式，可用于测试或调试（可选）                                             | StyleProp<TextStyle>     | No       | All      | yes               |

## Hooks

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Type           | Required | Platform | HarmonyOS Support |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | -------- | -------- | ----------------- |
| `useClearByFocusCell` | 简单的钩子，添加通过点击单元格修剪值的功能。调用此钩子后将返回包含两个值的数组`[props,getCellOnLayout]`；<br/> -`props`- 应该展开到`<CodeField/>`的对象<br/> - `getCellOnLayout(index: number): Function` - 返回`onLayout`处理程序的辅助方法<br/> - 如果您只需要设置一个边框（例如`borderBottom`），您需要了解React Native中关于[iOS上`<Text/>`边框样式的issue](https://github.com/facebook/react-native/issues/23537)。<br/> - 要解决这个问题，需要为单元格添加`<View/>`包装器，但别忘了将`onLayout={getCellOnLayoutHandler(index)`移动到`<View/>`上 | Function       | yes      | All      | yes               |
| `useBlurOnFulfill`    | 此钩子包含在值填满时使`<TextInput/>`失去焦点的逻辑。您应该传递两个参数：<br/> - `value?: string` - 字符串值；<br/> - `cellCount: number`；<br/>返回值将是应该传递给`<CodeField/>`组件的TextInput引用。当值的长度等于cellCount时，将调用`.blur()`方法。它与`useClearByFocusCell`钩子完美配合工作                                                                                                                                                                                                                                                                        | Ref<TextInput> | yes      | All      | yes               |

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/Kureev/react-native-blur/blob/master/LICENSE) ，请自由地享受和参与开源。
