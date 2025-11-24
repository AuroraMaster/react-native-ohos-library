> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-video-cache</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/zhigang1992/react-native-video-cache">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-video-cache)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information:

| Third-party Library Version | Release Information                                                     | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.7.4@deprecated      | [@react-native-oh-tpl/react-native-video-cache Releases(deprecated)](https://github.com/react-native-oh-library/react-native-video-cache/releases) | 0.72       |
| 2.7.5      | [@react-native-ohos/react-native-video-cache Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-video-cache/releases)                        | 0.72       |
| 2.8.0      | [@react-native-ohos/react-native-video-cache Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-video-cache/releases)                        | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-video-cache
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-video-cache
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useEffect, useState } from "react";
import { StyleSheet, Text, View } from "react-native";
import  { convertAsync } from "react-native-video-cache";

export default function App() {
    const url =
        "https://cdn.plyr.io/static/demo/View_From_A_Blue_Moon_Trailer-720p.mp4";
    const [asyncVersion, setAsyncVersion] = useState<string>('');
    useEffect(() => {
        convertAsync(url).then(setAsyncVersion);
    }, [])
    return (
        <View style={styles.container}>
            <Text style={styles.welcome}>☆Original URL☆</Text>
            <Text style={styles.instructions}>{url}</Text>
            <Text style={styles.welcome}>☆Async Proxy URL☆</Text>
            <Text style={styles.instructions}>{asyncVersion}</Text>
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: "center",
        alignItems: "center",
        backgroundColor: "#F5FCFF",
        padding: 20
    },
    welcome: {
        fontSize: 20,
        textAlign: "center",
        margin: 10,
    },
    instructions: {
        textAlign: "center",
        color: "#333333",
        marginBottom: 5,
    },
});
```

## Link

Version >= @react-native-ohos/react-native-video-cache@2.7.5 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks. Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/rnoh-video-cache": "file:../../node_modules/@react-native-ohos/react-native-video-cache/harmony/react_native_video_cache.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/rnoh-video-cache": "file:../../node_modules/@react-native-ohos/react-native-video-cache/harmony/react_native_video_cache"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install --no-link
```

### 3. Introducing RNVideoCachePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+   import { RNVideoCachePackage } from '@react-native-ohos/rnoh-video-cache/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNVideoCachePackage(ctx)
  ];
}
```

### 4. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Please refer to the Releases page of the third-party library for the corresponding version information:

| Third-party Library Version | Release Information                                                     | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.7.4@deprecated      | [@react-native-oh-tpl/react-native-video-cache Releases(deprecated)](https://github.com/react-native-oh-library/react-native-video-cache/releases) | 0.72       |
| 2.7.5      | [@react-native-ohos/react-native-video-cache Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-video-cache/releases)                        | 0.72       |
| 2.8.0      | [@react-native-ohos/react-native-video-cache Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-video-cache/releases)                        | 0.77       |

This document is verified based on the following versions:

1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1(full sdk); IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;

## APIs

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-video-cache](https://github.com/zhigang1992/react-native-video-cache)

| Name           | Description                                          | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | ---------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| convertToCache | Return the local proxy cache server URL using sync.  | string | no       | Androis/IOS | no                |
| convertAsync   | Return the local proxy cache server URL using async. | string | no       | Androis/IOS | yes               |

## Known Issues
- [ ] 由于 HarmonyOS 侧原生依赖 HarmonyOS 三方库@ohos/video-cache中HttpProxyCacheServer实例化对象方法getProxyUrl暂为异步方法，导致本库同步方法convertToCache暂无法实现，问题：[issue#1](https://github.com/react-native-oh-library/react-native-video-cache/issues/1)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://www.mit-license.org).
