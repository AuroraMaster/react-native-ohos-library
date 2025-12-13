> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-colors</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/osamaqarem/react-native-image-colors">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20|%20expo%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/osamaqarem/react-native-image-colors/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-image-colors)

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 2.4.0-0.0.7@deprecated      | [@react-native-oh-tpl/react-native-image-colors Releases(deprecated)](https://github.com/react-native-oh-library/react-native-image-colors/releases) | 0.72       |
| 2.4.1      | [@react-native-ohos/react-native-image-colors Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-colors/releases)             | 0.72       |
| 2.5.1      | [@react-native-ohos/react-native-image-colors Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-colors/releases)             | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-image-colors
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-image-colors
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useEffect, useState } from 'react'
import {
  Platform,
  StyleSheet,
  Text,
  View,
  Image,
  SafeAreaView,
  Button,
} from 'react-native'
import { getColors } from 'react-native-image-colors'

const imgCat = require('./assets/images/cat.jpg')
const yunaUrl = 'https://img0.baidu.com/it/u=1934875822,4119553331&fm=253&fmt=auto&app=138&f=JPEG?w=720&h=480'
const base = 'data:image/jpeg;base64...'

const initialState = {
  colorOne: { value: '', name: '' },
  colorTwo: { value: '', name: '' },
  colorThree: { value: '', name: '' },
  colorFour: { value: '', name: '' },
  rawResult: '',
}

export default function demo() {
  const [colors, setColors] = useState(initialState)
  const fetchColors = async () => {
    const result = await getColors(imgCat, {
      fallback: '#000000',
    })

    switch (result.platform) {
      case 'android':
      case 'web':
        setColors({
          colorOne: { value: result.lightVibrant, name: 'lightVibrant' },
          colorTwo: { value: result.dominant, name: 'dominant' },
          colorThree: { value: result.vibrant, name: 'vibrant' },
          colorFour: { value: result.darkVibrant, name: 'darkVibrant' },
          rawResult: JSON.stringify(result),
        })
        break
      case 'ios':
        setColors({
          colorOne: { value: result.background, name: 'background' },
          colorTwo: { value: result.detail, name: 'detail' },
          colorThree: { value: result.primary, name: 'primary' },
          colorFour: { value: result.secondary, name: 'secondary' },
          rawResult: JSON.stringify(result),
        })
        break
      case 'harmony':
        setColors({
          colorOne: { value: result.mainColor, name: 'mainColor' },
          colorTwo: { value: result.largestProportionColor, name: 'largestProportionColor' },
          colorThree: { value: result.highestSaturationColor, name: 'highestSaturationColor' },
          colorFour: { value: result.averageColor, name: 'averageColor' },
          rawResult: JSON.stringify(result),
        })
        break
      default:
        throw new Error('Unexpected platform')
    }
  }

  return (
    <View style={styles.container}>
      <SafeAreaView style={styles.resultContainer}>
        <Text style={styles.loading}>Result:</Text>
        <Button title='button' onPress={() => fetchColors() }></Button>
        <Text style={styles.result}>{colors.rawResult}</Text>
      </SafeAreaView>
      <Image
        resizeMode="contain"
        style={styles.image}
        source={ imgCat }
      />
      <View style={styles.row}>

        <Box name={colors.colorOne.name} value={colors.colorOne.value} />
        <Box name={colors.colorTwo.name} value={colors.colorTwo.value} />
      </View>
      <View style={styles.row}>
        <Box name={colors.colorThree.name} value={colors.colorThree.value} />
        <Box name={colors.colorFour.name} value={colors.colorFour.value} />
      </View>
    </View>
  )
}

interface BoxProps {
  value: string
  name: string
}

const Box = ({ value, name }: BoxProps) => {
  return (
    <View
      style={[
        styles.box,
        {
          backgroundColor: value,
        },
      ]}
    >
      <Text style={styles.colorName}>{name}</Text>
    </View>
  )
}

const styles = StyleSheet.create({
  image: {
    width: '100%',
    height: 250,
  },
  colorName: {
    backgroundColor: 'white',
    padding: 4,
    fontSize: 18,
  },
  box: {
    flex: 1,
    backgroundColor: 'red',
    justifyContent: 'center',
    alignItems: 'center',
  },
  row: {
    flex: 1,
    flexDirection: 'row',
    width: '100%',
  },
  resultContainer: {
    flex: 1,
    padding: 20,
    width: '100%'
  },
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  loading: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  result: {
    textAlign: 'center',
    color: '#333333',
  },
})
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                           | Is supported autolink | Supported RN Version |
|---------------------------|-----------------------|----------------------|
| ~2.5.1                    | No                    |  0.77                |
| ~2.4.1                    | Yes                   |  0.72                |
| <= 2.4.0-0.0.7@deprecated | No                    |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

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
    "@react-native-ohos/react-native-image-colors": "file:../../node_modules/@react-native-ohos/react-native-image-colors/harmony/image_colors.har"
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

### 3. Configure CMakeLists and import ImageColorsPackage

> If you are using version <= 2.4.0-0.0.7, please skip this chapter.

open `entry/src/main/cpp/CMakeLists.txt`，add：

```cmake
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-image-colors/src/main/cpp" ./image-colors)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_image_colors)
# RNOH_END: manual_package_linking_2
```

open `entry/src/main/cpp/PackageProvider.cpp`，add：

```c++
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ImageColorsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ImageColorsPackage>(ctx)
    };
}
```

### 4. Introducing RNImageColorsPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNImageColorsPackage } from "@react-native-ohos/react-native-image-colors/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNImageColorsPackage(ctx)
  ];
}
```

</details>

## Running

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

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## API

### ImageColors.getColors(uri: string, config?: Config): Promise

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name      | Description                           | Type     | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------- | -------- | -------- | -------- | ----------------- |
| getColors | Fetch prominent colors from an image. | Function | yes      | all      | yes               |

### Uri

A string which can be:

| Name | Description                                                                                                                                                                                                        | Type   | Required | Platform | HarmonyOS Support |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| uri  | 1. URL: [`https://i.imgur.com/O3XSdU7.jpg`](https://i.imgur.com/O3XSdU7.jpg);<br>2. Local file: const catImg = require('./images/cat.jpg');<br>3. Base64: const catImgBase64 = 'data:image/jpeg;base64,/9j/4Ri...' | string | yes      | all      | yes               |

> The mime type prefix for base64 is required (e.g. data:image/png;base64).

### Config

The config object is optional.

| Name           | Description                                                                                                                                                                                    | Type                                                   | Required | Default     | Supported    | HarmonyOS Support |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ | -------- | ----------- | ------------ | ----------------- |
| `fallback`     | If a color property couldn't be retrieved, it will default to this hex color string                                                                                                            | `string`                                               | no       | `"#000000"` | all          | yes               |
| `cache`        | Enables in-memory caching of the result - skip downloading the same image next time.                                                                                                           | `boolean`                                              | no       | `false`     | all          | yes               |
| `key`          | Unique key to use for the cache entry. The image URI is used as the unique key by default. You should explicitly pass a key if you enable caching and you're using a base64 string as the URI. | `string`                                               | no       | `undefined` | all          | yes               |
| `headers`      | HTTP headers to be sent along with the GET request to download the image                                                                                                                       | `Record<string, string>`                               | no       | `undefined` | iOS, Android | yes               |
| `pixelSpacing` | How many pixels to skip when iterating over image pixels. Higher means better performance (**note**: value cannot be lower than 1).                                                            | `number`                                               | no       | `5`         | Android      | no                |
| `quality`      | Highest implies no downscaling and very good colors.                                                                                                                                           | `'lowest'` <br> `'low'` <br> `'high'` <br> `'highest'` | no       | `'low'`     | iOS, Web     | no                |

### ImageColorsResult

Every result object contains a respective `platform` key to help narrow down the type.

HarmonyImageColors

| Name                     | Description                                         | Type     | Required | Platform  | HarmonyOS Support |
| ------------------------ | --------------------------------------------------- | -------- | -------- | --------- | ----------------- |
| `mainColor`              | The main colors of the image.                       | `string` | no       | harmonyOS | yes               |
| `largestProportionColor` | The color with the highest proportion in the image. | `string` | no       | harmonyOS | yes               |
| `highestSaturationColor` | The color with the highest saturation in the image. | `string` | no       | harmonyOS | yes               |
| `averageColor`           | The average color of the image.                     | `string` | no       | harmonyOS | yes               |
| `platform`               | The platform is HarmonyOS.                          | `string` | no       | all       | yes               |

### ImageColors.cache

| Name       | Description             | Type     | Required | Params                                | Platform | HarmonyOS Support |
| ---------- | ----------------------- | -------- | -------- | ------------------------------------- | -------- | ----------------- |
| getItem    | Read cache result.      | Function | no       | key: string                           | all      | yes               |
| setItem    | Set a cached result.    | Function | no       | key: string, value: ImageColorsResult | all      | yes               |
| removeItem | Delete a cached result. | Function | no       | key: string                           | all      | yes               |
| clear      | Clearing the cache.     | Function | no       |                                       | all      | yes               |

### Notes

- Since the implementation of each platform is different you can get **different color results for each**.
- This module is a wrapper around the [Palette](https://developer.android.com/reference/androidx/palette/graphics/Palette) class on Android, [UIImageColors](https://github.com/jathu/UIImageColors) on iOS and [node-vibrant](https://github.com/Vibrant-Colors/node-vibrant) for the web and [@ohos.effectKit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-effectkit-V5) on harmonyOS.

## Known Issues

- [x] harmonyOS 获取颜色值暂时只能得到固定的一种颜色，暂不支持通过传入`pixelSpacing`或`quality`参数来计算获取不同精确度的颜色值。[issue 链接](https://github.com/react-native-oh-library/react-native-image-colors/issues/16)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/osamaqarem/react-native-image-colors/blob/master/LICENSE).
