> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-translucent-modal</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/23mf/react-native-translucent-modal">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/23mf/react-native-translucent-modal/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-translucent-modal)

Please refer to the Releases page of the third-party library for the corresponding version information:

| Third-party Library Version | Release Information                                                     | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.1.0      | [@react-native-oh-tpl/react-native-translucent-modalReleases](https://github.com/react-native-oh-library/react-native-translucent-modal/releases) | 0.72       |
| 1.2.0      | [@react-native-ohos/react-native-translucent-modal Releases]() | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-translucent-modal

# 0.77
npm install @react-native-ohos/react-native-translucent-modal
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-translucent-modal

# 0.77
yarn add @react-native-ohos/react-native-translucent-modal
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import { View, TouchableWithoutFeedback, Image, Button, StyleSheet } from "react-native-harmony";
// @ts-expect-error
import Modal from "react-native-translucent-modal";

const STYLES = StyleSheet.create({
    wrapper: {
        flex: 1,
    },
    imageBackground: {
        width: 300,
        height: 200,
    }
});

export const E_ReactNativeTranslucentModal: React.FC = (): JSX.Element => {

    const [transparent, setTransparent] = useState(false)
    const [visible, setVisible] = useState(false)
    const [animationType, setAnimationType] = useState('none')

    return <View style={STYLES.wrapper}>
        <Modal transparent={transparent} animationType={animationType}
            visible={visible} onRequestClose={() => setVisible(!visible)}>
            <TouchableWithoutFeedback onPress={() => setVisible(false)}>
             {/* Note: 1. This image component is used as an example. You need to import your component as needed.
                2. The sample image address needs to be replaced as needed. */}
                <Image source={{ uri: "https://hbimg.huabanimg.com/ed258f740ab675e3b3a0b6e7abc44eb7bd832c523396b-cJL1G9_fw658"}} style={STYLES.imageBackground} />
            </TouchableWithoutFeedback>
        </Modal>
        <Button title="Display Modal" onPress={() => setVisible(true)}></Button>
        <Button title="Set transparent to true" onPress={() => setTransparent(true)}></Button>
        <Button title="Set animationType to 'slide'" onPress={() => setAnimationType('slide')}></Button>
        <Button title="Set animationType to 'fade'" onPress={() => setAnimationType('fade')}></Button>
    </View>;
}

```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.868; ROM: 6.0.0.112;

Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

> [!TIP] The **Modal** component provided by React Native can implement the immersive effect of the status bar on the HarmonyOS and iOS platforms.

| Name                          | Description                                         | Type     | Required | Platform | HarmonyOS Support |
| ----------------------------- | --------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| `animationType`               | Animation type of modal.                            | string   | No      | All      | yes               |
| `transparent`                 | Whether the background of the modal is transparent. | boolean  | No      | All      | yes               |
| `visible`                     | Controls whether the modal is displayed.            | boolean  | No      | All      | yes               |
| `onRequestClose?: () => void` | Called when the model request close.                | function | No      | ALL      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/23mf/react-native-translucent-modal/blob/master/LICENSE.md).
