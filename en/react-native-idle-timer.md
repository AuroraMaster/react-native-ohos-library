> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-idle-timer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/marcshilling/react-native-idle-timer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/marcshilling/react-native-idle-timer/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-idle-timer)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                                                                                                    | Supported RN Version |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| 2.2.3@deprecated      | [@react-native-oh-tpl/react-native-idle-timer Releases(deprecated)](https://github.com/react-native-oh-library/react-native-idle-timer/releases) | 0.72       |
| 2.2.4      | [@react-native-ohos/react-native-idle-timer Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-idle-timer/releases)                        | 0.72       |
| 2.3.0      | [@react-native-ohos/react-native-idle-timer Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-idle-timer/releases)                        | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-idle-timer
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-idle-timer
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useEffect } from 'react';
import { View, Text, Button } from 'react-native';
import IdleTimerManager from 'react-native-idle-timer';

const IdleTimerExample = () => {  
  useEffect(() => {
    // Disable the idle timer to prevent the screen from dimming or locking.
    IdleTimerManager.setIdleTimerDisabled(true, "video");

    // A cleanup function to re-enable the idle timer when the component is unmounted
    return () => {
     IdleTimerManager.setIdleTimerDisabled(false, "video");
    };
  }, []);
  return (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
      <Text>By default, the screen will remain on</Text>
    </View>
  );
};

export default IdleTimerExample;
```

## Use Codegen

> [!TIP] Version >= 2.2.4 no need to execute Codegen

If this repository has been adapted to Codegen, generate the bridge code of the third-party library by using the Codegen. For details, see[ Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-idle-timer@2.2.4 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks. Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

Open the harmony directory of the HarmonyOS project in DevEco Studio.

### 1.Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
  }
}
```

### 2.Introducing Native Code

Currently, two methods are available:

1. Use the HAR file.
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony" : "file:../react_native_openharmony",
    "@react-native-ohos/react-native-idle-timer": "file:../../node_modules/@react-native-ohos/react-native-idle-timer/harmony/idle_timer.har"
  }
```

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md)


### 3.Introducing RNIdleTimerPackage Package to ArkTS

Open the entry/src/main/ets/RNPackagesFactory.ts file and add the following code:

```diff
  ...
import type {RNPackageContext, RNPackage} from '@rnoh/react-native-openharmony/ts';
+import {RNIdleTimerPackage}  from '@react-native-ohos/react-native-idle-timer/ts';


export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+    new RNIdleTimerPackage(ctx)
  ];
}
```

### 4.Running

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

The following combinations have been verified:

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

## API

> [!tip] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                        | Type     | Required | Platform | HarmonyOS Support |
| -------------------- | ---------------------------------- | -------- | -------- | -------- | ----------------- |
| setIdleTimerDisabled | enable/forbidden screen idle timer | function | no       | All      | yes               |

## Known Issues

## Others 

## License

This project is licensed under [The MIT License (MIT)](https://github.com/marcshilling/react-native-idle-timer/blob/master/LICENSE.md).
