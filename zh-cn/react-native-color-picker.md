> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-color-picker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/instea/react-native-color-picker">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/instea/react-native-color-picker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [Github 地址](https://github.com/instea/react-native-color-picker)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-color-picker@0.6.0
```

#### **yarn**

```bash
yarn add react-native-color-picker@0.6.0
```

<!-- tabs:end -->

### 示例

下面的代码展示了如何在一个页面中使用此颜色选择器组件：

> [!WARNING] 使用时 import 的库名不变。

```javascript
import React from 'react'
import { View, Text, Alert } from 'react-native'
import { TriangleColorPicker, toHsv } from 'react-native-color-picker'

export default class App extends React.Component {

  constructor(...args) {
    super(...args)
    this.state = { color: toHsv('green') }
    this.onColorChange = this.onColorChange.bind(this)
  }

  onColorChange(color) {
    this.setState({ color })
  }

  render() {
    return (
      <View style={{flex: 1, padding: 45, backgroundColor: '#212021'}}>
        <Text style={{color: 'white'}}>React Native Color Picker - Controlled</Text>
        <TriangleColorPicker
          oldColor='purple'
          color={this.state.color}
          onColorChange={this.onColorChange}
          onColorSelected={color => Alert.alert(`Color selected: ${color}`)}
          onOldColorSelected={color => Alert.alert(`Old color selected: ${color}`)}
          style={{flex: 1}}
        />
      </View>
    )
  }

}
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

本文档内容基于以下版本验证通过：

react-native-harmony：0.72.86; SDK：HarmonyOS 5.1.0.125; IDE：DevEco Studio 5.1.0.849; ROM：5.0.0.150;

react-native-harmony：0.77.18; SDK：HarmonyOS 5.1.0.125; IDE：DevEco Studio 5.1.0.849; ROM：5.0.0.150;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 核心属性

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `color` | 受控属性，用于设置选择器的当前颜色。 | `String` \| `HSV` | No | All | yes |
| `defaultColor` | 非受控属性，用于设置选择器的初始颜色。 | `String` \| `HSV` | No | All | yes |
| `oldColor` | 用于视觉比较的旧颜色。如果提供，选择器中心会分块显示新旧颜色。 | `String` | No | All | yes |
| `style` | 应用于选择器根容器的样式。 | `Style` | No | All | yes |
| `hideSliders` | **(仅限 HoloPicker)** 是否隐藏饱和度和明度滑块。默认值：false | `boolean` | No | All | yes |
| `hideControls` | **(仅限 TrianglePicker)** 是否隐藏底部的颜色预览和确认按钮。默认值：false | `boolean` | No | All | yes |
| `sliderComponent`| **(仅限 HoloPicker)** 传入一个自定义的滑块组件。 | `React.Component` | No | All | yes |

### 回调函数

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `onColorChange` | 当颜色发生任何变化时触发的回调。返回 HSV 格式的颜色对象。 | `(color: HSV) => void` | No | All | yes |
| `onColorSelected`| 当用户确认选择颜色时触发（例如点击选择器中心）。返回十六进制颜色字符串。 | `(color: string) => void` | No | All | yes |
| `onOldColorSelected` | 当用户点击旧颜色预览区域时触发。返回旧颜色的十六进制字符串。 | `(color: string) => void` | No | All | yes |

### 工具函数

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `toHsv` | 将颜色字符串（如 `'blue'`, `'#ff0000'`）转换为 HSV 对象。 | `(color: string) => HSV` | No | All | yes |
| `fromHsv`| 将 HSV 对象转换为十六进制颜色字符串。 | `(hsv: HSV) => string` | No | All | yes |

## 遗留问题

## 其他

**HSV 对象格式**:
```javascript
{
  h: number, // 色相: 0-360
  s: number, // 饱和度: 0-1
  v: number, // 透明度: 0-1
}
```

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/instea/react-native-color-picker/blob/master/LICENSE) ，请自由地享受和参与开源。


