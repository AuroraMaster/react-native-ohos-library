> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-signature-capture</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/RepairShopr/react-native-signature-capture">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/RepairShopr/react-native-signature-capture/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>



> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-signature-capture)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 0.4.12@deprecated        | [@react-native-oh-tpl/react-native-signature-capture Releases(deprecated)](https://github.com/react-native-oh-library/react-native-signature-capture/releases) | 0.72                 |
| 0.4.13                | [@react-native-ohos/react-native-signature-capture Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-signature-capture/releases) | 0.72       |
| 0.5.0                 | [@react-native-ohos/react-native-signature-capture Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-signature-capture/releases) | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

####  npm

```bash
npm install @react-native-ohos/react-native-signature-capture
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-signature-capture
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```tsx
var React = require('react');
var ReactNative = require('react-native');

var {Component} = React;

var {
    AppRegistry,
    StyleSheet,
    Text,
    View, TouchableHighlight
} = ReactNative;

import SignatureCapture from 'react-native-signature-capture';

class RNSignatureExample extends Component {
    render() {
        return (
            <View style={{ flex: 1, flexDirection: "column" }}>
                <Text style={{alignItems:"center",justifyContent:"center"}}>Signature Capture Extended </Text>
                <SignatureCapture
                    style={[{flex:1},styles.signature]}
                    ref="sign"
                    onSaveEvent={this._onSaveEvent}
                    onDragEvent={this._onDragEvent}
                    saveImageFileInExtStorage={false}
                    showNativeButtons={false}
                    showTitleLabel={false}
                    backgroundColor="#ff00ff"
                    strokeColor="#ffffff"
                    minStrokeWidth={4}
                    maxStrokeWidth={4}
                    viewMode={"portrait"}/>

                <View style={{ flex: 1, flexDirection: "row" }}>
                    <TouchableHighlight style={styles.buttonStyle}
                        onPress={() => { this.saveSign() } } >
                        <Text>Save</Text>
                    </TouchableHighlight>

                    <TouchableHighlight style={styles.buttonStyle}
                        onPress={() => { this.resetSign() } } >
                        <Text>Reset</Text>
                    </TouchableHighlight>

                </View>

            </View>
        );
    }

    saveSign() {
        this.refs["sign"].saveImage();
    }

    resetSign() {
        this.refs["sign"].resetImage();
    }

    _onSaveEvent(result) {
        //result.encoded - for the base64 encoded png
        //result.pathName - for the file path name
        console.log(result);
    }
    _onDragEvent() {
         // This callback will be called when the user enters signature
        console.log("dragged");
    }
}

const styles = StyleSheet.create({
    signature: {
        flex: 1,
        borderColor: '#000033',
        borderWidth: 1,
    },
    buttonStyle: {
        flex: 1, justifyContent: "center", alignItems: "center", height: 50,
        backgroundColor: "#eeeeee",
        margin: 10
    }
});

AppRegistry.registerComponent('RNSignatureExample', () => RNSignatureExample);


```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~0.5.0                               |  No                   |  0.77                |
| ~0.4.13                              |  Yes                  |  0.72                |
| <= 0.4.12@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

### 1.Open `entry/oh-package.json5` file and add the following dependencies:

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
    "@react-native-ohos/react-native-signature-capture": "file:../../node_modules/@react-native-ohos/react-native-signature-capture/harmony/rnoh_signature_capture.har"
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

### 3. Configure CMakeLists and import RNBackgroundFetchPackage

> If you are using version <= 0.4.12, please skip this chapter.

open `entry/src/main/cpp/CMakeLists.txt`，add：

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

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-signature-capture/src/main/cpp" ./signature-capture)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_signature_capture)
# RNOH_END: manual_package_linking_2
```

open `entry/src/main/cpp/PackageProvider.cpp`，add：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "generated/SignatureCapturePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SignatureCapturePackage>(ctx),
    };
}
```

### 4. Introducing SignatureCaptureArkView Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { SignatureCaptureArkView } from '@react-native-ohos/react-native-signature-capture'

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+    if (ctx.componentName === SignatureCaptureArkView.NAME) {
+      SignatureCaptureArkView({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
...
}
...
```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.  

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ SignatureCaptureArkView.NAME
  ];
```

### 5. Introducing SignatureCapturePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { SignatureCapturePackage } from '@react-native-ohos/react-native-signature-capture/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SignatureCapturePackage(ctx)
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

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name                                                              | Description                                                                                                                                                                     | Type                      | Required | Platform    | HarmonyOS Support |
|-------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|----------|-------------|-------------------|
| showBorder                                                        | If this props is made to false, it will hide the dashed border.                                                                                                                 | boolean                   | no       | iOS         | yes               |
| showNativeButtons                                                 | If this props is made to true, it will display the native buttons "Save" and "Reset"..                                                                                          | boolean                   | no       | iOS/Android | yes               |
| showTitleLabel                                                    | If this props is made to true, it will display the "x_ _ _ _ _ _ _ _ _ _ _" placeholder indicating where to sign.                                                               | boolean                   | no       | iOS         | yes               |
| viewMode                                                          | "portrait" or "landscape" change the screen orientation based on boolean value                                                                                                  | "portrait" \| "landscape" | no       | iOS/Android | yes               |
| maxSize                                                           | sets the max size of the image maintains aspect ratio, default is 500                                                                                                           | number                    | no       | iOS/Android | yes               |
| minStrokeWidth                                                    | sets the min stroke line width                                                                                                                                                  | number                    | no       | Android     | yes               |
| maxStrokeWidth                                                    | sets the max stroke line width                                                                                                                                                  | number                    | no       | Android     | yes               |
| backgroundColor                                                   | Sets the background color of the component. Defaults to white. May be 'transparent'.                                                                                            | color                     | no       | iOS/Android | yes               |
| strokeColor                                                       | Sets the color of the signature. Defaults to black.                                                                                                                             | color                     | no       | iOS/Android | yes               |
| saveImageFileInExtStorage                                         | Make this props true, if you want to save the image file in external storage. Default is false. Warning: Image file will be visible in gallery or any other image browsing app. | boolean                   | no       | Android     | no                |
| onSaveEvent: (event: {pathName: string, encoded: string}) => void | Triggered when saveImage() is called, which return Base64 Encoded String and image file path.                                                                                   | function                  | no       | iOS/Android | yes               |
| onDragEvent: (event: boolean) => void                             | Triggered when user marks his signature on the canvas. This will not be called when the user does not perform any action on canvas.                                             | function                  | no       | iOS/Android | yes               |

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name       | Description                                                                                         | Type     | Required | Platform    | HarmonyOS Support |
|------------|-----------------------------------------------------------------------------------------------------|----------|----------|-------------|-------------------|
| saveImage  | when called it will save the image and returns the base 64 encoded string on onSaveEvent() callback | function | no       | iOS/Android | yes               |
| resetImage | when called it will clear the image on the canvas                                                   | function | no       | iOS/Android | yes               |


## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/RepairShopr/react-native-signature-capture/blob/master/LICENSE).

