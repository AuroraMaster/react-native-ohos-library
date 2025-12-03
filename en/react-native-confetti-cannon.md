> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-confetti-cannon</code> </h1>
</p>

> [!TIP] [ GitHub address](https://github.com/VincentCATILLON/react-native-confetti-cannon)

Please check the corresponding version information in the Releases section of the third-party library's repository:

| Third-Party Library Version | Supported RN Version |
| ----------------------------| -------------------- |
| 1.5.2                     |  0.72/0.77 |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-confetti-cannon@1.5.2
```

#### **yarn**

```bash
yarn add react-native-confetti-cannon@1.5.2
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

#### Using a Component

```js
import * as React from "react";
import { StyleSheet, View, Text } from "react-native";
import ConfettiCannon from "react-native-confetti-cannon";

export default function ConfettiCannonExample() {
  return (
    <View style={{ width: "100%", height: "100%" }}>
      <ConfettiCannon count={50} origin={{ x: -10, y: -10 }} />
    </View>
  );
}
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; OH SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio: 5.0.3.400; ROM: 3.0.0.25;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name           | Description                                | Type                   | Required | Platform        | HarmonyOS Support |
| -------------- | ------------------------------------------ | ---------------------- | -------- | --------------- | ----------------- |
| count          | items count to display                     | number                 | yes      | iOS,Android,Web | yes               |
| origin         | animation position origin                  | {x: number, y: number} | yes      | iOS,Android,Web | yes               |
| explosionSpeed | explosion duration (ms) from origin to top | number                 | no       | iOS,Android,Web | yes               |
| fallSpeed      | fall duration (ms) from top to bottom      | number                 | no       | iOS,Android,Web | yes               |
| fadeOut        | make the confettis disappear at the end    | boolean                | no       | iOS,Android,Web | yes               |
| colors         | give your own colors to the confettis      | string[]               | no       | iOS,Android,Web | yes               |
| autoStart      | auto start the animation                   | boolean                | no       | iOS,Android,Web | yes               |
| autoStartDelay | delay to wait before triggering animation  | number                 | no       | iOS,Android,Web | yes               |

## Event

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name              | Description                            | Type     | Required | Platform        | HarmonyOS Support |
| ----------------- | -------------------------------------- | -------- | -------- | --------------- | ----------------- |
| onAnimationStart  | callback triggered at animation start  | Function | no       | iOS,Android,Web | yes               |
| onAnimationResume | callback triggered at animation resume | Function | no       | iOS,Android,Web | yes               |
| onAnimationStop   | callback triggered at animation stop   | Function | no       | iOS,Android,Web | yes               |
| onAnimationEnd    | callback triggered at animation end    | Function | no       | iOS,Android,Web | yes               |

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name   | Description                           | Type     | Required | Platform        | HarmonyOS Support |
| ------ | ------------------------------------- | -------- | -------- | --------------- | ----------------- |
| start  | start the animation programmatically  | Function | no       | iOS,Android,Web | yes               |
| resume | resume the animation programmatically | Function | no       | iOS,Android,Web | yes               |
| stop   | stop the animation programmatically   | Function | no       | iOS,Android,Web | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/VincentCATILLON/react-native-confetti-cannon/blob/master/LICENSE).
