> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-hole-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ibitcy/react-native-hole-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://mitlicense.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-hole-view)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 3.0.0-alpha4-0.0.5@deprecated | [@react-native-oh-tpl/react-native-hole-view Releases(deprecated)](https://github.com/react-native-oh-library/react-native-hole-view/releases) | 0.72                 |
| 3.0.1             | [@react-native-ohos/react-native-hole-view Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-hole-view/releases)   | 0.72       |
| 3.1.0             | [@react-native-ohos/react-native-hole-view Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-hole-view/releases)   | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/react-native-hole-view
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-hole-view
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```jsx
import React, {useCallback, useEffect, useState} from 'react';
import {
    ScrollView,
    View,
    Text, TouchableOpacity,
} from 'react-native';

import {RNHole, RNHoleView, ERNHoleViewTimingFunction, IRNHoleViewAnimation} from "react-native-hole-view/src";

import Video from 'react-native-video';

const firstHole: RNHole = {x: 150, y: 390, width: 120, height: 120, borderRadius: 60};
const secondHole: RNHole = {x: 150, y: 40, width: 120, height: 120, borderRadius: 60};

const animationSettings: IRNHoleViewAnimation = {timingFunction: ERNHoleViewTimingFunction.EASE_IN_OUT, duration: 200};

const App = () => {
    const [holes, setHoles] = useState<RNHole[]>([]);
    const [animated, setAnimated] = useState<boolean>(false);
    const [animation, setAnimation] = useState<IRNHoleViewAnimation | undefined>(undefined);

    const onPress = useCallback(() => {
        if (animated) {
            setHoles([firstHole]);
        } else {
            setHoles([secondHole])
        }

        setAnimation({...animationSettings});
        setAnimated(!animated);
    }, [animated, animation])

    useEffect(() => {
        onPress();
    }, []);

    return (
        <View style={{flex: 1, alignItems: 'center', justifyContent: 'center'}}>
            <Text style={{flexGrow: 0, flex: 0, padding: 10}}>{"Wow! I'm a text inside a hole!"}</Text>
            <TouchableOpacity onPress={() => {
            }} style={{backgroundColor: 'pink', padding: 10, borderRadius: 5}}>
                <Text>{"Wow! I'm a button inside a hole!"}</Text>
            </TouchableOpacity>
            <ScrollView style={{flexGrow: 0, flex: 0, padding: 10}} horizontal={true}>
                <Text numberOfLines={1}>
                    {
                        "Wow! I'm a ScrollView inside a hole! Wow! I'm a ScrollView inside a hole! Wow! I'm a ScrollView inside a hole!"
                    }
                </Text>
            </ScrollView>
            <RNHoleView
                style={{
                    position: 'absolute',
                    width: '100%',
                    height: '100%',
                    backgroundColor: 'rgba(34,146,231,0.4)'
                }}
                animation={animation}
                holes={holes}
                onAnimationFinished={() => {
                    setAnimation(undefined);
                }}
            >
                <Video source={{uri: 'http://clips.vorwaerts-gmbh.de/VfE_html5.mp4'}}
                       resizeMode={"contain"}
                       style={{flex: 1}}
                />
            </RNHoleView>
            <View
                pointerEvents={'box-none'}
                style={{
                    position: 'absolute',
                    flex: 1,
                    width: '100%',
                    height: '100%',
                    alignItems: 'flex-end',
                    flexDirection: 'row',
                    justifyContent: 'center'

                }}>
                <TouchableOpacity onPress={onPress}
                                  style={{backgroundColor: 'pink', padding: 10, borderRadius: 5, bottom: 50}}>
                    <Text>{"Animate!"}</Text>
                </TouchableOpacity>
            </View>
        </View>
    );
};

export default App;

```

## Link

Version >= @react-native-ohos/react-native-hole-view@3.0.1 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/en/Autolinking.md

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
    "@react-native-ohos/react-native-hole-view": "file:../../node_modules/@react-native-ohos/react-native-hole-view/harmony/rnoh_holeview.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).

### 3. Configuring CMakeLists and Introducing HoleViewPackage

> If you are using version <= 3.0.0-alpha4-0.0.5, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-hole-view/src/main/cpp" ./rnohkeys)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_holeview)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "HoleViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<RNOHHoleViewPackage>(ctx),
    };
}
```

### 4. Introducing RNOHHoleViewPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import {RNOHHoleViewPackage} from '@react-native-ohos/react-native-audio-recorder-player/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNOHHoleViewPackage(ctx)
  ];
}
```

### 5. Running

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

| Name                | Description                   | Type                                                            | Required | Platform    | HarmonyOS Support |
| ------------------- | ----------------------------- | --------------------------------------------------------------- | -------- | ----------- | ----------------- |
| Holes               | Hole Array                    | Hole[]                                                          | no       | iOS/Android | yes               |
| animation           | Hole update animation effect  | { duration: number, timingFunction: ERNHoleViewTimingFunction } | no       | iOS/Android | yes               |
| onAnimationFinished | Animation completion callback | () => void                                                      | no       | iOS/Android | yes               |

## Known Issues

- [ ] Using C API OH_ArkUI_PointerEvent_SetStopPropagation to prevent the event from bubbling up causes scrollView out of control. This results in scrollView being able to scroll even outside the designated area: [issue#1](https://github.com/react-native-oh-library/react-native-hole-view/issues/2)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://mitlicense.org/).
