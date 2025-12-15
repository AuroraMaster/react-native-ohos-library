> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-image-sequence</code> </h1>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-image-sequence)

## 1. Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 0.9.1-0.0.3@deprecated     | [@react-native-oh-tpl/react-native-image-sequence-2 Releases(deprecated)](https://github.com/react-native-oh-library/react-native-image-sequence/releases) | 0.72       |
| 0.9.2                | [@react-native-ohos/react-native-image-sequence-2 Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-sequence/releases) | 0.72       |
| 0.10.0                | [@react-native-ohos/react-native-image-sequence-2 Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-sequence/releases) | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-image-sequence-2
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-image-sequence-2
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { StyleSheet, View } from "react-native";
import ImageSequence from 'react-native-image-sequence-2'
const images = [
    { uri: "https://octodex.github.com/images/stormtroopocat.jpg" },
    { uri: 'https://octodex.github.com/images/saint_nictocat.jpg' },
    require("./assets/2.jpg"),
    require("./assets/3.jpg"),
    require("./assets/4.jpg"),
    require("./assets/5.jpg"),
    require("./assets/6.jpg"),
];
const centerIndex = Math.floor(Math.random() * images.length);
const TestDemo = () => {
    return (
        <View style={styles.container}>
            <ImageSequence
                images={images}
                startFrameIndex={centerIndex}
                style={{ width: 200, height: 300 }}
            />
        </View>
    )
}
const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center'
    },
})

export default TestDemo
```

## 2. Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## 3. Link

|                           | Is supported autolink | Supported RN Version |
|---------------------------|-----------------------|----------------------|
| ~0.10.0                   | No                    |  0.77                |
| ~0.9.2                    | Yes                   |  0.72                |
| <= 0.9.1-0.0.3@deprecated | No                    |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

### 3.1 Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 3.2 Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code.

1. Method 1 (recommended): Use the HAR file.


> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-image-sequence-2":"file:../../node_modules/@react-native-ohos/react-native-image-sequence-2/harmony/image_sequence.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP]For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3.3 Configuring CMakeLists and Introducing ImageSequence2Package Package

> If you are using version <= 0.9.1-0.0.3, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-image-sequence-2/src/main/cpp" ./image_sequence_2)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_image_sequence_2)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "ImageSequence2Package.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
+     std::make_shared<ImageSequence2Package>(ctx)
    };
}
```

(If the code of the repository is written through CAPI, delete this section.)<br>Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { RNImageSequence } from "@react-native-ohos/react-native-image-sequence-2"

const arkTsComponentNames: Array<string> = ["SampleView", 
"Generated",
"PropsDisplayer",
+ RNImageSequence.NAME
]

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+  if (ctx.componentName === RNImageSequence.NAME) {
+     RNImageSequence({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag
+     })
+   }
...
}
...
```

Open the `entry/src/main/ets/RNPackagesFactory.ts`，file and add the following code:

```diff
  ...
+ import { ImageSequencePackage } from "@react-native-ohos/react-native-image-sequence-2/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ImageSequencePackage(ctx) 
  ];
}
```

</details>

## 4. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 5. Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 6. Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name             | Description                                                  | Type    | Required | Platform | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| images           | An array of source images. Each element of the array should be the result of a call to require(imagePath) | any[]   | Yes      | All      | Yes               |
| startFrameIndex  | Which index of the images array should the sequence start at. Default: 0 | number  | No       | All      | Yes               |
| framesPerSecond  | Playback speed of the image sequence. Default: 24            | number  | No       | All      | Yes               |
| loop             | Should the sequence loop. Default: true                      | boolean | No       | All      | Yes               |
| downsampleWidth  | The width to use for optional downsampling. Both `downsampleWidth` and `downsampleHeight` must be set to a positive number to enable downsampling. Default: -1 | number  | No       | All      | Yes               |
| downsampleHeight | The height to use for optional downsampling. Both `downsampleWidth` and `downsampleHeight` must be set to a positive number to enable downsampling. Default: -1 | number  | No       | All      | Yes               |

## 7. Known Issues

## 8. Others

## 9. License

This project is licensed under [The MIT License (MIT)](https://github.com/bwindsor/react-native-image-sequence/blob/aee3d372d7960234721e32d2b02432fb5d0fa98b/LICENSE), Please enjoy and participate freely in open source.
