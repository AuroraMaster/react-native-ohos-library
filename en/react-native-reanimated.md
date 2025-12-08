> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-reanimated</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-reanimated">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/software-mansion/react-native-reanimated/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [Github address](https://github.com/react-native-oh-library/react-native-harmony-reanimated/tree/sig)

The repository of this third-party library has been migrated to Gitcode and supports direct download from npm. The new package name is: @react-native-ohos/react-native-reanimated. The specific version ownership relationship is as follows:

| Version | Package Name                                                     | Repository | Release | Support RN version |
| ---------- | ------------------------------------------------------------ | ---------- |  ---------- |  ---------- |
| 3.6.0 | @react-native-oh-tpl/react-native-reanimated | [Github](https://github.com/react-native-oh-library/react-native-harmony-reanimated)|[Github Releases](https://github.com/react-native-oh-library/react-native-harmony-reanimated/releases)|0.72       |
| 3.18.0 | @react-native-ohos/react-native-reanimated         | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-reanimated/tree/br_rnoh0.77) |[Gitcode Releases]() | 0.77       |


## Installation and Usage


Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install react-native-reanimated@3.6.0
npm install @react-native-oh-tpl/react-native-reanimated

# 0.77
npm install react-native-reanimated@3.18.0
npm install @react-native-ohos/react-native-reanimated
```

#### **yarn**

```bash
# 0.72
yarn add react-native-reanimated@3.6.0
yarn add @react-native-oh-tpl/react-native-reanimated

# 0.77
yarn add react-native-reanimated@3.18.0
yarn add @react-native-ohos/react-native-reanimated
```

<!-- tabs:end -->

Add react-native-reanimated/plugin to `babel.config.js`:

> [!TIP] Why is this needed? The Reanimated Babel plugin automatically converts special JavaScript functions (called worklets) so that they can be passed and run on the UI thread.

```js
  module.exports = {
    presets: [
      ... // don't add it here :)
    ],
    plugins: [
      ...
      'react-native-reanimated/plugin',
    ],
  };
```

Clear the Metro cache (recommended):

<!-- tabs:start -->

#### **npm**

```bash
npm start --reset-cache
```

#### **yarn**

```bash
yarn start --reset-cache
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { Button, View } from "react-native";
import Animated, { useSharedValue, withSpring } from "react-native-reanimated";

export default function App() {
  const width = useSharedValue(100);

  const handlePress = () => {
    width.value = withSpring(width.value + 50);
  };

  return (
    <View style={{ flex: 1, alignItems: "center" }}>
      <Animated.View
        style={{
          width,
          height: 100,
          backgroundColor: "violet",
        }}
      />
      <Button onPress={handlePress} title="Click me" />
    </View>
  );
}
```

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

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

### 2.Introducing Native Code

Currently, two methods are available:


Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

- 0.72

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-reanimated": "file:../../node_modules/@react-native-oh-tpl/react-native-reanimated/harmony/reanimated.har"
  }
```

- 0.77

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-ohos/react-native-reanimated": "file:../../node_modules/@react-native-ohos/react-native-reanimated/harmony/reanimated.har"
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

### 3. Configuring CMakeLists and Introducing ReanimatedPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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
# 0.72
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-reanimated/src/main/cpp" ./reanimated)

# 0.77
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-reanimated/src/main/cpp" ./reanimated)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_reanimated)
# RNOH_BEGIN: manual_package_linking_2
```
> [!Tip] **Note**: The NODE_MODULES path refers to the installation path of the source repository. Users can define NODE_MODULES based on the path where the source repository is installed.

Open`entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ReanimatedPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ReanimatedPackage>(ctx)
    };
}
```

### 4. Introducing ReanimatedPackage to ArkTS 

Open`entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
// 0.72
+ import { ReanimatedPackage} from '@react-native-oh-tpl/react-native-reanimated/ts';

// 0.77
+ import { ReanimatedPackage} from '@react-native-ohos/react-native-reanimated/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ReanimatedPackage(ctx),
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


The content of this document has been verified based on the following version：

1、RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); IDE: DevEco Studio 5.1.1.830; ROM: 6.0.0.112 SP12;  
2、RNOH: 0.77.18; SDK: HarmonyOS-5.1.1.208(API19); IDE: DevEco Studio 5.1.1.830; ROM: 6.0.0.112 SP12;

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                                                                                                                                                                                                                | Type     | Required | Platform | HarmonyOS Support |
| ------------------ |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------| -------- | -------- | ----------------- |
| `withTiming`       | withTiming lets you create an animation based on duration and easing..                                                                                                                                                     | function | No       | All      | yes               |
| `withSpring`       | withSpring lets you create spring-based animations.                                                                                                                                                                        | function | No       | All      | yes               |
| `withDecay`        | withDecay lets you create animations that mimic objects in motion with friction. The animation will start with the provided velocity and slow down over time according to the given deceleration rate until it stops.      | function | No       | All      | yes               |
| `withRepeat`       | withRepeat is an animation modifier that lets you repeat an animation given number of times or run it indefinitely.                                                                                                        | function | No       | All      | yes               |
| `useSharedValue`   | useSharedValue lets you define shared values in your components.                                                                                                                                                           | function | No       | All      | yes               |
| `useAnimatedStyle` | useAnimatedStyle lets you create a styles object, similar to StyleSheet styles, which can be animated using shared values.                                                                                                 | function | No       | All      | yes               |
| `useAnimatedRef`   | useAnimatedRef lets you get a reference of a view. Used alongside measure, scrollTo, and useScrollViewOffset functions.                                                                                                    | function | No       | All      | yes               |
| `useDerivedValue`  | useDerivedValue lets you create new shared values based on existing ones while keeping them reactive.                                                                                                                      | function | No       | All      | yes               |
| `cancelAnimation`  | cancelAnimation lets you cancel a running animation paired to a shared value.                                                                                                                                              | function | No       | All      | yes               |
| `runOnJS`          | runOnJS lets you asynchronously run non-workletized functions that could not otherwise run on the UI thread. This applies to most external libraries as they do not have their functions marked with "worklet"; directive. | function | No       | All      | yes               |
| `runOnUI`          | runOnUI lets you asynchronously run workletized functions on the UI thread.                                                                                                                                                | function | No       | All      | yes               |
| `measure`          | measure lets you synchronously get the dimensions and position of a view on the screen, all on the UI thread.                                                                                                              | function | No       | All      | yes               |
| `Easing`           | easing set motion trajectory                                                                                                                                                                                               | function | No       | All      | yes               |
| `useAnimatedKeyboard`           | useAnimatedKeyboard lets you create animations based on state and height of the virtual keyboard.                                                                                                             | function | No       | All      | yes               |
| `useComposedEventHandler`<sup>3.18.0+</sup> | This is a hook that lets you compose useEvent-based event handlers (such as useAnimatedScrollHandler or your own custom ones) into a single, combined event handler. | function | No       | All      | yes               |
| `makeMutable`<sup>3.18.0+</sup> | makeMutable is a function internally used by the useSharedValue hook to create a shared value | function | No       | All      | yes               |
| `ReducedMotionConfig`<sup>3.18.0+</sup> | change behavior in response to the device's reduced motion accessibility setting. | function | No       | All      | yes               |
| `useAnimatedGestureHandler`<sup>deprecated from 3.18.0</sup> | lets you create animations based on gesture handlers. | function | No | All | No |
| `useScrollViewOffset` | lets you to create animations based on the offset of a ScrollView.<br /><br />3.6.0:useScrollViewOffset(aref: RefObject<Animated.ScrollView>) => [SharedValue\<number\>];<br />3.18.0:useScrollViewOffset(animatedRef: AnimatedRef\<AnimatedScrollView\>, providedOffset?: SharedValue\<number\>): SharedValue\<number\>; | function | No | All | yes |

## Properties

**WithSpringConfig**

| Name                    | Description                                                  | Type             | Required | Platform        | HarmonyOS  Support |
| ----------------------- | ------------------------------------------------------------ | ---------------- | -------- | --------------- | ------------------ |
| clamp<sup>3.18.0+</sup> | Limit of the scope of movement. If your spring would exceed this limit, then `dampingRatio` will be reduced (to make the spring less bouncy) | [number, number] | No       | Android and iOS | yes                |

**SharedValue**

| Name                  | Description                                                  | Type     | Required | Platform        | HarmonyOS  Support |
| --------------------- | ------------------------------------------------------------ | -------- | -------- | --------------- | ------------------ |
| get<sup>3.18.0+</sup> | Returns current value                                        | function | No       | Android and iOS | yes                |
| set<sup>3.18.0+</sup> | Updates stored value (supports direct value or updater function) | function | No       | Android and iOS | yes                |
| addListener           | Registers value change listener<br /><br />3.6.0:addListener:(listenerID: number, listener: (value: any) => void) => void;<br />3.18.0:addListener:(listenerID: number, listener: (value: Value) => void) => void; | function | No       | Android and iOS | yes                |
| modify                | Applies transformation to current value<br /><br />3.6.0:modify:(modifier?: (value: any) => any, forceUpdate?: boolean) => void;<br />3.18.0:modify:(modifier?: \<T extends Value\>(value: T) => T, forceUpdate?: boolean) => void; | Object   | No       | Android and iOS | yes                |

**DerivedValue**

| Name                                 | Description                 | Type     | Required | Platform        | HarmonyOS  Support |
| ------------------------------------ | --------------------------- | -------- | -------- | --------------- | ------------------ |
| set<sup>deprecated from 3.18.0</sup> | Derived values are readonly | function | No       | Android and iOS | No                 |

**CurrentLayoutAnimationsValues**

| Name                                  | Description           | Type   | Required | Platform        | HarmonyOS  Support |
| ------------------------------------- | --------------------- | ------ | -------- | --------------- | ------------------ |
| currentBorderRadius<sup>3.18.0+</sup> | Border radius of view | number | No       | Android and iOS | No                 |

**EntryAnimationsValues**

| Name                                 | Description           | Type   | Required | Platform        | HarmonyOS  Support |
| ------------------------------------ | --------------------- | ------ | -------- | --------------- | ------------------ |
| targetBorderRadius<sup>3.18.0+</sup> | Border radius of view | number | No       | Android and iOS | No                 |

**itemLayoutAnimation**

| Name                                  | Description                               | Type            | Required | Platform        | HarmonyOS  Support |
| ------------------------------------- | ----------------------------------------- | --------------- | -------- | --------------- | ------------------ |
| itemLayoutAnimation<sup>3.18.0+</sup> | Defines layout transitions for list items | LayoutAnimation | No       | Android and iOS | yes                |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/software-mansion/react-native-reanimated/blob/main/LICENSE).
