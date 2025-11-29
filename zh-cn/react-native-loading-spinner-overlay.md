> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-loading-spinner-overlay</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ladjs/react-native-loading-spinner-overlay">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ladjs/react-native-loading-spinner-overlay/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/ladjs/react-native-loading-spinner-overlay)

| 三方库版本                 | 支持RN版本                 |
| ------------------------- | -------------------------- |
| 3.0.1               |  0.72/0.77 |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-loading-spinner-overlay@3.0.1
```

#### **yarn**

```bash
yarn add react-native-loading-spinner-overlay@3.0.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from "react";
import { StyleSheet, Text, View } from "react-native";
import Spinner from "react-native-loading-spinner-overlay";

type Props = {};
export default class App extends Component<Props> {
	state = {
		spinner: false
	};

	componentDidMount() {
		setInterval(() => {
			this.setState({
				spinner: !this.state.spinner
			});
		}, 3000);
	}

	render() {
		return (
			<View style={styles.container}>
				<Spinner visible={this.state.spinner} textContent={"Loading..."} textStyle={styles.spinnerTextStyle} />
			</View>
		);
	}
}

const styles = StyleSheet.create({
	spinnerTextStyle: {
		color: "#FFF"
	},
	container: {
		flex: 1,
		justifyContent: "center",
		alignItems: "center",
		backgroundColor: "#F5FCFF"
	}
});
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Default | Required | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- | --- |
| cancelable | 设置为false时，按下返回按钮将阻止spinner隐藏。设置为true时，按下返回按钮将允许spinner隐藏。 | Boolean | `false` | no | Android | yes |
| color | 更改spinner的颜色（例如值有`red`、`#ff0000`等）。要调整对比度，请参见下面的`overlayColor`属性。 | String | `"white"` | no | All | yes |
| animation | 更改显示和隐藏spinner视图时的动画效果。 | String (enum) `none`, `slide`, `fade` | `"none"` | no | All | yes |
| overlayColor | 更改遮罩层的颜色。 | String | `rgba(0, 0, 0, 0.25)` | no | All | yes |
| size | 设置spinner的大小。目前不支持其他跨平台大小。 | String (enum) `small`, `normal`, `large` | `"large"` | no | All | yes |
| textContent | 可选的要显示的文本字段。 | String | `""` | no | All | yes |
| textStyle | 应用于显示`textContent`的`<Text>`的样式。 | StyleSheet | `-` | no | All | yes |
| visible | 控制spinner的可见性。 | Boolean | `false` | yes | All | yes |
| indicatorStyle | [ActivityIndicator](https://facebook.github.io/react-native/docs/activityindicator)继承的额外样式 | StyleSheet | `undefined` | no | All | yes |
| customIndicator | 用于替代默认`<ActivityIndicator />`的自定义组件 | Element | `undefined` | no | All | yes |
| children | 要嵌套在spinner内部的子元素 | Element | `undefined` | no | All | yes |

## 遗留问题

- [ ] 在RNOH框架中引入RN组件`Modal`和`ActivityIndicator`嵌套使用(`ActivityIndicator`作为`Modal`的 children)时会出现`ActivityIndicator`无法正常运作，导致当前库也无法在HarmonyOS中正常运行。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ladjs/react-native-loading-spinner-overlay/blob/master/LICENSE) ，请自由地享受和参与开源。

