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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-credit-card-input)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                      | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.4.1      | [@react-native-oh-tpl/react-native-credit-card-input Releases](https://github.com/react-native-oh-library/react-native-credit-card-input/releases) | 0.72       |
| 1.0.1      | [@react-native-ohos/react-native-credit-card-input Releases]()        | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：


<!-- tabs:start -->

#### **npm**

```bash
# V0.4.1
npm install @react-native-oh-tpl/react-native-credit-card-input

# V1.0.1
npm install @react-native-ohos/react-native-credit-card-input
```

#### **yarn**

```bash
# V0.4.1
yarn add @react-native-oh-tpl/react-native-credit-card-input

# V1.0.1
yarn add @react-native-ohos/react-native-credit-card-input
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

1.RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;

## 属性

>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-credit-card-input](https://github.com/sbycrosz/react-native-credit-card-input)

### LiteCreditCardInput

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| autoFocus  | 	Automatically focus Card Number field on render | PropTypes.bool  | no | Android/iOS      | yes |
| onChange  | Receives a formData object every time the form changes | PropTypes.func  | no | Android/iOS | yes |
| onFocus<sup>deprecated  from 1.0.1</sup>  | 	Receives the name of currently focused field| 	PropTypes.func  | no | Android/iOS | yes |
| placeholders  | Defaults to\{ number: "1234 5678 1234 5678", expiry: "MM/YY", cvc: "CVC" \}  | string | no | Android/iOS | yes |
| inputStyle| Style for credit-card form's textInput | Text.propTypes.style | no | Android/iOS | yes |
| validColor<sup>deprecated  from 1.0.1</sup>  | Color that will be applied for valid text input. Defaults to: "\{inputStyle.color\}" | PropTypes.string | no | Android/iOS | yes |
| invalidColor<sup>deprecated  from 1.0.1</sup>  | Color that will be applied for invalid text input. Defaults to: "red" | PropTypes.string | no | Android/iOS | yes |
| placeholderColor| Color that will be applied for text input placeholder. Defaults to: "gray" | PropTypes.string | no | Android/iOS | yes |
| additionalInputsProps<sup>deprecated from 1.0.1</sup> | An object with Each key of the object corresponding to the name of the field. Allows you to change all props documented in RN TextInput. | PropTypes.objectOf(TextInput.propTypes) | no | Android/iOS | yes |
| onFocusField<sup>1.0.1+</sup>  | Callback function called when a field gains focus. | PropTypes.func | no | Android/iOS | yes |
| style<sup>1.0.1+</sup>  | Custom style for the component's container. | PropTypes.style | no | Android/iOS | yes |

### CreditCardInput

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| autoFocus | Automatically focus Card Number field on render  | 	PropTypes.bool  | no | Android/iOS | yes |
| onChange  | Receives a formData object every time the form changes | PropTypes.func   | no | Android/iOS | yes |
| onFocus<sup>deprecated  from 1.0.1</sup> | Receives the name of currently focused field   | 	PropTypes.func  | no | Android/iOS  | yes |
| labels |	Defaults to\{ number: "CARD NUMBER", expiry: "EXPIRY", cvc: "CVC/CCV" \}| PropTypes.object  | no | Android/iOS | yes |
| placeholders  | Defaults to\{ number: "1234 5678 1234 5678", expiry: "MM/YY", cvc: "CVC" \} | PropTypes.object   | no | Android/iOS | yes |
| cardScale<sup>deprecated  from 1.0.1</sup> | 	Scales the credit-card view.Defaults to 1, which translates to \{ width: 300, height: 190 \}   | PropTypes.number  | no | Android/iOS  | yes |
| cardFontFamily<sup>deprecated  from 1.0.1</sup> | Font family for the CreditCardView, works best with monospace fonts. Defaults to Courier (iOS) or monospace (android)  | PropTypes.string  | no | Android/iOS | yes |
| cardImageFront<sup>deprecated  from 1.0.1</sup>  | Image for the credit-card view e.g. require("./card.png") | PropTypes.number   | no | Android/iOS | yes |
| cardImageBack<sup>deprecated  from 1.0.1</sup> | Image for the credit-card view e.g. require("./card.png")   | PropTypes.number  | no | Android/iOS  | yes |
| labelStyle  | Style for credit-card form's labels | Text.propTypes.style   | no | Android/iOS | yes |
| inputStyle | 	Style for credit-card form's textInput   | Text.propTypes.style  | no | Android/iOS  | yes |
| inputContainerStyle<sup>deprecated  from 1.0.1</sup>  | 	Style for textInput's containerDefaults to: \{ borderBottomWidth: 1, borderBottomColor:"black" \} | ViewPropTypes.style   | no | Android/iOS | yes |
| validColor<sup>deprecated  from 1.0.1</sup> | Color that will be applied for valid text input. Defaults to: "\{inputStyle.color\}"   | PropTypes.string  | no | Android/iOS  | yes |
| invalidColor<sup>deprecated  from 1.0.1</sup> | 	Color that will be applied for invalid text input. Defaults to: "red"   | PropTypes.string  | no | Android/iOS  | yes |
| placeholderColor | Color that will be applied for text input placeholder. Defaults to: "gray"  | PropTypes.string  | no | Android/iOS  | yes |
| requiresName<sup>deprecated  from 1.0.1</sup> | Shows cardholder's name field Default to false  | PropTypes.bool  | no | Android/iOS  | yes |
| requiresCVC<sup>deprecated  from 1.0.1</sup> | Shows CVC field Default to true  | PropTypes.bool | no | Android/iOS  | yes |
| requiresPostalCode<sup>deprecated  from 1.0.1</sup> | 	Shows postalCode field Default to false  | PropTypes.string  | no | Android/iOS  | yes |
| validatePostalCode<sup>deprecated  from 1.0.1</sup> | 	Function to validate postalCode, expects incomplete, valid, or invalid as return values  | PropTypes.func  | no | Android/iOS  | yes |
| allowScroll<sup>deprecated  from 1.0.1</sup> | enables horizontal scrolling on CreditCardInput Defaults to false  | PropTypes.bool | no | Android/iOS  | yes |
| cardBrandIcons<sup>deprecated  from 1.0.1</sup> | 		brand icons for CardView. see ./src/Icons.js for details  | PropTypes.object  | no | Android/iOS  | yes |
| additionalInputsProps<sup>deprecated from 1.0.1</sup> | An object with Each key of the object corresponding to the name of the field. Allows you to change all props documented in RN TextInput.  | PropTypes.objectOf(TextInput.propTypes)  | no | Android/iOS  | yes |
| onFocusField<sup>1.0.1+</sup> | Callback function called when a field gains focus. | PropTypes.func | no | Android/iOS | yes |
| style<sup>1.0.1+</sup> | Custom style for the component's container. | PropTypes.style | no | Android/iOS | yes |

### CreditCardView

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| focused<sup>deprecated  from 1.0.1</sup>  | Determines the front face of the card | PropTypes.string  | no | Android/iOS  | yes |
| brand<sup>deprecated  from 1.0.1</sup> | Brand of the credit card | PropTypes.string  | no | Android/iOS  | yes |
| name  | Cardholder's name (Use empty string if you need to hide the placeholder) | PropTypes.string  | no | Android/iOS  | yes |
| number | Credit card number (you'll need to the formatting yourself) | PropTypes.string  | no | Android/iOS  | yes |
| expiry  | Credit card expiry (should be in MM/YY format) | PropTypes.string  | no | Android/iOS  | yes |
| cvc | Credit card CVC | PropTypes.string  | no | Android/iOS  | yes |
| placeholder  | Placeholder texts | PropTypes.object  | no | Android/iOS  | yes |
| scale<sup>deprecated  from 1.0.1</sup> | Scales the card | PropTypes.number  | no | Android/iOS  | yes |
| fontFamily  | Defaults to Courier and monospace in iOS and Android respectively | PropTypes.string  | no | Android/iOS  | yes |
| imageFront | Image for the credit-card | PropTypes.number | no | Android/iOS  | yes |
| imageBack  | Image for the credit-card | PropTypes.number  | no | Android/iOS  | yes |
| customIcons<sup>deprecated  from 1.0.1</sup> | brand icons for CardView. see ./src/Icons.js for details | PropTypes.object  | no | Android/iOS  | yes |
| focusedField<sup>1.0.1+</sup> | Specifies which field is currently focused | 'name' \| 'number' \| 'expiry' \| | no | Android/iOS | yes |
| type<sup>1.0.1+</sup> | Specifies the type of the credit card issuer | 'visa'  \| 'mastercard' \| 'american-express' \| 'diners-club' \| 'discover' \| 'jcb' | no | Android/iOS | yes |
| style<sup>1.0.1+</sup> | Custom style for the component's container. | PropTypes.style | no | Android/iOS | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/sbycrosz/react-native-credit-card-input/blob/master/LICENSE) ，请自由地享受和参与开源。