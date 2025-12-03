> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-htmlview</code> </h1>
</p>

> [!TIP] [GitHub address](https://github.com/jsdf/react-native-htmlview)

Please check the corresponding version information in the Releases section of the third-party library's repository:

| Third-Party Library Version | Supported RN Version |
| ----------------------------| -------------------- |
| 0.17.0                     |  0.72/0.77 |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-htmlview@0.17.0
```

#### **yarn**

```bash
yarn add react-native-htmlview@0.17.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { StyleSheet, View, Linking } from "react-native";
import HTMLView from "react-native-htmlview";

const HtmlViewExample = () => {
  const htmlContent = `
      <h1>Hello, World!</h1>
      <p>This is a <a href="https://www.vmall.com">link</a></p>
      <p>Here is an image: <img src="https://res.vmallres.com/pimages/uomcdn/CN/pms/202404/displayProduct/10086102004921/428_428_a_mobileFF345C8650FF6E88771386A6433556D0.jpg" alt="Example Image" /></p>
  `;

  return (
    <View style={{ ...styles.container, backgroundColor: "white" }}>
      <HTMLView
        value={htmlContent}
        stylesheet={styles} // Optional: Pass custom styles for HTML elements
        onLinkPress={(url) => Linking.openURL(url)} // Optional: Handle link presses
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 16,
  },
  // Define custom styles for HTML elements
  a: {
    fontWeight: "bold",
    color: "blue",
    fontSize: 20,
    borderColor: "#000000",
    borderWidth: 2,
  },
  img: {
    width: 200,
    height: 100,
  },
});

export default HtmlViewExample;
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Preview2; IDE: DevEco Studio 4.1.3.700; ROM: 3.0.0.19;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

> [!tip] This library is a UI component library. You can use the label of this library to implement the corresponding functions in HTML format that cannot take effect in the RN framework.

| Name            | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| value           | a string of HTML content to render                           | string | yes      | All      | yes               |
| onLinkPress     | a function which will be called with a url when a link is pressed. Passing this prop will override how links are handled | string | no       | All      | yes               |
| onLinkLongPress | a function which will be called with a url when a link is long pressed. The default is | string | no       | All      | yes               |
| stylesheet      | a stylesheet object keyed by tag name, which will override the styles applied to those respective tags. | string | no       | All      | yes               |
| renderNode      | a custom function to render HTML nodes however you see fit.  | string | no       | All      | yes               |
| bullet          | text which is rendered before every inside a ` li``ul `      | string | no       | All      | yes               |
| paragraphBreak  | text which appears after every element`p`                    | string | no       | All      | yes               |
| lineBreak       | text which appears after text elements which create a new line | string | no       | All      | yes               |
| addLineBreaks   | when explicitly , effectively sets                           | boolean | no       | All      | yes               |

## License

This project is licensed under [The ISC License (ISC)](https://github.com/jsdf/react-native-htmlview/blob/master/LICENSE).
