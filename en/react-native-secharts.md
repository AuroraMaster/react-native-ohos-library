> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-secharts</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/shifeng1993/react-native-secharts">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/shifeng1993/react-native-secharts/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/shifeng1993/react-native-secharts)

| Library Version | Supported RN Version |
| :--- | :--- |
| 1.7.0 | 0.72/0.77 |

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-secharts@1.7.0
```

#### **yarn**

```bash
yarn add react-native-secharts@1.7.0
```

> [!WARNING] The online echart file link that the library depends on has expired and needs to be replaced with a new domain name link to be introduced to use it normally

```js

// node_modules\react-native-secharts\main\dist\tmp\templates.js

//     <script type="text/javascript" src="https://cdn.bootcss.com/echarts/4.2.1/echarts.min.js"></script> // The linked certificate expired on Monday, March 10, 2025 at 09:02:41
+      <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/echarts/4.2.1/echarts.min.js"></script>

```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from "react";
import { View, StyleSheet, Text } from "react-native";
import { Echarts, echarts } from "react-native-secharts";

export default class SechartsBar extends Component {
  constructor(props) {
    super(props);
    this.state = {
      image: "",
      value: null,
      option1:
        (option = option =
          {
            xAxis: {
              type: "category",
              data: ["Mon", "Tue", "Wed", "Thu", "Fri"],
            },
            yAxis: {
              type: "value",
            },
            series: [
              {
                data: [120, 200, 150, 80, 70],
                type: "bar",
              },
            ],
          }),
      flag: false, // 这个布尔值是为了测试option1在setstate操作后不会被重置成初始状态。
    };
    this.echart1 = React.createRef();
  }

  render() {
    return (
      <View style={styles.container}>
        <View>
          <Echarts
            ref={this.echart1}
            option={this.state.option1}
            onPress={this.onPress}
            height={600}
            width={300}
            backgroundColor={"#468B58"}
            renderLoading={() => (
              <View style={{ backgroundColor: "rgba(255,255,0,0)" }} />
            )}
          />
        </View>
        <View>
          <Text>
            {!this.state.value
              ? "The clicked value is displayed here."
              : "The clicked value：" + this.state.value}
          </Text>
        </View>
      </View>
    );
  }
  onPress = (e) => {
    this.setState({ value: e.value });
  };
}
const styles = StyleSheet.create({
  container: {
    // flex: 1,
    // justifyContent: 'center',
    // alignItems: 'center',
    backgroundColor: "#F5FCFF",
  },
  buttonContainer: {
    width: 300,
    marginTop: 5,
  },
});
```

## Link


The HarmonyOS implementation of this library depends on the native code from react-native-webview. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [react-native-webview docs](/en/react-native-webview.md) to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `option` | ECharts configuration options. For details, please refer to https://echarts.apache.org/zh/option.html#title | object | yes | All | yes |
| `backgroundColor` | Background color of the chart canvas | string | no | All | yes |
| `width` | Canvas width | number | no | All | yes |
| `height` | Canvas height | number | no | All | yes |
| `renderLoading` | Loading overlay. Customization is not supported by default. To customize, please modify `startInLoadingState={true}` in `main/dist/index.js` within the `react-native-secharts` source code. | function | no | All | yes |
| `onPress` | Data press/click event on the canvas | function | no | All | yes |

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Prop | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `setOption` | Accepts an option object. Using this method is not recommended for `react-native-secharts` versions after 1.5.0. You can bind directly using React component state; simply update the state with the new option to trigger changes. | function | no | All | yes |
| `getImage` | Returns a base64 string via the callback, which can be combined with RNFS to save the image to the gallery. | function | no | All | yes |
| `clear` | Clears the ECharts canvas. | function | no | All | yes |

## Known Issues

## Others

The `renderLoading` prop does not take effect on Android and iOS. HarmonyOS behaves consistently with Android and iOS. [issue#109](https://github.com/shifeng1993/react-native-secharts/issues/109)

The original library uses an online CDN, so the ECharts component requires network support to display correctly. HarmonyOS behaves consistently with Android and iOS. [issue#79](https://github.com/shifeng1993/react-native-secharts/issues/79)

## License

This project is licensed under [The MIT License (MIT)](https://github.com/shifeng1993/react-native-secharts/blob/master/LICENSE).
