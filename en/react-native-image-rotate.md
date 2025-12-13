> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-rotate</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/dgladkov/react-native-image-rotate">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/dgladkov/react-native-image-rotate/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-image-rotate)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                     | Supported RN Version |
|-------| ------------------------------------------------------------ | ---------- |
| <= 2.1.0-0.0.1@deprecated | [@react-native-oh-tpl/react-native-image-rotate Releases(deprecated)](https://github.com/react-native-oh-library/react-native-image-rotate/releases) | 0.72       |
| 2.1.1 | [@react-native-ohos/react-native-image-rotate Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-rotate/releases)                        | 0.72       |
| 2.2.0 | [@react-native-ohos/react-native-image-rotate Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-rotate/releases)                        | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

Go to the project directory and execute the following instruction:

#### npm

```bash
npm install @react-native-ohos/react-native-image-rotate
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-image-rotate
```

The following code shows the basic use scenario of the repository:

```js
import React, { Component } from 'react';
import {
  Image,
  StyleSheet,
  Text,
  TouchableHighlight,
  View
} from 'react-native';

import ImageRotate from 'react-native-image-rotate';

const SOURCE_IMAGE = 'https://upload.wikimedia.org/wikipedia/en/5/56/Warcraft_Teaser_Poster.jpg';

export default class App extends Component {

  constructor() {
    super();
    this.state = {
      image: SOURCE_IMAGE,
      currentAngle: 0,
      width: 150,
      height: 240,
    };

    this.rotate = this.rotate.bind(this);
  }

  rotate(angle) {
    const nextAngle = this.state.currentAngle + angle;
    ImageRotate.rotateImage(
      SOURCE_IMAGE,
      nextAngle,
      (uri) => {
        this.setState({
          image: uri,
          currentAngle: nextAngle,
          width: this.state.height,
          height: this.state.width,
        });
      },
      (error) => {
        console.error(error);
      }
    );
  }

  render() {
    return (
      <View style={styles.container}>
        <View style={styles.imageContainer}>
          <Image style={{width: this.state.width, height: this.state.height}} source={{uri: this.state.image}} />
        </View>
        <TouchableHighlight
          onPress={() => this.rotate(90)}
          style={styles.button}
        >
          <Text style={styles.text}>ROTATE CW</Text>
        </TouchableHighlight>

        <TouchableHighlight
          onPress={() => this.rotate(-90)}
          style={styles.button}
        >
          <Text style={styles.text}>ROTATE CCW</Text>
        </TouchableHighlight>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  button: {
    backgroundColor: 'red',
    padding: 5,
    margin: 5,
  },
  imageContainer: {
    height: 240,
    justifyContent: 'center',
  },
  text: {
    color: 'white',
  },
});

```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                           | Is supported autolink | Supported RN Version |
|---------------------------|-----------------------|----------------------|
| ~2.2.0                    | No                    |  0.77                |
| ~2.1.1                    | Yes                   |  0.72                |
| <= 2.1.0-0.0.1@deprecated | No                    |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

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

Currently, two methods are available:

1. Use the HAR file.
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-image-rotate": "file:../../node_modules/@react-native-ohos/react-native-image-rotate/harmony/imageRotate.har"
  }
```

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see[Directly Linking Source Code](/en/link-source-code.md)

### 3.Configuring CMakeLists and Introducing ImageRotatePackage

> If you are using version <= 2.1.0-0.0.1, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt`, and add the following code:

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-image-rotate/src/main/cpp" ./imageRotate)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_image_rotate)
# RNOH_END: manual_package_linking_2
```
Open `entry/src/main/cpp/PackageProvider.cpp`, and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ImageRotatePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ImageRotatePackage>(ctx)
    };
}
```

### 4.Introducing RNImageRotatePackage Package to ArkTS

Open the entry/src/main/ets/RNPackagesFactory.ts file and add the following code:

```diff
  ...
  
+  import { RNImageRotatePackage } from '@react-native-ohos/react-native-image-rotate/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNImageRotatePackage(ctx)
  ];
}
```

</details>

## Running

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

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## Static Method

> [!TIP]The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!TIP]If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name        | Description    | Type     | Required | Platform    | HarmonyOS   Support |
| ----------- | -------------- | -------- | -------- | ----------- | ------------------- |
| rotateImage | rotate picture | Function | no       | iOS/Android | yes                 |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/dgladkov/react-native-image-rotate/blob/master/LICENSE).
