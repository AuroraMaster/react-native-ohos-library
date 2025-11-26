> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-signature-canvas</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/YanYuanFE/react-native-signature-canvas">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/YanYuanFE/react-native-signature-canvas/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/YanYuanFE/react-native-signature-canvas)


## 安装与使用

| Version | Post Information                                                      | Supports RN version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 4.7.2      | [https://github.com/YanYuanFE/react-native-signature-canvas Releases](https://github.com/react-native-oh-library/react-native-svg-charts/releases) | 0.72       |
| 5.0.1      | [https://github.com/YanYuanFE/react-native-signature-canvas Releases](https://github.com/react-native-oh-library/react-native-svg-charts/releases) | 0.77   

<!-- tabs:start -->

#### **npm**

```bash
#0.72
npm install --save react-native-signature-canvas@4.7.2

#0.77
npm install --save react-native-signature-canvas@5.0.1
```

#### **yarn**

```bash
#0.72
yarn add react-native-signature-canvas@4.7.2

#0.77
yarn add react-native-signature-canvas@5.0.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { StyleSheet, Text, View, Image } from "react-native";
import Signature from "react-native-signature-canvas";

export const SignatureScreen = () => {
  const [signature, setSign] = useState(null);

  const handleOK = (signature) => {
    console.log(signature);
    setSign(signature);
  };

  const handleEmpty = () => {
    console.log("Empty");
  };

  const style = `.m-signature-pad--footer
    .button {
      background-color: red;
      color: #FFF;
    }`;
  return (
    <View style={{ flex: 1 }}>
      <View style={styles.preview}>
        {signature ? (
          <Image
            resizeMode={"contain"}
            style={{ width: 335, height: 114 }}
            source={{ uri: signature }}
          />
        ) : null}
      </View>
      <Signature
        onOK={handleOK}
        onEmpty={handleEmpty}
        descriptionText="Sign"
        clearText="Clear"
        confirmText="Save"
        webStyle={style}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  preview: {
    width: 335,
    height: 114,
    backgroundColor: "#F8F8F8",
    justifyContent: "center",
    alignItems: "center",
    marginTop: 15,
  },
  previewText: {
    color: "#FFF",
    fontSize: 14,
    height: 40,
    lineHeight: 40,
    paddingLeft: 10,
    paddingRight: 10,
    backgroundColor: "#69B2FF",
    width: 120,
    textAlign: "center",
    marginTop: 10,
  },
});
```
## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-webview的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-webview 文档](/zh-cn/react-native-webview.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.27; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM:3.0.0.25;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

## 属性

### SignatureScreen 

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。



| Name            | Description     | Type                                                                                                                     | Required | Platform | HarmonyOS Support    |
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- |
| autoClear  | 点击确认按钮后应自动清除签名  |boolean| no   | iOS/Android       | yes |
| backgroundColor            | 默认值是 "rgba(255,255,255,0)"（透明），画布的背景颜色 |string| no   | iOS/Android       | yes |
| bgHeight            | 	背景图片的高度  |number| no   | iOS/Android       | yes |
| bgWidth            |背景图像的宽度 |number| no   | iOS/Android       | yes |
| bgSrc            |	背景图像来源 URI（网址） |string| no   | iOS/Android       | yes |
| clearText            |清除按钮文字|string| no   | iOS/Android       | yes |
| confirmText            |保存按钮文字 |string| no   | iOS/Android       | yes |
| customHtml            |允许你修改布局或元素的 HTML 字符串 |(injectedJavaScript: string) => string| no   | iOS/Android       | yes |
| dataURL            |默认值为 ""，Base64 字符串，从 dataURL 中加载已保存的签名。 |string| no   | iOS/Android       | yes |
| descriptionText            |签名的描述文字 |string| no   | iOS/Android       | yes |
| dotSize            |单个点的半径（不是笔触宽度） |number| no   | iOS/Android       | yes |
| imageType            |导出签名的 imageType：“image/png”（默认）、“image/jpeg”、“image/svg+xml”|string| no   | iOS/Android       | yes |
| minWidth            |线条最小宽度。默认值为 0.5 |number| no   | iOS/Android       | yes |
| maxWidth            |行的最大宽度。默认值为2.5 |number| no   | iOS/Android       | yes |
| minDistance<sup>5.0.1+</sup> |只有在前一点距离大于 x 像素时才添加下一点。默认值为 5 |number| no | iOS/Android | yes |
| onError<sup>5.0.1+</sup> |发生错误时的回调函数 |function| no | iOS/Android | no |
| onOK            |保存非空签名后的回调函数|function| no   | iOS/Android       | yes |
| onEmpty            |尝试保存空签名后的回调函数|function| no   | iOS/Android       | yes |
| onClear            |清除签名后的回调函数|function| no   | iOS/Android       | yes |
| onGetData            |当调用 getData() 时的回调函数 |function| no   | iOS/Android       | yes |
| onBegin            |开始新笔画时的回调函数 |function| no   | iOS/Android       | yes |
| onEnd            |当笔画结束时的回调函数 |function| no   | iOS/Android       | yes |
| onLoadEnd            |当 WebView 画布加载完成时的回调函数 |function| no   | iOS/Android       | yes |
| onUndo            |当调用 undo() 时的回调函数 |function| no   | iOS/Android       | yes |
| onRedo	            |当调用 redo() 时的回调函数 |function| no   | iOS/Android       | yes |
| onDraw            |启用绘图时的回调函数 |function| no   | iOS/Android       | yes |
| onErase            |启用擦除时的回调函数 |function| no   | iOS/Android       | yes |
| onChangePenColor            |更改画笔颜色后的回调函数|function| no   | iOS/Android       | yes |
| onChangePenSize            |更改画笔大小后的回调函数 |function| no   | iOS/Android       | yes |
| overlayHeight            |覆盖图像的高度 |number| no   | iOS/Android       | yes |
| overlayWidth            |覆盖图像的宽度 |number| no   | iOS/Android       | yes |
| overlaySrc            |覆盖图像源 URI (url) 必须为带有透明背景的 .png |string| no   | iOS/Android       | yes |
| penColor            |默认是“黑色”，笔的颜色|string| no   | iOS/Android       | yes |
| rotated            |将签名板旋转90度 |boolean| no   | iOS/Android       | yes |
| style            |包装视图样式|object| no   | iOS/Android       | yes |
| scrollable<sup>5.0.1+</sup> |在签名板中启用滚动。默认值为 false|boolean| no | iOS/Android | yes |
| trimWhitespace           |裁剪图片空白|boolean| no   | iOS/Android       | yes |
| webStyle            |用于覆盖默认样式的 webview 样式，所有样式： https://github.com/YanYuanFE/react-native-signature-canvas/blob/master/h5/css/signature-pad.css |string| no   | iOS/Android       | yes |
| androidLayerType            |设置 Android WebView 的 layerType |none、software、hardware| no   | Android       | no |
| androidHardwareAccelerationDisabled           |react-native-webview 的 androidHardwareAccelerationDisabled。默认值为 false |boolean| no   | Android       | no |
| showsVerticalScrollIndicator            |布尔值，用于决定是否在 WebView 中显示垂直滚动条，默认值为 true.|boolean| no   | iOS/Android       | no |
| nestedScrollEnabled            |启用嵌套滚动以便在滚动视图中使用|boolean| no   | no      | no |
| webviewProps<sup>5.0.1+</sup> |要传递给底层 WebView 的额外属性|object| no | iOS/Android | partially |




## 静态方法


> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。



| Name            | Description     | Type                                                                                                                     | Required | Platform | HarmonyOS Support    |
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- |
| clearSignature  |清除当前签名  |function| no   | iOS/Android       | yes |
| changePenColor  |更改笔的颜色 |function| no   | iOS/Android       | yes |
| changePenSize |更改笔的大小  |function| no   | iOS/Android       | yes |
| draw  |启用手写签名  |function| no   | iOS/Android       | yes |
| erase  |启用擦除签名  |function| no   | iOS/Android       | yes |
| getData  |用一个数据 JSON 字符串触发 onGetData 回调  |function| no   | iOS/Android       | yes |
| readSignature  |读取画布上的当前签名，并触发 onOK 或 onEmpty 回调  |function| no   | iOS/Android       | yes |
| undo  |撤销上一步  |function| no   | iOS/Android       | yes |
| redo  |重做上一次笔划 |function| no   | iOS/Android       | yes |
| fromData<sup>5.0.1+</sup> |加载签名数据 |function| no | no | no |



## 遗留问题
- [ ] showsVerticalScrollIndicator属性不生效: [issue#137](https://github.com/react-native-oh-library/react-native-webview/issues/137)

## 其他

 1、nestedScrollEnabled属性在 iOS,Android 不生效，harmonyOS与其表现一致；[issue#363](https://github.com/YanYuanFE/react-native-signature-canvas/issues/363)

 2、fromData方法在 iOS,Android 不生效，harmonyOS与其表现一致；[issue#386](https://github.com/YanYuanFE/react-native-signature-canvas/issues/386)


## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/YanYuanFE/react-native-signature-canvas/blob/master/LICENSE) ，请自由地享受和参与开源。