> Template version: v0.2.2

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

> [!TIP] [ GitHub address](https://github.com/react-native-oh-library/react-native-barcode-builder)

## Installation and Usage

Please refer to the Releases page of the third-party library for corresponding version information:

| Library Version | Release Information | Supported RN Version |
| :--- | :--- | :--- |
| 2.0.0 | [@react-native-oh-tpl/react-native-barcode-builder](https://github.com/react-native-oh-library/react-native-barcode-builder/releases) | 0.72 |
| 2.1.0 | [@react-native-ohos/react-native-barcode-builder](https://gitcode.com/openharmony-sig/rntpc_react-native-barcode-builder) | 0.77 |

Go to the project directory and execute the following instruction:

For older versions not published to npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.


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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

The HarmonyOS implementation of this library depends on the native code from react-native-svg. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [react-native-svg docs](/en/react-native-svg-capi.md) to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:
1. RNOH：0.72.86; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;


## Properties

### Barcode

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

This library is a UI component library that achieves corresponding functions by configuring the Properties tag.

| Name       | Type     | Description                                                                                      | Required | Platform    | HarmonyOS Support |
| ---------- | -------- | ------------------------------------------------------------------------------------------------ | -------- | ----------- | ----------------- |
| value      | string   | What the barcode stands for.                                                                     | yes      | iOS/Android | yes               |
| format     | string   | Which barcode type to use. [learn more](https://github.com/lindell/JsBarcode#supported-barcodes) | no       | iOS/Android | yes               |
| width      | number   | Width of a single bar.                                                                           | no       | iOS/Android | yes               |
| height     | number   | Height of the barcode.                                                                           | no       | iOS/Android | yes               |
| text       | string   | Override text that is displayed.                                                                 | no       | iOS/Android | yes               |
| lineColor  | string   | Color of the bars.                                                                               | no       | iOS/Android | yes               |
| textColor  | string   | Color of the text.                                                                               | no       | iOS/Android | yes               |
| background | string   | Background color of the barcode.                                                                 | no       | iOS/Android | yes               |
| onError    | function | Handler for invalid barcode of selected format.                                                  | no       | iOS/Android | yes               |

## License

This project is licensed under [The Apache License (Apache)](https://github.com/wonsikin/react-native-barcode-builder/blob/master/LICENSE).
