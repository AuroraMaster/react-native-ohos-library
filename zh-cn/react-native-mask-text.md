> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-mask-text</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/akinncar/react-native-mask-text">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/akinncar/react-native-mask-text/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/akinncar/react-native-mask-text)


请到三方库的 Releases 发布地址查看配套的版本信息：

| Version | RN Version |
| ---------- | ---------- |
| 0.15.0      | 0.72/0.77 |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-mask-text@0.15.0
```

#### **yarn**

```bash
yarn add react-native-mask-text@0.15.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { StyleSheet, Text, View } from "react-native";
import { MaskedTextInput, MaskedText } from "react-native-mask-text";

export default function App() {
	const [maskedValue, setMaskedValue] = useState("");
	const [unMaskedValue, setUnmaskedValue] = useState("");

	const [currencyMaskedValue, setCurrencyMaskedValue] = useState("");
	const [currencyUnMaskedValue, setCurrencyUnmaskedValue] = useState("");

	return (
		<View style={styles.container}>
			<Text style={styles.title}>MaskedTextInput Component:</Text>
			<MaskedTextInput
				mask="AAA-999"
				onChangeText={(text, rawText) => {
					setMaskedValue(text);
					setUnmaskedValue(rawText);
				}}
				style={styles.input}
				keyboardType="numeric"
			/>
			<Text style={styles.paragraph}>Raw Text: {unMaskedValue}</Text>
			<Text style={styles.paragraph}>Masked Text: {maskedValue}</Text>

			<Text style={styles.title}>MaskedTextInput Component with Currency:</Text>
			<MaskedTextInput
				type="currency"
				options={{
					prefix: "$",
					decimalSeparator: ".",
					groupSeparator: ",",
					precision: 2
				}}
				onChangeText={(text, rawText) => {
					setCurrencyMaskedValue(text);
					setCurrencyUnmaskedValue(rawText);
				}}
				style={styles.input}
				keyboardType="numeric"
			/>
			<Text style={styles.paragraph}>Raw Text: {currencyUnMaskedValue}</Text>
			<Text style={styles.paragraph}>Masked Text: {currencyMaskedValue}</Text>

			<Text style={styles.title}>MaskedText Component:</Text>
			<MaskedText mask="99/99/9999" style={styles.paragraph}>
				30081990
			</MaskedText>
		</View>
	);
}

const styles = StyleSheet.create({
	container: {
		flex: 1,
		justifyContent: "center",
		backgroundColor: "#ecf0f1",
		padding: 8
	},
	title: {
		margin: 24,
		fontSize: 24,
		textAlign: "center",
		fontWeight: "bold"
	},
	paragraph: {
		margin: 24,
		fontSize: 18,
		textAlign: "center"
	},
	input: {
		height: 40,
		margin: 12,
		borderWidth: 1
	}
});
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); DevEco Studio  6.0.0.868; ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| 属性名 | 描述 | 类型 | 默认值 | 是否必填 | 支持平台 | HarmonyOS 支持 |
| --- | --- | --- | --- | --- | --- | --- |
| type | 显示类型 | String (enum) `custom`, `date`, `time`,`currency` | custom | 否 | 全平台 | 是 |
| mask | 自定义掩码，控制组件的输入匹配模式 | `9` - 接受数字；`A` - 接受字母；`S` - 接受字母或数字 | null | 否 | 全平台 | 是 |

### Date Mask

These options only are used if you use prop `type="date"` in your component:

| 属性名       | 描述 | 类型   | 默认值    | 是否必填 | 支持平台 | HarmonyOS 支持 |
| ---------- | ----------- | ------ | ---------- | -------- | -------- | ----------------- |
| dateFormat | 日期格式 | string | yyyy/mm/dd | 否       | 全平台      | 是               |

### Time Mask

These options only are used if you use prop `type="time"` in your component:

| 属性名       | 描述 | 类型   | 默认值  | 是否必填 | 支持平台 | HarmonyOS 支持 |
| ---------- | ----------- | ------ | -------- | -------- | -------- | ----------------- |
| timeFormat | 时间格式 | string | HH:mm:ss | 否       | 全平台      | 是               |

### Currency Mask

这些选项仅在您的组件中使用了 `type="currency"` 属性时才会被使用:

| 属性名                   | 描述                                 | 类型   | 默认值 | 是否必填 | 支持平台 | HarmonyOS 支持 |
| ---------------------- | ------------------------------------------- | ------ | ------- | -------- | -------- | ----------------- |
| prefix                 | 需要追加在数值前的前缀字符串                           | string | null    | 否       | 全平台      | 是               |
| decimalSeparator       | 小数部分的分隔符                     | string | null    | 否       | 全平台      | 是               |
| groupSeparator         | 整数部分的分组分隔符      | string | null    | 否       | 全平台      | 是               |
| precision              | 小数部分的精度（小数位数）         | number | 0       | 否       | 全平台      | 是               |
| groupSize              | 整数部分的主分组尺寸   | number | 3       | 否       | 全平台      | 是               |
| secondaryGroupSize     | 整数部分的次级分组尺寸 | number | null    | 否       | 全平台      | 是               |
| fractionGroupSeparator | 小数部分的分组分隔符     | string | null    | 否       | 全平台      | 是               |
| fractionGroupSize      | 小数部分的分组大小          | number | null    | 否       | 全平台      | 是               |
| suffix                 | 需要追加在数值后的后缀字符串                            | string | null    | 否       | 全平台      | 是               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/akinncar/react-native-mask-text/blob/main/LICENSE) ，请自由地享受和参与开源。
