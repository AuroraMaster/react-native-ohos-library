> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@bam.tech/react-native-image-resizer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/bamlab/react-native-image-resizer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bamlab/react-native-image-resizer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-image-resizer)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 3.0.9@deprecated  | [@react-native-oh-tpl/react-native-image-resizer Releases(deprecated)](https://github.com/react-native-oh-library/react-native-image-resizer/releases) | 0.72       |
| 3.0.10            | [@react-native-ohos/react-native-image-resizer Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-resizer/releases)   | 0.72       |
| 3.1.0             | [@react-native-ohos/react-native-image-resizer Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-resizer/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Go to the project directory and enter the following command:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-image-resizer
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-image-resizer
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported library remains unchanged.

```tsx
import React, { useRef, useState } from 'react';
import {
  Alert,
  Image,
  Platform,
  ScrollView,
  StyleSheet,
  Text,
  TextInput,
  TouchableOpacity,
  View,
} from 'react-native';
import ImageResizer from '@bam.tech/react-native-image-resizer';
import type {
  ResizeMode,
  Response,
} from '@bam.tech/react-native-image-resizer';
import { launchImageLibrary } from 'react-native-image-picker';

const modeOptions: { label: string; value: ResizeMode }[] = [
  {
    label: 'contain',
    value: 'contain',
  },
  {
    label: 'cover',
    value: 'cover',
  },
  {
    label: 'stretch',
    value: 'stretch',
  },
];

const onlyScaleDownOptions: { label: string; value: boolean }[] = [
  {
    label: 'true',
    value: true,
  },
  {
    label: 'false',
    value: false,
  },
];

function ImageResizerDemo() {
  const [selectedMode, setMode] = useState<ResizeMode>('contain');
  const [onlyScaleDown, setOnlyScaleDown] = useState(false);
  const [imageUri, setImageUri] = useState<null | string>();
  const [sizeTarget, setSizeTarget] = useState(80);
  const [resizedImage, setResizedImage] = useState<null | Response>();

  const resize = async () => {
    if (!imageUri) return;

    setResizedImage(null);

    try {
      let result = await ImageResizer.createResizedImage(
        imageUri,
        sizeTarget,
        sizeTarget,
        'JPEG',
        100,
        0,
        undefined,
        false,
        {
          mode: selectedMode,
          onlyScaleDown,
        }
      );

      setResizedImage(result);
    } catch (error) {
      Alert.alert('Unable to resize the photo');
    }
  };
  
  const selectImageFromPicker = async () => {
    launchImageLibrary({ mediaType: 'photo' }, (response) => {
      if (!response || !response.assets) return;
      const asset = response.assets[0];
      if (asset) {
        setImageUri(asset.uri);
      }
    });
  };

  return (
    <ScrollView
      style={styles.scrollView}
      contentContainerStyle={styles.container}
    >
      <Text style={styles.welcome}>Image Resizer example</Text>
      <View style={styles.imageSourceButtonContainer}>
        <TouchableOpacity style={styles.button} onPress={selectImageFromPicker}>
          <Text>{'Select an image (react-native-image-picker)'}</Text>
        </TouchableOpacity>
      </View>
     
      <Text style={styles.instructions}>This is the original image:</Text>
      {imageUri ? (
        <Image
          style={styles.image}
          source={{ uri: imageUri }}
          resizeMode="contain"
        />
      ) : null}

      <Text style={styles.instructions}>Resized image:</Text>
      <Text>Mode: </Text>
      <View style={styles.optionContainer}>
        {modeOptions.map((mode) => (
          <TouchableOpacity
            style={styles.buttonOption}
            onPress={() => setMode(mode.value)}
            key={mode.label}
          >
            <Text>{`${mode.label} ${
              selectedMode === mode.value ? '✅' : ''
            }`}</Text>
          </TouchableOpacity>
        ))}
      </View>

      <Text>Only scale down? </Text>
      <View style={styles.optionContainer}>
        {onlyScaleDownOptions.map((scaleDownOption) => (
          <TouchableOpacity
            style={styles.buttonOption}
            onPress={() => setOnlyScaleDown(scaleDownOption.value)}
            key={scaleDownOption.label}
          >
            <Text>{`${scaleDownOption.label} ${
              onlyScaleDown === scaleDownOption.value ? '✅' : ''
            }`}</Text>
          </TouchableOpacity>
        ))}
      </View>

      <Text>Target size: </Text>
      <TextInput
        style={styles.textInput}
        placeholder={sizeTarget.toString()}
        keyboardType="decimal-pad"
        onChangeText={(text) => {
          setSizeTarget(Number(text));
        }}
      />

      <TouchableOpacity style={styles.button} onPress={resize}>
        <Text>Click me to resize the image</Text>
      </TouchableOpacity>
      {resizedImage ? (
        <>
          <Image
            style={styles.image}
            source={{ uri: resizedImage.uri }}
            resizeMode="contain"
          />
          <Text>Width: {resizedImage.width}</Text>
          <Text>Height: {resizedImage.height}</Text>
        </>
      ) : null}
    </ScrollView>
  );
};  
  
const styles = StyleSheet.create({
  scrollView: {
    backgroundColor: '#F5FCFF',
  },
  container: {
    paddingVertical: 100,
    paddingHorizontal: 10,
  },
  imageSourceButtonContainer: {
    marginBottom: 10,
  },
  welcome: {
    fontSize: 20,
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
  image: {
    height: 250,
    marginBottom: 10,
  },
  button: {
    backgroundColor: '#2596be',
    paddingHorizontal: 30,
    paddingVertical: 20,
    borderRadius: 10,
    alignItems: 'center',
  },
  optionContainer: {
    alignSelf: 'stretch',
    flexDirection: 'row',
    justifyContent: 'space-around',
    marginBottom: 10,
  },
  buttonOption: {
    backgroundColor: '#2596be',
    paddingHorizontal: 10,
    paddingVertical: 10,
    borderRadius: 10,
  },
  textInput: {
    height: 40,
    borderColor: 'black',
    borderWidth: 2,
    margin: 10,
    alignSelf: 'stretch',
    textAlign: 'center',
    overflow: 'hidden',
  },
});

export default ImageResizerDemo;    
```

## Use Codegen

Version >= @react-native-ohos/react-native-image-resizer@3.0.10, compatible with codegen-lib for generating bridge code.

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-image-resizer@3.0.10 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

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

1. Import via har package (this method will be deprecated after the IDE improves related functions; currently the preferred method);
2. Directly link to the source code.

Method 1 (recommended): Import via har package

> [!TIP] The har package is located in the `harmony` folder under the third-party library installation path.

Open `entry/oh-package.json5` and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-image-resizer": "file:../../node_modules/@react-native-ohos/react-native-image-resizer/harmony/image_resizer.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following command in the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code

> [!TIP] If you need to directly link to the source code, please refer to [Direct Source Code Linking Instructions](/en/link-source-code.md).

### 3. Introducing ImageResizerPackage in ArkTs

Open `entry/src/main/ets/RNPackagesFactory.ts` and add:

```diff
  ...
+ import {ImageResizerPackage} from '@react-native-ohos/react-native-image-resizer/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ImageResizerPackage(ctx)
  ];
}
```

### 4. Configuring CMakeLists and Introducing ImageResizerPackage

> V3.0.10 requires configuring CMakeLists and importing ImageResizerPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-image-resizer/src/main/cpp" ./image-resizer)

# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_ImageResizer)
# RNOH_BEGIN: manual_package_linking_2
```

> [!Tip] Note: The NODE_MODULES definition above is the installation path of the source library. Users can define NODE_MODULES according to the path where the source library is installed.

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ImageResizerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ImageResizerPackage>(ctx)
    };
}
```

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following command in the terminal:

```bash
cd entry
ohpm install
```

Then compile and run.

> [!TIP] This library also depends on [[@react-native-ohos/react-native-image-picker](https://github.com/react-native-oh-library/usage-docs/blob/master/en/react-native-image-picker.md)]. If this library has already been introduced in the HarmonyOS project, you can skip the steps in this chapter and use it directly.

If not introduced, please refer to the Link section of [[@react-native-ohos/react-native-image-picker](https://github.com/react-native-oh-library/usage-docs/blob/master/en/react-native-image-picker.md)](https://github.com/react-native-oh-library/usage-docs/blob/master/en/react-native-image-picker.md#link) for introduction.

## Constraints

### Compatibility

To use this library, you need to use the correct React-Native and RNOH versions. Additionally, you need to use the matching DevEco Studio and phone ROM.

Verified successfully in the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 5.1.0.150 (API Version 12); IDE: DevEco Studio 5.1.1.830; ROM: 5.1.0.150;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 5.0.0.71(API Version 12 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 5.1.0.150;             |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description         | Type     | Required | Platform    | HarmonyOS Support |
|--------------------|---------------------|----------|----------|-------------|-------------------|
| createResizedImage | Resize local images | function | No       | Android/iOS | Yes               |

### createResizedImage parameters

| Name                 | Description         | Type    | Platform    | HarmonyOS Support |
|----------------------|---------------------|---------|-------------|-------------------|
| imageUri             | Path of image file, or a base64 encoded image string prefixed with 'data:image/imagetype' where imagetype is jpeg or png. | string  | Android/iOS | Yes               |
| width                | Width to resize to (see mode for more details) | number  | Android/iOS | Yes               |
| height               | Height to resize to (see mode for more details) | number  | Android/iOS | Yes               |
| compressFormat       | Can be either JPEG, PNG or WEBP. | string  | Android/iOS | Yes               |
| quality              | A number between 0 and 100. Used for the JPEG compression. | number  | Android/iOS | Yes               |
| rotation             | Rotation to apply to the image, in degrees. | number  | Android/iOS | Yes               |
| outputPath           | The resized image path. If null, resized image will be stored in cache folder. To set outputPath make sure to add option for rotation too (if no rotation is needed, just set it to 0). | string  | Android/iOS | Yes               |
| keepMeta             | If true, will attempt to preserve all file metadata/exif info, except the orientation value since the resizing also does rotation correction to the original image. Defaults to false, which means all metadata is lost. Note: This can only be true for JPEG images which are loaded from the file system (not Web). | boolean | Android/iOS | Yes               |
| options.mode         | Similar to react-native Image's resizeMode: either contain (the default), cover, or stretch. contain will fit the image within width and height, preserving its ratio. cover preserves the aspect ratio, and makes sure the image is at least width wide or height tall. stretch will resize the image to exactly width and height. | string  | Android/iOS | Yes               |
| options.onlyScaleDown | 	If true, will never enlarge the image, and will only make it smaller. | boolean | Android/iOS | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/bamlab/react-native-image-resizer/blob/master/LICENSE).