> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-camera</code> </h1>
</p>

This project is based on [react-native-camera@v3.40.0](https://github.com/react-native-camera/react-native-camera/tree/v3.40.0).

Please go to the Releases release address of the third-party library to view the supporting version information: [@eact-native-ohos/react-native-camera Releases](https://github.com/react-native-oh-library/react-native-camera/releases). For older versions that are not published to npm, install the tgz package by referring to the [Installation Guide](/en/tgz-usage-en.md).

| Version                   | Releases info                                      |  Support RN version                    |
| ------------------------- | ------------------------------------------------- |  -------------------------- |
| v3.40.0                 | [@react-native-ohos/react-native-camera Releases](https://github.com/react-native-oh-library/react-native-camera/releases)  | 0.72/0.77 |



## 1. Installation and Usage

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install @react-native-ohos/react-native-camera
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-camera
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from 'react';
import { Text, View } from 'react-native';
import { RNCamera } from 'react-native-camera';
import {
    StyleSheet,
} from 'react-native';

export function CameraExample() {
    return (
        <View>
            <View style={[styles.button, styles.margin20]}
                onTouchEnd={() => {
                    const options = {
                        quality: 0.5,
                        base64: true,
                        width: 300,
                        height: 300,
                    };
                    this.camera.takePictureAsync(options).then((photoResult) => {
                        console.log("takepicture result:" + photoResult?.path)
                    });

                }
                }>
                <Text style={styles.buttonText}>Test takePicture</Text>
            </View>
           

            <RNCamera
                ref={ref => {
                    this.camera = ref;
                }}
                style={styles.cameraPreview}
            >
            </RNCamera>
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        paddingTop: 10,
        backgroundColor: '#000',
    },
    button: {
        width: 160,
        height: 36,
        backgroundColor: 'hsl(190, 50%, 70%)',
        paddingHorizontal: 16,
        paddingVertical: 8,
        borderRadius: 8,
    },
    margin20: {
        marginLeft: 20
    },
    buttonText: {
        width: '100%',
        height: '100%',
        fontWeight: 'bold',
    },
    cameraPreview: { width: '100%', aspectRatio: 56 / 100 }
});

export default CameraExample;
```

## 2. Manual Link

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1 Overrides RN SDK

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

### 2.2 Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@react-native-ohos/react-native-camera": "file:../../node_modules/@react-native-ohos/react-native-camera/harmony/reactNativeCamera.har"
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

### 2.3 Configuring CMakeLists and Introducing NativeCameraPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-camera/src/main/cpp" ./reactNativeCamera)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_native_camera)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "NativeCameraPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<NativeCameraPackage>(ctx)
    };
}
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "NativeCameraPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+        std::make_shared<NativeCameraPackage>(ctx)
    };
}
```


### 2.4 Import the react-native-camera component on the ArkTS side

Locate `function buildCustomRNComponent()`, usually in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add:

```diff
...
+ import { ReactCameraView } from '@react-native-ohos/react-native-camera';

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
...
+    if (ctx.componentName === ReactCameraView.NAME) {
+      ReactCameraView({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag,
+      })
+    }
...
}
...
```

> [!TIP] This library uses a hybrid approach, so you need to register the component name.

In `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, locate the `arkTsComponentNames` constant and add the component name to the array:

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ ReactCameraView.NAME
  ];
```

### 2.5 Introducing RNPhotoManipulatorPackage Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff  
  ... 
+ import { ReactNativeCameraPackage, FaceDectorPackage } from '@react-native-ohos/react-native-camera/ts';
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ReactNativeCameraPackage(ctx),
+   new FaceDectorPackage(ctx)
  ];
}
```

### 2.6 Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1 Compatibility

Check the release version information in the release address of the third-party library: [@react-native-ohos/react-native--photo-manipulator Releases](https://github.com/react-native-oh-library/react-native-camera/releases).

### 3.2 Permission Requirements

#### Add permissions in `module.json5` under the `entry` directory

Open `entry/src/main/module.json5` and add:

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.CAMERA",
+    "reason": "$string:camera_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"inuse"
+    }
+  },
+  {
+    "name": "ohos.permission.MICROPHONE",
+    "reason": "$string:microphone_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"inuse"
+    }
+  },
]
```

#### Add the permission rationale strings in `entry/src/main/resources/base/element/string.json`

```diff
...
{
  "string": [
+    {
+      "name": "camera_reason",
+      "value": "Use the camera"
+    },
+    {
+      "name": "microphone_reason",
+      "value": "Use the microphone"
+    },
  ]
}
```

## 4. Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform  | HarmonyOS Support |
| ---- | ----------- | ---- | -------- |-----------|-------------------|
| children                 | Set child components          | View    | no       | iOS/Android | yes               |
| type                     | Select the camera             | string  | no       | iOS/Android | yes               |
| flashMode                | Configure flash mode          | string  | no       | iOS/Android | yes               |
| exposure                 | Configure exposure            | number  | no       | iOS/Android | yes               |
| autoFocus                | Configure autofocus           | string  | no       | iOS/Android | yes               |
| whiteBalance             | Configure white balance       | string  | no       | iOS/Android | yes               |
| captureAudio             | Enable audio capture          | boolean | no       | iOS/Android | yes               |
| zoom                     | Set zoom factor               | number  | no       | iOS/Android | yes               |
| focusDepth               | Focus depth when autofocus is disabled | number  | no       | iOS/Android | yes |
| maxZoom                  | Set maximum zoom factor       | number  | no       | iOS/Android | yes               |
| pictureSize              | Set default picture resolution| string  | no       | iOS/Android | yes               |
| notAuthorizedView        | View displayed when not authorized | View | no   | Android     | no                |
| pendingAuthorizationView | View displayed while requesting authorization | View | no | Android | no |
| ratio                    | Camera aspect ratio           | string  | no       | Android     | no                |
| defaultVideoQuality      | Default video resolution      | string  | no       | iOS/Android | yes               |

###
## Static Methods

> [!TIP] The "Platform" column indicates the platforms supported by the original third-party library.

> [!TIP] "HarmonyOS Support" is `yes` if the HarmonyOS platform supports the method, `no` if not, and `partially` if only partially supported. Usage is consistent across platforms and mirrors the behavior on iOS or Android.

### camera
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- |-------------------|
| onBarCodeRead        | Receive barcode scan data     | BarCodeReadEvent    | no       | iOS/Android | yes               |
| onFacesDetected      | Receive face detection data   | Face | no | iOS/Android | no             |
| takePictureAsync     | Take a photo                  | TakePictureResponse | no       | iOS/Android | yes               |
| recordAsync          | Start recording video         | RecordResponse      | no       | iOS/Android | yes               |
| stopRecording        | Stop recording                | void                | no       | iOS/Android | yes               |
| getCameraIdAsync     | Retrieve available camera IDs | CameraType          | no       | iOS/Android | yes               |
| refreshAuthorization | Request permissions           | void                | no       | iOS/Android | yes               |


## 5. Known Issues
- [ ] `onFacesDetected` is not yet implemented [issue#1](https://github.com/react-native-oh-library/react-native-camera/issues/8) 

## 6. Others
- notAuthorizedView and pendingAuthorizationView attributes are unique to Android, representing the UI displayed during authorization requests. Harmony already provides a pop-up window during authorization.
- ratio is a unique property of Android and has no effect on iOS. [Source library readme location](https://github.com/react-native-camera/react-native-camera/blob/v3.40.0/docs/RNCamera.md#android-ratio)

## 7. License

This project is licensed under the [MIT License (MIT)](https://github.com/react-native-camera/react-native-camera/blob/master/LICENSE). Enjoy and feel free to contribute.