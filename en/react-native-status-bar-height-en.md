> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-status-bar-height</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ovr/react-native-status-bar-height">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ovr/react-native-status-bar-height/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-status-bar-height)

## Installation and Usage

Find the matching version information in the release address of a third-party library：

| Third-party library version | release information | Support RN version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.6.1      | [@react-native-ohos/react-native-status-bar-height Releases](https://github.com/react-native-oh-library/react-native-status-bar-height/releases) | 0.72，0.77     |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
# V2.6.1
npm install @react-native-ohos/react-native-status-bar-height
```

#### **yarn**

```bash
# V2.6.1
yarn add @react-native-ohos/react-native-status-bar-height
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```ts
import React, { useState } from "react";
import { View, Text, Button, PixelRatio } from "react-native";
import {TestCase, Tester} from "@rnoh/testerino"
import { getStatusBarHeight } from 'react-native-status-bar-height';

const App = (props) => {
    let [statusBarHeight,setData] = useState<number>(0);
    const getstatusbarHeight = () => {
    statusBarHeight = getStatusBarHeight(false);
    setData(statusBarHeight) 
    console.debug(statusBarHeight);
  };
  
  return (
    <Tester style={{flex: 1 , marginTop: 30}}>
      <TestCase itShould={"getstatusbarHeight"}>
        <View style={{ margin: 50, flexDirection: "column", justifyContent: "center" }}>
          <View>
            <Button
              title="getStatusBarHeight"
              onPress={() => getstatusbarHeight()}
            />
            <Text>{"statusBarHeight: "+JSON.stringify(statusBarHeight)+" dp"}</Text>
            <Text>{"statusBarHeight: "+JSON.stringify(PixelRatio.getPixelSizeForLayoutSize(statusBarHeight))+" px"}</Text>
          </View>
        </View>
      </TestCase>
    </Tester>
  );
};

export default App
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: 
| Third-party library version | release information | Support RN version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.6.1      | [@react-native-ohos/react-native-status-bar-height Releases](https://github.com/react-native-oh-library/react-native-status-bar-height/releases) | 0.72，0.77       |

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- |
| getStatusBarHeight | Called on each swipe event | `func` | yes | iOS,Android | yes |
| isIPhoneX | Whether it is an iPhoneX. | `function` |  yes | iOS | no |
| isIPhoneXMax | Whether it is an iPhoneX Max. | `function` |  yes | iOS | no |
| isIPhone12 | Whether it is an iPhone12. | `function` |  yes | IOS | no |
| isIPhone12Max | Whether it is an iPhone12 Max. | `function` |  yes | iOS | no |
| isIPhoneWithMonobrow | Whether it is an iPhone with Monobrow. | `function` |  yes | IOS | no |
| isExpo | whether to use Expo. | `function` |  yes | iOS,Android | no |

## Known Issues

## Others
isIPhoneX, isIPhoneXMax, isIPhone12, isIPhone12Max, and isIPhoneWithMonobrow are interfaces used to determine iPhone models, but HarmonyOS does not support them and they are not implemented. 

isExpo is used to determine whether the Expo framework is being used, but HarmonyOS does not support using the Expo framework and it is not implemented.
## License

This project is licensed under [The MIT License (MIT)](https://github.com/ovr/react-native-status-bar-height/blob/master/LICENSE).

