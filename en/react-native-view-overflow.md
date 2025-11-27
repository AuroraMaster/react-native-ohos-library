> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-view-overflow</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/entria/react-native-view-overflow">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/entria/react-native-view-overflow/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-view-overflow)

Please refer to the Releases page of the third-party library for the corresponding version information:

| Third-party Library Version | Release Information                                                     | Supported RN Version |
| ----------- | ------------------------------------------------------------ | ---------- |
| 0.0.5 | [@react-native-oh-tpl/react-native-view-overflow Releases](https://github.com/react-native-oh-library/react-native-view-overflow/releases) | 0.72       |
| 0.1.0   | [@react-native-ohos/react-native-view-overflow Releases]()   | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-view-overflow

# 0.77
npm install @react-native-ohos/react-native-view-overflow
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-view-overflow

# 0.77
yarn add @react-native-ohos/react-native-view-overflow
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import {View} from 'react-native';

import ViewOverflow from 'react-native-view-overflow';

export function ViewOverflowDemo() {
  return (
  <View style={{height: '100%', backgroundColor: 'white', padding: 10}}>

    <View style={{width: 200, height: 100, backgroundColor: 'red'}}>
      <ViewOverflow style={{width: 100, height: 50, backgroundColor: 'blue'}}>
          <ViewOverflow style={{width: 50, height: 25, backgroundColor: 'skyblue', left: 60, top: 30}}>
            <View style={{backgroundColor: 'yellow', height: '100%', left: 20, top: 10}} />
          </ViewOverflow>
      </ViewOverflow>
    </View>

  </View>
  );
}
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.868; ROM: 6.0.0.112;

## Properties
[!TIP] This library can be used as a container component similar to the View component, allowing child controls to overflow and be displayed outside the parent layout. It can be used with public properties only and does not involve private properties or API methods.

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/entria/react-native-view-overflow/blob/master/LICENSE).
