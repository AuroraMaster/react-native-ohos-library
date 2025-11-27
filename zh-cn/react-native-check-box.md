> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-check-box</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/crazycodeboy/react-native-check-box">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/crazycodeboy/react-native-check-box/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/crazycodeboy/react-native-check-box)

## 安装与使用

| 三方库版本 | 支持RN版本 |
| :--- | :--- |
| 2.1.7 | 0.72/0.77 |

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-check-box@2.1.7
```
#### **yarn**

```bash
yarn add react-native-check-box@2.1.7
```
<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, {Component} from 'react';
import {StyleSheet, View} from 'react-native';
import CheckBox from 'react-native-check-box'

type Props = {};
export default class CheckBoxDemo extends Component<Props> {
  constructor(props){
    super(props);
    this.state={
      isChecked:true
    }
  }
  render() {
    return (
      <View style={styles.container}>
        <CheckBox
            style={{flex: 1, padding: 10}}
            onClick={()=>{
              this.setState({
                  isChecked:!this.state.isChecked
              })
            }}
            isChecked={this.state.isChecked}
            rightText={"CheckBox"}
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    height:'100%',
    backgroundColor: '#F5FCFF',
  }
});
```

## 兼容性

在以下版本验证通过

1. RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| style | 自定义复选框样式 | ViewPropTypes.style | No | Android、IOS | Yes |
| leftText | 自定义左侧文本 | PropTypes.string | No | Android、IOS | Yes |
| leftTextStyle | 自定义左侧文本样式 | Text.propTypes.style | No | Android、IOS | Yes |
| rightText | 自定义右侧文本 | PropTypes.string | No | Android、IOS | Yes |
| rightTextView | 自定义右侧文本视图 | PropTypes.element | No | Android、IOS | Yes |
| rightTextStyle | 自定义右侧文本样式 | Text.propTypes.style | No | Android、IOS | Yes |
| checkedImage | 自定义选中状态图片 | PropTypes.element | No | Android、IOS | Yes |
| unCheckedImage | 自定义未选中状态图片 | PropTypes.element | No | Android、IOS | Yes |
| isChecked | 复选框选中状态 | PropTypes.bool | Yes | Android、IOS | Yes |
| onClick | 回调函数 | PropTypes.func.isRequired | Yes | Android、IOS | Yes |
| disabled | 禁用复选框按钮 | PropTypes.bool | No | Android、IOS | Yes |
| checkBoxColor | 复选框图片的着色颜色（此属性同时适用于选中和未选中状态） | PropTypes.string | Yes | Android、IOS | Yes |
| checkedCheckBoxColor | 选中状态复选框图片的着色颜色（此属性将覆盖 checked 状态下的 checkBoxColor 值） | PropTypes.string | No | Android、IOS | Yes |
| uncheckedCheckBoxColor | 未选中状态复选框图片的着色颜色（此属性将覆盖 unchecked 状态下的 checkBoxColor 值） | PropTypes.string | No | Android、IOS | Yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/crazycodeboy/react-native-check-box/blob/master/LICENSE) ，请自由地享受和参与开源。