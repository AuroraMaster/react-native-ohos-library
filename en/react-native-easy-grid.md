> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-easy-grid</code> </h1>
</p>

> [!TIP] [GitHub address](https://github.com/GeekyAnts/react-native-easy-grid)

Please check the corresponding version information in the Releases section of the third-party library's repository:

| Third-Party Library Version | Supported RN Version |
| ----------------------------| -------------------- |
| 0.2.2                      |  0.72/0.77 |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.


## Installation and Usage

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install react-native-easy-grid@0.2.2
```

#### **yarn**

```bash
yarn add react-native-easy-grid@0.2.2
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { Text } from "react-native";
import { Col, Row, Grid } from "react-native-easy-grid";

const App = () => {
  return (
    <Grid>
      <Col style={{ backgroundColor: "#9400D3" }}>
        <Row size={1} style={{ backgroundColor: "#FFB6C1" }}></Row>
        <Row size={2} style={{ backgroundColor: "#9400D3" }}></Row>
      </Col>
      <Col size={2} style={{ backgroundColor: "#FF4500" }}></Col>
      <Col size={3}>
        <Row size={1} style={{ backgroundColor: "#FFB6C1" }}></Row>
        <Row size={2} style={{ backgroundColor: "#9400D3" }}></Row>
        <Row size={1} style={{ backgroundColor: "#008000" }}></Row>
      </Col>
    </Grid>
  );
};

export default App;
```

## Constraints

##### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT Developer Beta1 5.0.0.25 ; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## Properties

The **Grid**, **Row**, and **Col** components receive the properties of all [React Native View](https://reactnative.dev/docs/view#props) components.

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**Common properties of RowProps and ColProps**

| Name                | Description | Type     | Required | Platform    | HarmonyOS Support |
| ------------------- | ----------- | -------- | -------- | ----------- | ----------------- |
| size                | Layout size.   | number   | no       | iOS,Android | yes               |
| onPress: () => void | Press event.   | function | no       | iOS,Android | yes               |

## Known Issues

## License

This project is licensed under [Apache License 2.0](https://github.com/GeekyAnts/react-native-easy-grid/blob/master/LICENSE).
