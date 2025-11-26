> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/awesomejerry/react-native-qrcode-svg)

| Version  | Supported RN Version  |
| -----    | -------------------- |
| 6.2.0  |  0.72 |
| 6.3.20 |  0.77 |

## Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

> [!TIP] If the error message `Property 'TextEncoder' doesn't exist` is displayed. [solution](https://github.com/awesomejerry/react-native-qrcode-svg/issues/199)


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

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-svg. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-svg-capi](/en/react-native-svg-capi.md) to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH:0.72.27; SDK:HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE:DevEco Studio 5.0.3.400; ROM:3.0.0.25;
2. RNOH:0.72.96; SDK:HarmonyOS 5.1.1 Release SDK; IDE:DevEco Studio 5.1.1.840; ROM:6.0.0;
3. RNOH:0.77.18; SDK:HarmonyOS 5.1.1 Release SDK; IDE:DevEco Studio 5.1.1.840; ROM:6.0.0;


## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                   | Description                                                                                                               | Type     | Required | Platform | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| `size`                 | Size of rendered image in pixels                                                                                          | number   | No       | iOS,Android      | yes               |
| `value`                | String Value of the QR code                                                                                               | string   | yes      | iOS,Android      | yes               |
| `color`                | Color of the QR code                                                                                                      | string   | No       | iOS,Android      | yes               |
| `backgroundColor`      | Color of the background                                                                                                   | string   | No       | iOS,Android      | yes               |
| `enableLinearGradient` | enables or disables linear gradient                                                                                       | boolean  | No       | iOS,Android      | yes                |
| `linearGradient`       | array of 2 rgb colors used to create the linear gradient                                                                  | string[] | No       | iOS,Android      | yes                |
| `gradientDirection`    | the direction of the linear gradient                                                                                      | string   | No       | iOS,Android      | yes                |
| `logo`                 | Image source object. Ex. {uri: 'base64string'} or {require('pathToImage')}                                                | V6.2.0 : `ImageSourcePropType` <br/> v6.3.20 :  `ImageSourcePropType  \| string`  | No       | iOS,Android      | yes               |
| `logoSize`             | Size of the imprinted logo. Bigger logo = less error correction in QR code                                                | number   | No       | iOS,Android      | yes               |
| `logoBackgroundColor`  | The logo gets a filled quadratic background with this color. Use 'transparent' if your logo already has its own backdrop. | string   | No       | iOS,Android      | yes               |
| `logoMargin`           | logo's distance to its wrapper                                                                                            | number   | No       | iOS,Android      | yes               |
| `logoBorderRadius`     | the border-radius of logo image (Android is not supported)                                                                | number   | No       | iOS      | yes                |
| `quietZone`            | quiet zone around the qr in pixels (useful when saving image to gallery)                                                  | number   | No       | iOS,Android      | yes                |
| `getRef`               | Get SVG ref for further usage                                                                                             | callback | No       | iOS,Android      | yes            |
| `ecl`                  | Error correction level                                                                                                    | string   | No       | iOS,Android      | yes               |
| `onError(error)`       | Callback fired when exception happened during the code generating process                                                 | callback | No       | iOS,Android      | yes            |
| `logoSVG`<sup>6.3.20+</sup> | SVG to  render as logo. Can be either a svg string or a React component if you're  using ex: '@svgr/webpack' or similar. In case both this prop and `logo` are  provided, then this prop takes precedence and `logo` will be ignored. | React.FC<SvgProps> \| string | No | All | yes |
| `logoColor`<sup>6.3.20+</sup> | If the  logo is provided via `logoSVG` prop, this color will be set as it's `fill`  property, otherwise it does nothing | string | No | All | yes |
| `testID`<sup>6.3.20+</sup> | testID  for testing | string | No | All | yes |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/awesomejerry/react-native-qrcode-svg/blob/master/LICENSE).
