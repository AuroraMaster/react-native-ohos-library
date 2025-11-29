> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-switch-pro</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/poberwong/react-native-switch-pro">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/poberwong/react-native-switch-pro/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-switch-pro)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：
| version | Package Name                                       |Repository | Release               |  RN version |
| ---------- | ------------------------------------------------------------ | -------|--------|---------- |
| 1.0.5     | @react-native-oh-tpl/react-native-switch-pro | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-switch-pro)  | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-switch-pro/releases)|0.72       |
| 1.1.0    | @react-native-ohos/react-native-switch-pro  |[Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-switch-pro)  | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-switch-pro/releases)| 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
#0.72
npm install @react-native-oh-tpl/react-native-switch-pro

#0.77
npm install @react-native-ohos/react-native-switch-pro
```

#### **yarn**

```bash
#0.72
yarn add @react-native-oh-tpl/react-native-switch-pro

#0.77
yarn add @react-native-ohos/react-native-switch-pro
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import Switch from 'react-native-switch-pro'
...
  render() {
    return (
      <View style={styles.container}>
        <Switch onSyncPress={value => {...}}/>
      </View>
    )
  }
...

```
## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.0.5      | [@react-native-oh-tpl/react-native-switch-pro Releases](https://github.com/react-native-oh-library/react-native-switch-pro/releases) | 0.72       |
| 1.1.0     | [@react-native-ohos/react-native-switch-pro Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-switch-pro) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.23; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio: 5.0.3.27; ROM: 3.0.0.19;
2. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| width| 开关宽度  | number  | no | Android/IOS      | yes              |
| height  | 开关高度         | number  | no | Android/IOS      | yes                |
| value  | 支持双向绑定的开关状态 | bool  | no | Android/IOS      | yes |
| disabled  | 开关是否可点击 | bool  | no | Android/IOS      | yes |
| circleColorActive  | 开关开启状态下圆形控制柄的颜色 | string  | no | Android/IOS      | yes |
| circleColorInactive  | 开关关闭状态下圆形控制柄的颜色 | string  | no | Android/IOS      | yes |
| style  | styles that will be applied for switch container | style  | no | Android/IOS      | yes |
| circleStyle  | 将应用于开关容器的样式 | style  | no | Android/IOS      | yes |
| backgroundActive  | 开关开启时的颜色 | string  | no | Android/IOS      | yes |
| backgroundInactive  | 开关关闭时的颜色 | string  | no | Android/IOS      | yes |
| onSyncPress  | 点击开关时的回调 | func  | no | Android/IOS      | yes |
| onAsyncPress | 有一个回调结果为async | func  | no | Android/IOS      | yes | 


## 注意
* 最好不要同时使用 onSyncPress 和 onAsyncPress，否则只会调用 onSyncPress。

* value 与双向绑定一起使用，可以是 redux、state 等。
在 onAsyncPress 中，您应该写如下（带有状态）：

	```javascript
	<Switch
	  value={this.state.value}
	  onAsyncPress={(callback) => {
	    callback(false or true, value => this.setState({value}))
     }}
	/>
	```
	`value => this.setState({value})仅当 result 为 true 时才会调用。

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/poberwong/react-native-switch-pro/blob/master/LICENSE) ，请自由地享受和参与开源。