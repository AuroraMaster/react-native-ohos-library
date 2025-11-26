<p align="center">
  <h1 align="center"> <code>react-native-textinput-maxlength-fixed</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/2017398956/react-native-textinput-maxlength-fixed">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/2017398956/react-native-textinput-maxlength-fixed/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-textinput-maxlength-fixed)

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-textinput-maxlength-fixed Releases](https://github.com/react-native-oh-library/react-native-textinput-maxlength-fixed/releases).
| Third-party Library Version | Release Information                                                     | Support RN version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.1.2     | [@react-native-oh-tpl/react-native-textinput-maxlength-fixed Releases](https://github.com/react-native-oh-library/react-native-textinput-maxlength-fixed/releases) | 0.72       |
| 0.2.0     | [@react-native-ohos/react-native-textinput-maxlength-fixed Releases]()     | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-textinput-maxlength-fixed
# 0.77
npm install @react-native-ohos/react-native-textinput-maxlength-fixed
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-textinput-maxlength-fixed
# 0.77
yarn add @react-native-ohos/react-native-textinput-maxlength-fixed
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```ts
import * as React from 'react';

import { StyleSheet, View, Text, TextInput } from 'react-native';
import { multiply } from 'react-native-textinput-maxlength-fixed';

export default function App() {
  const [result, setResult] = React.useState<number | undefined>();

  React.useEffect(() => {
    multiply(3, 7).then(setResult);
  }, []);

  return (
    <View style={styles.container}>
      <Text>Result: {result}</Text>
      <TextInput maxLength={6} style={styles.textInput} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  box: {
    width: 60,
    height: 60,
    marginVertical: 20,
  },
  textInput: {
    borderColor: 'gray',
    borderWidth: 1,
    padding: 16,
    width: 300,
  },
});
```

## Use Codegen

> [!TIP] V0.2.0 for RN0.77 does not require execution of Codegen.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1.Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.Introducing Native Code
> [!TIP] Before introducing native code, please confirm the IDE version. For versions 5.0.3.810 and later, the following configuration needs to be added to the hvigor-config.json5 file in the Harmony project to solve the compilation error caused by excessively long paths
> "properties":{
>      "ohos.nativeResolver":false
> }

Currently, two methods are available:

1. Use the HAR file(recommended)；
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

- V0.1.2

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-textinput-maxlength-fixed": "file:../../node_modules/@react-native-oh-tpl/react-native-textinput-maxlength-fixed/harmony/textinput_maxlength_fixed.har"
  }
```

- V0.2.0

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-textinput-maxlength-fixed": "file:../../node_modules/@react-native-ohos/react-native-textinput-maxlength-fixed/harmony/textinput_maxlength_fixed.har"
  }
```

Click the `sync` button in the upper right corner.

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3.Introducing RNTextinputMaxlengthFixedPackage Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
import { RNPackageContext, RNPackage } from '@rnoh/react-native-openharmony';
import { SampleTurboModulePackage } from '../TurboModule/SampleTurboModulePackage';
import { ViewPagerPackage } from '@react-native-oh-tpl/react-native-pager-view/ts';
// V0.1.2
+import { RNTextinputMaxlengthFixedPackage } from "@react-native-oh-tpl/react-native-textinput-maxlength-fixed/ts";
// V0.2.0
+import { RNTextinputMaxlengthFixedPackage } from "@react-native-ohos/react-native-textinput-maxlength-fixed/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SampleTurboModulePackage(ctx),
    new ViewPagerPackage(ctx),
+    new RNTextinputMaxlengthFixedPackage(ctx),
  ];
}
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
2. RNOH: 0.77.17; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| multiply  | Calculate the product of two numbers. | number  | no | All      | yes |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-textinput-maxlength-fixed/blob/main/LICENSE).
