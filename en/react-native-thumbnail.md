> Template version: v0.2.2
<p align="center">
  <h1 align="center"> <code>react-native-thumbnail</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/phuochau/react-native-thumbnail">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/phuochau/react-native-thumbnail/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-thumbnail)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                     | Supported RN Version |
|-------| ------------------------------------------------------------ | ---------- |
| 1.1.3@deprecated | [@react-native-oh-tpl/react-native-thumbnail Releases(deprecated)](https://github.com/react-native-oh-library/react-native-thumbnail/releases) | 0.72       |
| 1.1.4 | [@react-native-ohos/react-native-thumbnail Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-thumbnail/releases)                        | 0.72       |
| 1.2.0 | [@react-native-ohos/react-native-thumbnail Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-thumbnail/releases)                        | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-thumbnail
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-thumbnail
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.<br>
> [!TIP] The example depends on the react-native-image-picker library, see the [@react-native-ohos/react-native-image-picker document](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-image-picker.md) for introducing.
```js
import React from 'react';
import { StyleSheet, Text, View, TouchableOpacity, Image } from 'react-native';
import { launchCamera, launchImageLibrary } from 'react-native-image-picker';
import RNThumbnail from 'react-native-thumbnail';

export default function ThumbnailExample() {
    const [thumbnail, setThumbnail] = React.useState(null);

    const openCamera = async () => {
        try {
            const options = {
                mediaType: 'video',
                saveToPhotos: true,
                includeExtra: false,
                durationLimit: 5,
            };
            console.log('Launching camera with options:', options);
            const result = await launchCamera(options);
            console.log('Camera result:', result);
            if (result.didCancel) {
                console.log('User cancelled camera');
            } else if (result.errorCode === 'permission') {
                console.log('Permission not granted for camera.');
            } else if (result.errorCode === 'camera_unavailable') {
                console.log('Camera not available on device.');
            } else if (result.errorCode === 'others') {
                console.log(`Other error: ${result.errorMessage}`);
            } else {
                // Check whether the video is successfully obtained.
                if (result && result.assets && result.assets.length > 0) {
                    const asset = result.assets[0];
                    if (asset.type.includes('mp4')) {
                        console.log('Received video from camera. Getting thumbnail.');
                        const thumbnailResult = await RNThumbnail.get(asset.uri);
                        console.log('Thumbnail result:', thumbnailResult);
                        setThumbnail(thumbnailResult.path);
                    } else {
                        console.log('Gallery asset.type:', asset.type);
                    }
                } else {
                    console.log('No video selected or other issue occurred.');
                }
            }
        } catch (error) {
            console.log('Error launching camera: ', error);
        }
    };

    const openGallery = async () => {
        try {
            const options = {
                mediaType: 'video', // Modify mediaType to video.
                selectionLimit: 1,
                includeExtra: false,
            };
            console.log('Launching gallery with options:', options);
            const result = await launchImageLibrary(options);
            if (result.didCancel) {
                console.log('User cancelled gallery');
            } else if (result.errorCode === 'permission') {
                console.log('Permission not granted for gallery.');
            } else if (result.errorCode === 'others') {
                console.log(`Other error: ${result.errorMessage}`);
            } else {
                if (result && result.assets && result.assets.length > 0) {
                    const asset = result.assets[0];
                    // Check if type is defined
                    if (asset.type === undefined) {
                        console.log('Asset type is undefined.');
                    }

                    if (asset.type.includes('mp4')) {
                        console.log('Received video from gallery. Getting thumbnail.');
                        const thumbnailResult = await RNThumbnail.get(asset.uri);
                        console.log('Thumbnail result:', thumbnailResult);
                        setThumbnail(thumbnailResult.path);
                    } else {
                        console.log('Gallery asset.type:', asset.type);
                    }
                }
            }
        } catch (error) {
            console.log('Error launching gallery: ', error);
        }
    };

    return (
        <View style={styles.container}>
            <TouchableOpacity onPress={openCamera}>
                <Text>Open Camera1</Text>
            </TouchableOpacity>
            <TouchableOpacity onPress={openGallery}>
                <Text>Open Gallery1</Text>
            </TouchableOpacity>
            {thumbnail? (
                <Image style={{ width: 200, height: 200, borderWidth: 1, borderColor: 'black' }} source={{ isStatic: true, uri: thumbnail }} />
            ) : null}
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        width: '100%',
        height: '100%',
        backgroundColor: '#fff',
        alignItems: 'center',
        justifyContent: 'center',
    },
});
```

## Use Codegen

Version >= @react-native-ohos/react-native-thumbnail@1.1.4, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to Codegen, generate the bridge code of the third-party library by using the Codegen. For details, see[ Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-thumbnail@1.1.4 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

Open the harmony directory of the HarmonyOS project in DevEco Studio.

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

1. Use the HAR file.
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-thumbnail": "file:../../node_modules/@react-native-ohos/react-native-thumbnail/harmony/thumbnail.har"
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

### 3. Introducing RNThumbnailPackage Package to ArkTS

Open the entry/src/main/ets/RNPackagesFactory.ts file and add the following code:

```diff
import { RNPackageContext, RNPackage } from '@rnoh/react-native-openharmony/ts';
+import { RNThumbnailPackage } from '@react-native-ohos/react-native-thumbnail/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+    new RNThumbnailPackage(ctx),
  ];
}
```

### 4. Running

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

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                     | Supported RN Version |
|-------| ------------------------------------------------------------ | ---------- |
| 1.1.3@deprecated | [@react-native-oh-tpl/react-native-thumbnail Releases(deprecated)](https://github.com/react-native-oh-library/react-native-thumbnail/releases) | 0.72       |
| 1.1.4 | [@react-native-ohos/react-native-thumbnail Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-thumbnail/releases)                        | 0.72       |
| 1.2.0 | [@react-native-ohos/react-native-thumbnail Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-thumbnail/releases)                        | 0.77       |

The content of this document has been verified based on the following versions:

1. RNOH: 0.72.98; SDK: HarmonyOS-5.0.0(API12); IDE: DevEco Studio 5.0.3.906; ROM: NEXT.0.0.71;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## API

> [!tip] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description                             | Type     | Required | Platform | HarmonyOS Support |
| ---- | --------------------------------------- | -------- | -------- | -------- | ----------------- |
| get  | Generates a thumbnail for a video file. | function | no       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/phuochau/react-native-thumbnail/blob/master/LICENSE).
