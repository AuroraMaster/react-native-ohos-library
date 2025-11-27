> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-qrcode-svg</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/awesomejerry/react-native-qrcode-svg">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/awesomejerry/react-native-qrcode-svg/blob/master/LICENSE">
        <img src="https://img.shields.io/npm/l/react-native-qrcode-svg.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/awesomejerry/react-native-qrcode-svg)

| Version  | Supported RN Version  |
| -----    | -------------------- |
| 6.2.0  |  0.72 |
| 6.3.20 |  0.77 |

## 安装与使用


进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# V6.2.0
npm install react-native-qrcode-svg@6.2.0

# V6.3.20
npm install react-native-qrcode-svg@6.3.20
```

#### **yarn**

```bash
# V6.2.0
yarn add react-native-qrcode-svg@6.2.0

# V6.3.20
yarn add react-native-qrcode-svg@6.3.20
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。
> [!TIP] 当报错信息为`Property 'TextEncoder' doesn't exist`[解决方案](https://github.com/awesomejerry/react-native-qrcode-svg/issues/199)


```js
import {  Text, View } from "react-native";
import QRCode from 'react-native-qrcode-svg';

export const SvgDemo = () => {
    return (
        <View style={{ flex: 1, backgroundColor: '#FFFFFF' }}>
            <QRCode
                size={300}
                value="HelloWorld"
            />
        </View>
    )
}
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg-capi 文档的 Link 章节](/zh-cn/react-native-svg-capi.md)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在下述版本验证通过：

1. RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25;
2. RNOH：0.72.96; SDK：HarmonyOS 5.1.1 Release SDK; IDE：DevEco Studio 5.1.1.840; ROM：6.0.0;
3. RNOH：0.77.18; SDK：HarmonyOS 5.1.1 Release SDK; IDE：DevEco Studio 5.1.1.840; ROM：6.0.0;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                   | Description                                                                                                               | Type     | Required | Platform | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| `size`                 | 渲染图像的尺寸，以像素为单位                                                                                              | number   | No       | iOS,Android      | yes               |
| `value`                | 二维码的字符串值                                                                                                          | string   | yes      | iOS,Android      | yes               |
| `color`                | 二维码的颜色                                                                                                              | string   | No       | iOS,Android      | yes               |
| `backgroundColor`      | 背景颜色                                                                                                                  | string   | No       | iOS,Android      | yes               |
| `enableLinearGradient` | 启用或禁用线性渐变                                                                                                        | boolean  | No       | iOS,Android      | yes                |
| `linearGradient`       | 用于创建线性渐变的2个RGB颜色数组                                                                                          | string[] | No       | iOS,Android      | yes                |
| `gradientDirection`    | 线性渐变的方向                                                                                                            | string   | No       | iOS,Android      | yes                |
| `logo`                 | 图像源对象。例如：{uri: 'base64string'} 或 {require('pathToImage')}                                                       | V6.2.0 : `ImageSourcePropType` <br/> v6.3.20 :  `ImageSourcePropType  \| string`  | No       | iOS,Android      | yes               |
| `logoSize`             | 嵌入logo的尺寸。较大的logo = 二维码中较少的纠错能力                                                                       | number   | No       | iOS,Android      | yes               |
| `logoBackgroundColor`  | logo会获得一个以此颜色填充的正方形背景。如果您的logo已有自己的背景，请使用'transparent'                                    | string   | No       | iOS,Android      | yes               |
| `logoMargin`           | logo与其包装器的距离                                                                                                      | number   | No       | iOS,Android      | yes               |
| `logoBorderRadius`     | logo图像的边框半径（Android不支持）                                                                                       | number   | No       | iOS      | yes                |
| `quietZone`            | 二维码周围的静区（quiet zone），以像素为单位（在保存图像到相册时有用）                                                    | number   | No       | iOS,Android      | yes                |
| `getRef`               | 获取SVG引用以供进一步使用                                                                                                 | callback | No       | iOS,Android      | yes            |
| `ecl`                  | 错误纠正等级                                                                                                              | string   | No       | iOS,Android      | yes               |
| `onError(error)`       | 在代码生成过程中发生异常时触发的回调函数                                                                                  | callback | No       | iOS,Android      | yes            |
| `logoSVG`<sup>6.3.20+</sup> | 作为logo渲染的SVG。可以是svg字符串，也可以是React组件（如果您使用'@svgr/webpack'或类似工具）。如果同时提供了此prop和`logo`，则此prop优先，`logo`将被忽略 | React.FC<SvgProps> \| string | No | All | yes |
| `logoColor`<sup>6.3.20+</sup> | 如果通过`logoSVG` prop提供logo，此颜色将设置为其`fill`属性，否则无效 | string | No | All | yes |
| `testID`<sup>6.3.20+</sup> | 用于测试的testID | string | No | All | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/awesomejerry/react-native-qrcode-svg/blob/master/LICENSE) ，请自由地享受和参与开源。

