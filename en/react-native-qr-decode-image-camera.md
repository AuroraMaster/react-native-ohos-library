> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-qr-decode-image-camera</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/deepanrajkumar/react-native-qr-decode-image-camera">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/deepanrajkumar/react-native-qr-decode-image-camera/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-qr-decode-image-camera)

## Installation and Usage

Find the matching version information in the release address of a third-party library：

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 1.1.4@deprecated     | [@react-native-oh-tpl/react-native-qr-decode-image-camera Releases(deprecated)](https://github.com/react-native-oh-library/react-native-qr-decode-image-camera/releases) | 0.72       |
| 1.1.5      | [@react-native-ohos/react-native-qr-decode-image-camera Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-qr-decode-image-camera/releases) | 0.72       |
| 1.2.0      | [@react-native-ohos/react-native-qr-decode-image-camera Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-qr-decode-image-camera/releases) | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-qr-decode-image-camera
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-qr-decode-image-camera
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

> In the example: The launchImageLibrary method requires the introduction of the react-native-image-picker library for Harmony OS,Navigate to [react-native-image-picker](/zh-cn/react-native-image-picker.md)to view the usage instructions.

QRreader

```js
import React, {useState} from 'react';
import {Button, View, Text} from 'react-native';
import {QRreader} from 'react-native-qr-decode-image-camera';
import {launchImageLibrary} from 'react-native-image-picker';

export const qrExample = () => {
  const [reader, setReader] = useState<any>('');
  return (
    <View style={{flex: 1, justifyContent: 'center', alignItems: 'center'}}>
      <Button
        onPress={() => {
          launchImageLibrary({mediaType: 'photo', selectionLimit: 1}, data => {
            if (data.assets?.length) {
              const path = {
                uri: data.assets[0].originalPath,
              };
              QRreader(path)
                .then(res => {
                  setReader(res?.[0]?.originalValue);
                })
                .catch(error => {
                  console.log(error);
                });
            }
          });
        }}
        title="Click to select a QR code photo"
      />
      <Text style={{fontSize: 20}}>{reader}</Text>
    </View>
  );
};
```
QRscanner

```json
import React, {useState} from 'react';
import { View, Text, TouchableOpacity, StyleSheet} from 'react-native';
import { QRscanner} from 'react-native-qr-decode-image-camera';


export const qrExample = () => {

  const [flashMode, setflashMode] = useState(false);
  const onRead = res => {
    console.log(res);
  };
  return (
    <View style={styles.container}>
      <QRscanner
        onRead={onRead}
        renderBottomView={() => {
          return (
            <View
              style={{
                flex: 1,
                flexDirection: 'row',
                backgroundColor: '#0000004D',
              }}>
              <TouchableOpacity
                style={{
                  flex: 1,
                  alignItems: 'center',
                  justifyContent: 'center',
                }}
                onPress={() => {
                  if (flashMode) {
                    setflashMode(false);
                  } else {
                    setflashMode(true);
                  }
                }}>
                <Text style={{color: '#fff'}}>flashMode</Text>
              </TouchableOpacity>
            </View>
          );
        }}
        flashMode={flashMode}
        finderY={50}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#000',
  },
});
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                | Is supported autolink  | Supported RN Version |
|--------------------------------|-----------------------|----------------------|
| ~1.2.0                         |  No                   |  0.77                |
| ~1.1.5                         |  Yes                  |  0.72                |
| <= 1.1.4@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

If it is not included, please refer to [@react-native-ohos/react-native-vision-camera](/zh-cn/react-native-vision-camera.md) for instructions on how to include it.

## 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

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
    "@react-native-ohos/react-native-qr-decode-image-camera": "file:../../node_modules/@react-native-ohos/react-native-qr-decode-image-camera/harmony/qr_decode_image_camera.har"
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

### 3. Introducing RNQrDecodeImageCameraPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:


```diff
  ...
+ import {RNQrDecodeImageCameraPackage} from '@react-native-ohos/react-native-qr-decode-image-camera/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNQrDecodeImageCameraPackage(ctx)
  ];
}
```

### 4. Introducing NativeScan Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { NativeScan } from "@react-native-ohos/react-native-qr-decode-image-camera"


@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === NativeScan.NAME) {
+   NativeScan({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

### 5. Configure CMakeLists and import QrDecodeImageCameraPackage

> If you are using version <= 1.1.4, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following:

```diff
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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-qr-decode-image-camera/src/main/cpp" ./qr-decode-image-camera)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_qr_decode_image_camera)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "QrDecodeImageCameraPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<QrDecodeImageCameraPackage>(ctx),
    };
}
```

</details>

## Running

Click the `sync` button in the top right corner

Or run the following command in the terminal:

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

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

 | Name | Description | Type | Required | Platform | HarmonyOS Support |
 | ----------------------------- | ---------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
 | QRreader | Invoke this method to invoke the gallery, select the QR code image for image decoding, and asynchronously return the result. | funtion | no | iOS/Android | yes |

## Properties

### QRscanner

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                                      | Type    | Required | Platform    | HarmonyOS Support |
| ------------------ | ------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| isRepeatScan       | whether to allow repeated scanning               | boolean | no       | iOS/Android | yes               |
| zoom               | Camera focal length range 0-1                    | number  | no       | iOS/Android | no                |
| flashMode          | Turn on the flashlight                           | boolean | no       | iOS/Android | yes               |
| onRead             | scan callback                                    | funtion | yes      | iOS/Android | yes               |
| maskColor          | mask layer color                                 | string  | no       | iOS/Android | yes               |
| borderColor        | border color                                     | string  | no       | iOS/Android | yes               |
| cornerColor        | Color of corner of scan frame                    | string  | no       | iOS/Android | yes               |
| borderWidth        | border width of scan frame                       | number  | no       | iOS/Android | yes               |
| cornerBorderWidth  | border width of scan frame corner                | number  | no       | iOS/Android | yes               |
| cornerBorderLength | width and height of the corner of the scan frame | number  | no       | iOS/Android | yes               |
| rectHeight         | Scan frame height                                | number  | no       | iOS/Android | yes               |
| rectWidth          | Scan Frame Width                                 | number  | no       | iOS/Android | yes               |
| finderX            | scan frame X axis offset                         | number  | no       | iOS/Android | yes               |
| finderY            | scan frame Y axis offset                         | number  | no       | iOS/Android | yes               |
| isCornerOffset     | whether the corners are offset                   | boolean | no       | iOS/Android | yes               |
| cornerOffsetSize   | offset                                           | number  | no       | iOS/Android | yes               |
| bottomHeight       | Reserved height at the bottom                    | number  | no       | iOS/Android | yes               |
| scanBarAnimateTime | scan line time                                   | number  | no       | iOS/Android | yes               |
| scanBarColor       | scan line color                                  | string  | no       | iOS/Android | yes               |
| scanBarImage       | scan line image                                  | any     | no       | iOS/Android | yes               |
| scanBarHeight      | scan line height                                 | number  | no       | iOS/Android | yes               |
| scanBarMargin      | scanline left and right margin                   | number  | no       | IOS/Android | yes               |
| hintText           | hintText                                         | string  | no       | IOS/Android | yes               |
| hintTextStyle      | hint string style                                | object  | no       | iOS/Android | yes               |
| hintTextPosition   | hintTextPosition                                 | number  | no       | iOS/Android | yes               |
| renderTopView      | render top View                                  | funtion | no       | iOS/Android | yes               |
| renderBottomView   | render bottom View                               | funtion | no       | iOS/Android | yes               |
| isShowScanBar      | whether to show scan lines                       | boolean | no       | iOS/Android | yes               |
| topViewStyle       | render top container style                       | object  | no       | iOS/Android | yes               |
| bottomViewStyle    | render bottom container style                    | object  | no       | iOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/deepanrajkumar/react-native-qr-decode-image-camera/blob/master/LICENSE).
