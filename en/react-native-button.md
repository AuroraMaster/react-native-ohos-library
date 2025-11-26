> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-button</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ide/react-native-button">       
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ide/react-native-button/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/ide/react-native-button)

| Version                 | Support RN version                 |
| ------------------------- | -------------------------- |
| 3.1.0               |  0.72/0.77 |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-button@3.1.0 --save
```

#### **yarn**

```bash
yarn add react-native-button@3.1.0 --save
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 * @flow
 */

import React, { Component } from 'react';
import Button from 'react-native-button';
import {
    View, Text
} from 'react-native';

export default class ExampleComponent extends Component {
    constructor(props, context) {
        super(props, context);
        this.state = {
            isDisabled: false
        }
    }
    _handlePress() {
        this.setState({
            isDisabled: true
        });
        console.log('Now, button disabled');
    }
    render() {
        const { isDisabled } = this.state;
        return (
            <View style={{ marginTop: 50 }}>
                <Button
                    allowFontScaling={false}
                    accessibilityLabel="Learn more about this purple button"
                    style={{ fontSize: 20, color: 'yellow' }}
                    styleDisabled={{ color: 'white' }}
                    disabled={isDisabled}
                    containerStyle={{ padding: 10, height: 45, overflow: 'hidden', borderRadius: 4, backgroundColor: 'aqua' }}
                    disabledContainerStyle={{ backgroundColor: 'pink' }}
                    onPress={() => this._handlePress()}>
                    Hello World
                </Button>
            </View>
        );
    }
};
```

## Constraints

## Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH: 0.77.17; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## Properties (If Any)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                                                                                            | Type     | default | Required | Platform | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- | ----------------- |
| `accessibilityLabel` | VoiceOver will read this string when a user selects the associated element. | String |  | No     | All      | yes               |
| `allowFontScaling` | Specifies whether fonts should scale to respect Text Size accessibility settings. | Bool |  | No     | All      | yes               |
| `Disabled` | Disables the button                | Bool | false   | No       | All      | yes               |
| `Style` | The style for the button                                       | View Style Prop | ｛｝ | No       | All      | yes               |
| `styleDisabled` | The style for the disabled button | View Style Prop | ｛｝ | No       | All      | yes               |
| `containerStyle` | The style for the container | View Style Prop | ｛｝ | No       | All      | yes               |
| `disabledContainerStyle` | The style for the container when the button is disabled | View Style Prop | ｛｝ | No       | All      | yes               |
| `childGroupStyle` | The style for the child views               | View Style Prop | ｛｝ | No       | All      | yes               |
| `androidBackground` | The background for android devices.                      | Background Prop Type |  | No       | Android | no             |
| `onPress`   | Handler to be called when the user taps the button.   | Function |         | No       | All      | yes              |

## Known Issues

-[ ] The allowFontScaling property is invalid, and the text font does not change with the modification of the system font.[issue#99](https://github.com/ide/react-native-button/issues/99)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ide/react-native-button/blob/main/LICENSE).
