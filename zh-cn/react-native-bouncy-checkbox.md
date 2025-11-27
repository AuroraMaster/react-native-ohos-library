> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-bouncy-checkbox</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/WrathChaos/react-native-bouncy-checkbox">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/WrathChaos/react-native-bouncy-checkbox/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/WrathChaos/react-native-bouncy-checkbox)

## 安装与使用

| 三方库版本 | 支持RN版本 |
| :--- | :--- |
| 4.0.1 | 0.72 |
| 4.1.2 | 0.77 |

> [!TIP] 需要配套的服务和三方依赖

| Dependencies                         | Version |
| ------------------------------------ | ------- |
| @freakycoder/react-native-bounceable | 1.0.3   |

本库依赖[@freakycoder/react-native-bounceable文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/freakycoder-react-native-bounceable.md)

#### **npm**

```bash
#0.72
npm install --save react-native-bouncy-checkbox@4.0.1
#0.77
npm install --save react-native-bouncy-checkbox@4.1.2
```

#### **yarn**

```bash
#0.72
yarn add react-native-bouncy-checkbox@4.0.1
#0.77
yarn add react-native-bouncy-checkbox@4.1.2
```

下面的代码展示了这个库的基本使用场景：
```js
import React, { useState } from "react";
import { StyleSheet,View,Image } from 'react-native';
import BouncyCheckbox from  "react-native-bouncy-checkbox";

export default function BouncyCheckboxwy () {
  const [checkboxState, setCheckboxState] = React.useState(false);
  return (
  <View style={styles.container}>      
  <BouncyCheckbox
        bounceEffectIn={0.3}
        bounceEffectOut={1}
        bounceVelocityIn={0.5}
        bounceVelocityOut={0.8}
        bouncinessIn={30}
        bouncinessOut={30}
        size={80}
        text="please press me!"
        textStyle={styles.textstyle}
        style={styles.container}
        textContainerStyle={styles.textContainer}
        fillColor={'black'}
        unFillColor={"red"}
        innerIconStyle={{ borderWidth: 5,borderColor:"black"}}
        isChecked={checkboxState}
        iconComponent={
            <Image
              style={{ height: 105, width: 105}}
              source={require("./local-assets/smile.png")}
            />
          }
        onPress={() => setCheckboxState(!checkboxState)}
      />
        </View>
 
  );
};
const styles = StyleSheet.create({
  container: {
    width: '100%',
    height: '100%',
  },
   textContainer:{
    backgroundColor: 'lightblue',
    borderWidth: 5,
    borderColor: 'black',
    padding: 5,
  },
  textstyle: {
    fontSize: 30,
    color: '#010101',
    fontWeight: '600',
    textDecorationLine: "none",
  }
}); 
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证：

1. RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio  5.0.3.404; ROM：5.0.0.31;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| isChecked | 如果你想自行控制选中状态，现在可以使用 `isChecked` 属性！ | boolean | no | All | yes |
| onPress | 设置弹跳效果后的自定义点击功能，如果 disableBuiltInState 为 false，回调会接收下一个 `isChecked` 布尔值。 | function | no | All | yes |
| onLongPress | 设置弹跳效果后的自定义长按功能，如果 disableBuiltInState 为 false，回调会接收下一个 `isChecked` 布尔值。 | function | no | All | yes |
| text | 设置复选框的文本。 | string | no | All | yes |
| textComponent | 通过 React 组件设置复选框的文本。 | component | no | All | yes |
| disableText | 如果你想使用不带文本的复选框，可以启用此项。 | boolean | no | All | yes |
| useBuiltInState<sup>4.1.2+</sup> | 若要完全在外部使用自己的状态控制复选框，只需将其设置为 `false` 并将你的状态值传递给 `isChecked` 属性。 | boolean | no | All | yes |
| size | 复选框 `width`（宽）和 `height`（高）的大小。 | number | no | All | yes |
| style | 设置/覆盖容器样式。 | style | no | All | yes |
| textStyle | 设置/覆盖文本样式。 | style | no | All | yes |
| iconStyle | 设置/覆盖外部图标容器样式。 | style | no | All | yes |
| innerIconStyle | 设置/覆盖内部图标容器样式。 | style | no | All | yes |
| fillColor | 更改复选框的填充颜色。 | color | no | All | yes |
| unfillColor | 更改复选框未被选中时的未填充颜色。 | color | no | All | yes |
| iconComponent | 设置你自己的图标组件。 | component | no | All | yes |
| checkIconImageSource | 设置你自己的选中图标图片。 | image | no | All | yes |
| textContainerStyle | 设置/覆盖文本容器样式。 | ViewStyle | no | All | yes |
| ImageComponent | 设置你自己的 Image 组件来代替 RN 的默认 Image 组件。 | component | no | All | yes |
| TouchableComponent | 使用任何 Touchable 组件（如 Pressable）设置/覆盖主 TouchableOpacity 组件。 | component | no | All | yes |
| bounceEffectIn | 更改按下时的弹跳效果。 | number | no | All | yes |
| bounceEffectOut | 更改松开时的弹跳效果。 | number | no | All | yes |
| bounceVelocityIn | 更改按下时的弹跳速度。 | number | no | All | yes |
| bounceVelocityOut | 更改松开时的弹跳速度。 | number | no | All | yes |
| bouncinessIn | 更改按下时的弹性。 | number | no | All | yes |
| bouncinessOut | 更改松开时的弹性。 | number | no | All | yes |

### 

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/WrathChaos/react-native-bouncy-checkbox/blob/master/LICENSE) ，请自由地享受和参与开源。