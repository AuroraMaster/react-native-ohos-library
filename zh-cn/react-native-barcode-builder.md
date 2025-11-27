> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-barcode-builder</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wonsikin/react-native-barcode-builder">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/wonsikin/react-native-barcode-builder/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-barcode-builder)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN0.77 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.0.0      | [@react-native-oh-tpl/react-native-barcode-builder](https://github.com/react-native-oh-library/react-native-barcode-builder/releases) | 0.72       |
| 2.1.0      | [@react-native-ohos/react-native-barcode-builder](https://gitcode.com/openharmony-sig/rntpc_react-native-barcode-builder)          | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-barcode-builder

# 0.77
npm install @react-native-ohos/react-native-barcode-builder
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-barcode-builder

# 0.77
yarn add @react-native-ohos/react-native-barcode-builder
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useEffect } from "react";
import { StyleSheet, View, Text } from "react-native";
import Barcode from "react-native-barcode-builder";
import { Colors } from "react-native/Libraries/NewAppScreen";
export const BarcodeBuilderExample = () => {
  const error = (e) => {
    console.log(e, "click");
  };
  return (
    <View
      style={{
        flex: 1,
        justifyContent: "center",
        alignItems: "center",
        backgroundColor: "#F5FCFF",
      }}
    >
      <Text style={{ fontSize: 50 }}>This is a Barcode Builder</Text>
      <Barcode
        value=" hello~~~"
        format="CODE128"
        text="hello world"
        onError={error}
        width={5}
        height={200}
      />
    </View>
  );
};
```

## Link

本库鸿蒙侧实现依赖 react-native-svg 的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[react-native-svg 文档](/zh-cn/react-native-svg-capi.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.86; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## 属性

### Barcode

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

该库为 UI 组件库，通过配置属性标签，实现对应的功能。

| Name | Type | Description | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| value | string | 条形码所代表的值。 | yes | iOS/Android | yes |
| format | string | 使用哪种条形码类型。[了解更多](https://github.com/lindell/JsBarcode#supported-barcodes) | no | iOS/Android | yes |
| width | number | 单个条的宽度。 | no | iOS/Android | yes |
| height | number | 条形码的高度。 | no | iOS/Android | yes |
| text | string | 覆盖显示的文本。 | no | iOS/Android | yes |
| lineColor | string | 条纹的颜色。 | no | iOS/Android | yes |
| textColor | string | 文本的颜色。 | no | iOS/Android | yes |
| background | string | 条形码的背景颜色。 | no | iOS/Android | yes |
| onError | function | 当所选格式的条形码无效时的回调函数。 | no | iOS/Android | yes |

## 开源协议

本项目基于 [The Apache License (Apache)](https://github.com/wonsikin/react-native-barcode-builder/blob/master/LICENSE) ，请自由地享受和参与开源。