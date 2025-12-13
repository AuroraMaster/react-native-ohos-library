> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-bindingx</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/alibaba/bindingx">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/alibaba/bindingx/blob/master/LICENSE.md">
       <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-bindingx)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <=1.0.3-0.0.4@deprecated  | [@react-native-oh-tpl/react-native-bindingx Releases(deprecated)](https://github.com/react-native-oh-library/react-native-bindingx/releases) | 0.72       |
| 1.0.4             | [@react-native-ohos/react-native-bindingx Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-bindingx/releases)   | 0.72       |
| 1.1.0             | [@react-native-ohos/react-native-bindingx Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-bindingx/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

```bash
npm install @react-native-ohos/react-native-bindingx
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-bindingx
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, {Component} from 'react';
import {
  StyleSheet,
  View,
  Text,
  findNodeHandle,
  TouchableHighlight,
  PanResponder
} from 'react-native';

import bindingx from 'react-native-bindingx';

export default class App extends Component {

  _panResponder = PanResponder.create({
    onStartShouldSetPanResponder: (evt, gestureState) => true,
    onPanResponderGrant: (evt, gestureState) => {
      this.onBind();
    }
  });

  _x = 0;
  _y = 0;

  componentDidMount() {
    let anchor = findNodeHandle(this.refs._anchor);
    bindingx.prepare({
      eventType: 'pan',
      anchor: anchor
    });
  }

  onPanEnd = (e) => {
    if (e.state === 'end') {
      this._x += e.deltaX;
      this._y += e.deltaY;
    }
  }

  onBind() {

    let expression_x_origin = "x+" + this._x;

    let expression_y_origin = "y+" + this._y;

    let anchor = findNodeHandle(this.refs._anchor);
    let token = bindingx.bind({
      eventType: 'pan',
      anchor: anchor,
      props: [
        {
          element: anchor,
          property: 'transform.translateX',
          expression: expression_x_origin
        },
        {
          element: anchor,
          property: 'transform.translateY',
          expression: expression_y_origin
        }
      ]
    },this.onPanEnd);
  }

  render() {
    return (
      <View style={styles.container}>
        <View
          ref="_anchor"
          style={styles.anchor}
          {...this._panResponder.panHandlers}
        />

      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#F5FCFF',
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 10,
  },
  text: {
    textAlign: 'center',
    color: '#ffffff',
  },
  wrapper: {
    backgroundColor: '#0000ff',
    height: 48,
    alignItems: 'center',
    justifyContent: 'center'
  },
  margin: {
    marginTop: 20
  },
  anchor: {
    width: 80,
    height: 80,
    backgroundColor: '#ff0000',
    marginTop: 48
  }
});

```

## Link

|                                      | Is supported autolink  | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~1.1.0                               |  No                   |  0.77                |
| ~1.0.4                               |  Yes                  |  0.72                |
| <= 1.0.3-0.0.4@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md.

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
    "@react-native-ohos/react-native-bindingx": "file:../../node_modules/@react-native-ohos/react-native-bindingx/harmony/bindingx.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing ReactBindingXPackge

> If you are using version <= 1.0.3-0.0.4, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-ohos/react-native-bindingx/src/main/cpp" ./bindingx)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_bindingx)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ReactBindingXPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ReactBindingXPackage>(ctx),
    };
}
...
```


### 4. Introducing ReactBindingXPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {ReactBindingXPackage} from '@react-native-ohos/react-native-bindingx/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ReactBindingXPackage(ctx)
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

To use this library, you need to use the correct React-Native and RNOH versions. Additionally, you need to use the matching DevEco Studio and phone ROM.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name              | Description                                                                                                                                                                   | Type            | Required | Platform        | HarmonyOS Support  |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- | -------- | ----------------| ------------------ |
| bind              | Build a specific event type of binding instance. When the event is triggered, corresponding expression will be executed and touch off transform in specified element.         | string          | no      | iOS/Android     |      yes           |
| unbind            | unbind specified binding instance.                                                                                                                                            | void            | no      | iOS/Android     |      yes           |
| unbindAll         | unbind all binding instance                                                                                                                                                   | void            | no      | iOS/Android     |      yes           |
| prepare           | launch bind. This method is only useful for pan type binding.                                                                                                                 | void            | no      | iOS/Android     |      yes           |
| getComputedStyle  | get styles of specified view.                                                                                                                                                 | Promise<string> | no      | iOS/Android     |      yes           |

## Known Issues

## Others

## License

This project is licensed under [Apache License2.0](https://github.com/alibaba/bindingx/blob/master/LICENSE.md).
