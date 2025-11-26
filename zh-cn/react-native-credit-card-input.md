> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-credit-card-input</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/sbycrosz/react-native-credit-card-input">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/sbycrosz/react-native-credit-card-input/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

本项目基于 [react-native-credit-card-input](https://github.com/sbycrosz/react-native-credit-card-input).

请访问第三方库的 Release 发布地址查看对应的版本信息：

| Version                   | Package Name                                      | Repository         | Release                    |Support RN version|
| ------------------------- | ------------------------------------------------- | ------------------ | -------------------------- |-------------------|
| 0.4.1  | @react-native-oh-tpl/react-native-credit-card-input | [Github](https://github.com/react-native-oh-library/react-native-credit-card-input) | [Github Releases](https://github.com/react-native-oh-library/react-native-credit-card-input/releases) |0.72       |
| 1.0.1     | @react-native-ohos/react-native-credit-card-input   | [Github](https://github.com/react-native-oh-library/react-native-credit-card-input/tree/br_rnoh0.77) | [Github Releases](https://github.com/react-native-oh-library/react-native-credit-card-input/tree/br_rnoh0.77) |0.77       |


## 安装与使用

进入到工程目录并输入以下命令：

#### **npm**

```bash

# 0.72
npm install @react-native-oh-tpl/react-native-credit-card-input

# 0.77
npm install @react-native-ohos/react-native-credit-card-input
```

#### **yarn**

```bash
# 0.72
yarn install @react-native-oh-tpl/react-native-credit-card-input

# 0.77
yarn install @react-native-ohos/react-native-credit-card-input
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React from "react";
import { StyleSheet, View, Switch, SafeAreaView } from 'react-native';
import { CreditCardInput, LiteCreditCardInput } from 'react-native-credit-card-input';

export default function App() {
  const [useLiteCreditCardInput, setUseLiteCreditCardInput] = React.useState(true);
  const _setUseLiteCreditCardInput = (value) => {
    setUseLiteCreditCardInput(value);
  };

  return (
    <SafeAreaView style={{ flex: 1 }}>
      <View style={style.container}>
        <Switch
          style={style.switch}
          onValueChange={_setUseLiteCreditCardInput}
          value={useLiteCreditCardInput} />

        {useLiteCreditCardInput ? (
          <LiteCreditCardInput
            style={style.style}
            inputStyle={style.input}
            placeholderColor={"pink"}
          />
        ) : (
          <CreditCardInput
            style={style.style}
            labelStyle={style.label}
            inputStyle={style.input}
            placeholderColor={"pink"}
          />
        )}
      </View>
    </SafeAreaView>
  );
}

const style = StyleSheet.create({
  switch: {
    alignSelf: "center",
    marginTop: 20,
    marginBottom: 20,
  },
  container: {
    backgroundColor: "#F5F5F5",
    marginTop: 60,
    flex: 1,
  },
  label: {
    color: "black",
    fontSize: 12,
  },
  input: {
    fontSize: 16,
    color: "black",
  },
  style: {
    backgroundColor: "#f0f0f0",
  },
});

```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS 5.1.1 Release SDK; IDE: DevEco Studio 5.1.1 Release; ROM: 5.0.1.120;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 属性

>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-credit-card-input](https://github.com/sbycrosz/react-native-credit-card-input)

### LiteCreditCardInput

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| autoFocus  | 渲染时自动聚焦卡号输入框 | PropTypes.bool  | no | Android/iOS      | yes |
| onChange  | 每次表单变化时接收一个 formData 对象 | PropTypes.func  | no | Android/iOS | yes |
| onFocus<sup>deprecated  from 1.0.1</sup>  | 接收当前聚焦字段的名称 | 	PropTypes.func  | no | Android/iOS | yes |
| placeholders  | 默认为 {number: "1234 5678 1234 5678", expiry: "MM/YY", cvc: "CVC"} | string | no | Android/iOS | yes |
| inputStyle| 信用卡表单文本输入框的样式 | Text.propTypes.style | no | Android/iOS | yes |
| validColor<sup>deprecated  from 1.0.1</sup>  | 应用于有效文本输入的颜色。默认为："{inputStyle.color}" | PropTypes.string | no | Android/iOS | yes |
| invalidColor<sup>deprecated  from 1.0.1</sup>  | 应用于无效文本输入的颜色。默认为："red" | PropTypes.string | no | Android/iOS | yes |
| placeholderColor| 应用于文本输入框占位符的颜色。默认为："gray" | PropTypes.string | no | Android/iOS | yes |
| additionalInputsProps<sup>deprecated from 1.0.1</sup> | 一个对象，该对象的每个键对应字段的名称。允许你更改 RN TextInput 中记录的所有属性。 | PropTypes.objectOf(TextInput.propTypes) | no | Android/iOS | yes |
| onFocusField<sup>1.0.1+</sup>  | 当字段获得焦点时调用的回调函数。 | PropTypes.func | no | Android/iOS | yes |
| style<sup>1.0.1+</sup>  | 组件容器的自定义样式。 | PropTypes.style | no | Android/iOS | yes |

### CreditCardInput

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| autoFocus | 渲染时自动聚焦卡号输入框 | 	PropTypes.bool  | no | Android/iOS | yes |
| onChange  | 每次表单变化时接收一个 formData 对象 | PropTypes.func   | no | Android/iOS | yes |
| onFocus<sup>deprecated  from 1.0.1</sup> | 接收当前聚焦字段的名称 | 	PropTypes.func  | no | Android/iOS  | yes |
| labels | 默认为 {number: "CARD NUMBER", expiry: "EXPIRY", cvc: "CVC/CCV"} | PropTypes.object  | no | Android/iOS | yes |
| placeholders  | 默认为 {number: "1234 5678 1234 5678", expiry: "MM/YY", cvc: "CVC"} | PropTypes.object   | no | Android/iOS | yes |
| cardScale<sup>deprecated  from 1.0.1</sup> | 缩放信用卡视图。默认为 1，对应 {width: 300, height: 190} | PropTypes.number  | no | Android/iOS  | yes |
| cardFontFamily<sup>deprecated  from 1.0.1</sup> | 信用卡视图的字体系列，使用等宽字体效果最佳。默认为 Courier（iOS）或 monospace（android） | PropTypes.string  | no | Android/iOS | yes |
| cardImageFront<sup>deprecated  from 1.0.1</sup>  | 信用卡视图的正面图片，例如 require ("./card.png") | PropTypes.number   | no | Android/iOS | yes |
| cardImageBack<sup>deprecated  from 1.0.1</sup> | 信用卡视图的背面图片，例如 require ("./card.png") | PropTypes.number  | no | Android/iOS  | yes |
| labelStyle  | 信用卡表单标签的样式 | Text.propTypes.style   | no | Android/iOS | yes |
| inputStyle | 信用卡表单文本输入框的样式 | Text.propTypes.style  | no | Android/iOS  | yes |
| inputContainerStyle<sup>deprecated  from 1.0.1</sup>  | 文本输入框容器的样式，默认为：{borderBottomWidth: 1, borderBottomColor:"black"} | ViewPropTypes.style   | no | Android/iOS | yes |
| validColor<sup>deprecated  from 1.0.1</sup> | 应用于有效文本输入的颜色。默认为："{inputStyle.color}" | PropTypes.string  | no | Android/iOS  | yes |
| invalidColor<sup>deprecated  from 1.0.1</sup> | 应用于无效文本输入的颜色。默认为："red" | PropTypes.string  | no | Android/iOS  | yes |
| placeholderColor | 应用于文本输入框占位符的颜色。默认为："gray" | PropTypes.string  | no | Android/iOS  | yes |
| requiresName<sup>deprecated  from 1.0.1</sup> | 显示持卡人姓名字段，默认为 false | PropTypes.bool  | no | Android/iOS  | yes |
| requiresCVC<sup>deprecated  from 1.0.1</sup> | 显示 CVC 字段，默认为 true | PropTypes.bool | no | Android/iOS  | yes |
| requiresPostalCode<sup>deprecated  from 1.0.1</sup> | 	显示邮政编码字段，默认为 false  | PropTypes.string  | no | Android/iOS  | yes |
| validatePostalCode<sup>deprecated  from 1.0.1</sup> | 	验证邮政编码的函数，期望返回 incomplete、valid 或 invalid  | PropTypes.func  | no | Android/iOS  | yes |
| allowScroll<sup>deprecated  from 1.0.1</sup> | 启用 CreditCardInput 上的水平滚动，默认为 false | PropTypes.bool | no | Android/iOS  | yes |
| cardBrandIcons<sup>deprecated  from 1.0.1</sup> | 卡片视图的品牌图标。详见./src/Icons.js  | PropTypes.object  | no | Android/iOS  | yes |
| additionalInputsProps<sup>deprecated from 1.0.1</sup> | 一个对象，该对象的每个键对应字段的名称。允许你更改 RN TextInput 中记录的所有属性。 | PropTypes.objectOf(TextInput.propTypes)  | no | Android/iOS  | yes |
| onFocusField<sup>1.0.1+</sup> | 当字段获得焦点时调用的回调函数。 | PropTypes.func | no | Android/iOS | yes |
| style<sup>1.0.1+</sup> | 组件容器的自定义样式。 | PropTypes.style | no | Android/iOS | yes |

### CreditCardView

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| focused<sup>deprecated  from 1.0.1</sup>  | 确定卡片的正面 | PropTypes.string  | no | Android/iOS  | yes |
| brand<sup>deprecated  from 1.0.1</sup> | 信用卡的品牌 | PropTypes.string  | no | Android/iOS  | yes |
| name  | 持卡人姓名（如果需要隐藏占位符，请使用空字符串） | PropTypes.string  | no | Android/iOS  | yes |
| number | 信用卡号码（你需要自己进行格式化） | PropTypes.string  | no | Android/iOS  | yes |
| expiry  | 信用卡有效期（应为 MM/YY 格式） | PropTypes.string  | no | Android/iOS  | yes |
| cvc | 信用卡 CVC 码 | PropTypes.string  | no | Android/iOS  | yes |
| placeholder  | 占位符文本 | PropTypes.object  | no | Android/iOS  | yes |
| scale<sup>deprecated  from 1.0.1</sup> | 缩放卡片 | PropTypes.number  | no | Android/iOS  | yes |
| fontFamily  | 默认为 iOS 中的 Courier 和 Android 中的 monospace | PropTypes.string  | no | Android/iOS  | yes |
| imageFront | 信用卡正面图片 | PropTypes.number | no | Android/iOS  | yes |
| imageBack  | 信用卡背面图片 | PropTypes.number  | no | Android/iOS  | yes |
| customIcons<sup>deprecated  from 1.0.1</sup> | 卡片视图的品牌图标。详见./src/Icons.js | PropTypes.object  | no | Android/iOS  | yes |
| focusedField<sup>1.0.1+</sup> | 指定当前聚焦的字段 | 'name' \| 'number' \| 'expiry' \| | no | Android/iOS | yes |
| type<sup>1.0.1+</sup> | 指定信用卡发卡机构的类型 | 'visa'  \| 'mastercard' \| 'american-express' \| 'diners-club' \| 'discover' \| 'jcb' | no | Android/iOS | yes |
| style<sup>1.0.1+</sup> | 组件容器的自定义样式。 | PropTypes.style | no | Android/iOS | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/sbycrosz/react-native-credit-card-input/blob/master/LICENSE) ，请自由地享受和参与开源。