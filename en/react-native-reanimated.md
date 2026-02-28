> Template version: v0.4.0

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

This project is based on [react-native-reanimated](https://github.com/software-mansion/react-native-reanimated)。

This third-party library has been migrated to Gitcode and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-reanimated`, The version correspondence details are as follows:

|Name| Version | Release Information | Supported RN Version |Supported Autolink|Compile API Version|Community Baseline Version|npm Address|
|-------|-------|-----| ---------- |---------- |---------- |---------- |---------- |
|@react-native-ohos/react-native-reanimated| ~4.0.0 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-reanimated/releases)               | 0.82       |No|API12+|4.2.1 |[Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-reanimated)|
|@react-native-ohos/react-native-reanimated| ~3.18.1 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-reanimated/releases)               | 0.77       |No|API12+|3.18.0 |[Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-reanimated)|
|@react-native-ohos/react-native-reanimated| ~3.6.5 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-reanimated/releases)               | 0.72       |Yes|API12+|3.6.0 |[Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-reanimated)|
|@react-native-oh-tpl/react-native-reanimated| <= 3.6.4@deprecated | [ Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-harmony-reanimated/releases) | 0.72       | No|API12+| 3.6.0 |[Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/react-native-reanimated)|

## 1. Installation and Usage

> [!TIP] Attention：
`react-native-reanimated version >= 4.0.0`, `worklets` has been separated into a standalone library and needs to be imported separately. Refer to the [@react-native-ohos/react-native-worklets documentation](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-worklets.md)

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
# RN 0.72
npm install react-native-reanimated@3.6.0
npm install @react-native-ohos/react-native-reanimated

# RN 0.77
npm install react-native-reanimated@3.18.0
npm install @react-native-ohos/react-native-reanimated

# RN 0.82
npm install react-native-reanimated@4.2.1
npm install @react-native-ohos/react-native-reanimated
```

#### **yarn**

```bash
# RN 0.72
yarn add react-native-reanimated@3.6.0
yarn add @react-native-ohos/react-native-reanimated

# RN 0.77
yarn add react-native-reanimated@3.18.0
yarn add @react-native-ohos/react-native-reanimated

# RN 0.82
yarn add react-native-reanimated@4.2.1
yarn add @react-native-ohos/react-native-reanimated
```

<!-- tabs:end -->

#### Plugin configuration

Add Plugin to `babel.config.js`:

> [!TIP] Why is this needed? The Reanimated Babel plugin automatically converts special JavaScript functions (called worklets) so that they can be passed and run on the UI thread.

```js
  module.exports = {
    presets: [
      ... // don't add it here :)
    ],
    plugins: [
      ...
      // version < 4.0.0
      'react-native-reanimated/plugin',

      // version >= 4.0.0
      'react-native-worklets/plugin',
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

## 2. Link

|                                      | Is supported autolink  | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~4.0.0                               |  No              |  0.82     |
| ~3.18.1                               |  No                   |  0.77                |
| ~3.6.5                              |  Yes                  |  0.72                |
| <= 3.6.4@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.

[!TIP] version >= 4.0.0.
This version of HarmonyOS requires native code implementation relying on `@react-native-ohos/react-native-worklets`. If this library has already been imported in the HarmonyOS project, there is no need to re-import it. You can skip the steps in this section and directly use it.
If it has not been imported, please refer to the [Link section of the @react-native-ohos/react-native-worklets documentation](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-worklets.md) for import instructions.

<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

### 2.1. Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an overrides field in the project's root oh-package.json5 file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the official documentation.

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony",
     // version >= 4.0.0
    "@react-native-ohos/react-native-worklets": "file:../node_modules/@react-native-ohos/react-native-worklets/harmony/worklets.har"
  }
}
```

### 2.2. Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

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

### 2.3. Configuring CMakeLists and Introducing ReanimatedPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

# version >= 4.0.0 If the corresponding SVG Feature flags are enabled, the following configuration is required:
+ add_compile_definitions(REANIMATED_FEATURE_FLAGS='[EXPERIMENTAL_CSS_ANIMATIONS_FOR_SVG_COMPONENTS:true]')

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)

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

### 2.4. Introducing ReanimatedPackage to ArkTS 

Open`entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { ReanimatedPackage} from '@react-native-ohos/react-native-reanimated/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ReanimatedPackage(ctx),
  ];
}
```

</details>

### 2.5 Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1 Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
4. RNOH: 0.82.7;  SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1.260; ROM: 6.0.0.130 SP15;

### 3.2.Permission requirements (If using sensors, corresponding sensor permissions need to be added)

> [!Tip] To utilize the function of the sensor, a version >= 4.0.0 is required. This function is only effective on the RN 82 version.

Add permissions in the `module.json5` file located in the `entry` directory.

```
"requestPermissions": [
+  {
+    "name": "ohos.permission.ACCELEROMETER",  // Acceleration sensor permission name
+    "reason": "$string:accele_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"inuse"
+    }
+  },
+  {
+    "name": "ohos.permission.GYROSCOPE", // Gyroscope sensor permission name
+    "reason": "$string:gyr_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"inuse"
+    }
+  },
]
```
Add the reasons for requesting the above permissions under the "entry" directory.
Open `entry/src/main/resources/base/element/string.json`, and add:
```
{
  "string": [
+    {
+      "name": "accele_reason",
+      "value": "Use the acceleration sensor"
+    },
+    {
+      "name": "gyr_reason",
+      "value": "Use the gyroscope sensor"
+    },
  ]
}
```

## 4. API

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
| `runOnJS`<sup>deprecated from 4.0.0</sup>            | runOnJS lets you asynchronously run non-workletized functions that could not otherwise run on the UI thread. This applies to most external libraries as they do not have their functions marked with "worklet"; directive. | function | No       | All      | yes               |
| `runOnUI`<sup>deprecated from 4.0.0</sup>            | runOnUI lets you asynchronously run workletized functions on the UI thread.                                                                                                                                                | function | No       | All      | yes               |
| `measure`          | measure lets you synchronously get the dimensions and position of a view on the screen, all on the UI thread.                                                                                                              | function | No       | All      | yes               |
| `Easing`           | easing set motion trajectory                                                                                                                                                                                               | function | No       | All      | yes               |
| `useAnimatedKeyboard`           | useAnimatedKeyboard lets you create animations based on state and height of the virtual keyboard.                                                                                                             | function | No       | All      | yes               |
| `useComposedEventHandler`<sup>3.18.0+</sup> | This is a hook that lets you compose useEvent-based event handlers (such as useAnimatedScrollHandler or your own custom ones) into a single, combined event handler. | function | No       | All      | yes               |
| `makeMutable`<sup>3.18.0+</sup> | makeMutable is a function internally used by the useSharedValue hook to create a shared value | function | No       | All      | yes               |
| `ReducedMotionConfig`<sup>3.18.0+</sup> | change behavior in response to the device's reduced motion accessibility setting. | function | No       | All      | yes               |
| `useAnimatedGestureHandler`<sup>deprecated from 3.18.0</sup> | lets you create animations based on gesture handlers. | function | No | All | No |
| `useScrollViewOffset`<sup> deprecated from 4.0.0 </sup> | lets you to create animations based on the offset of a ScrollView.<br /><br />3.6.0:useScrollViewOffset(aref: RefObject<Animated.ScrollView>) => [SharedValue\<number\>];<br />3.18.0:useScrollViewOffset(animatedRef: AnimatedRef\<AnimatedScrollView\>, providedOffset?: SharedValue\<number\>): SharedValue\<number\>; | function | No | All | yes |
| `useScrollOffset` <sup> 4.0.0+ </sup> | lets you to create animations based on the offset of a scrollable component (e.g. ScrollView, FlatList, FlashList) | function | No | All | yes |
| `createAnimatedComponent ` |  lets you create an Animated version of any React Native component | function | No | All | yes |
| `getStaticFeatureFlag` <sup> 4.0.0+ </sup> | A function for obtaining static functionality flags (feature flags) | function | No | All | yes |
| `setDynamicFeatureFlag` <sup> 4.0.0+ </sup> | A function for dynamically setting function flags | function | No | All | yes |
| `reanimatedVersion` <sup> 4.0.0+ </sup> | Obtain the version number of the animation library | function | No | All | yes |
| `useAnimatedProps` | It is a custom Hook in the React Native Reanimated library, used to create animatable component properties | function | No | All | yes |

## 5. Properties

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

**CSS Transitions** <sup>4.0.0+</sup>
| Name                                  | Description                               | Type            | Required | Platform        | HarmonyOS  Support |
| ------------------------------------- | ----------------------------------------- | --------------- | -------- | --------------- | ------------------ |
| transitionProperty | lets you specify the name or names of styles properties to transition. | object  | No       | Android and iOS | yes       |
| transitionDuration | lets you specify the length of time the transition lasts. |  object |No | Android and iOS | yes       |
| transitionDelay | lets you specify the length of time to wait before transition starts. | object | No       | Android and iOS | yes       |
| transitionTimingFunction |  lets you adjust how intermediate values are calculated during the transition. | object | No | Android and iOS | yes  |
| transitionBehavior |  lets you determine whether the transition is applied to discrete properties. | object | No | Android and iOS | yes  |


**CSS Animations** <sup>4.0.0+</sup>
| Name                                  | Description                               | Type            | Required | Platform        | HarmonyOS  Support |
| ------------------------------------- | ----------------------------------------- | --------------- | -------- | --------------- | ------------------ |
| animationName  |  lets you specify keyframes for the animation. | object  | No       | Android and iOS | yes       |
| animationDuration | lets you specify the length of time the transition lasts. | object  |No    | Android and iOS | yes       |
| animationDelay | lets you specify the length of time to wait before animation starts. | object | No       | Android and iOS | yes       |
| animationTimingFunction |  lets you adjust how intermediate values are calculated during the transition. | object | No | Android and iOS | yes  |
| animationDirection  |  lets you specify which direction the animation should run. | object | No | Android and iOS | yes  |
| animationIterationCount  |  lets you repeat an animation given number of times or run it indefinitely. | object | No | Android and iOS | yes  |
| animationFillMode   |  lets you specify how the computed styles will be persisted before the animation runs and after it finishes. | object | No | Android and iOS | yes  |
| animationPlayState   |  lets you play and pause the animation. | object | No | Android and iOS | yes  |

**Common object**
| Name                                  | Description                               | Type            | Required | Platform        | HarmonyOS  Support |
| ------- | --------------------- | --------------- | -------- | --------------- | ------------------ |
| `GentleSpringConfig ` <sup>4.0.0+</sup> |  It is a predefined spring animation configuration, which creates a smooth and gentle spring effect. | Object | No | All | yes |
| `GentleSpringConfigWithDuration ` <sup>4.0.0+</sup> |  It is another form of GentleSpringConfig. It uses the parameters of duration and dampingRatio to define the spring animation. | Object | No | All | yes |
| `Reanimated3DefaultSpringConfig ` <sup>4.0.0+</sup> |  It will generate an animation that is highly elastic and has obvious oscillations. | Object | No | All | yes |
| `Reanimated3DefaultSpringConfigWithDuration ` <sup>4.0.0+</sup> | A flexible animation will be generated. | Object | No | All | yes |
| `SnappySpringConfig ` <sup>4.0.0+</sup> | The configuration defines the "Snappy" (agile) spring animation. | Object | No | All | yes |
| `SnappySpringConfigWithDuration ` <sup>4.0.0+</sup> | The configuration defines the "Snappy" (quick) spring animation. | Object | No | All | yes |
| `WigglySpringConfig ` <sup>4.0.0+</sup> | The configuration defines the "Wiggly" (swinging) spring animation, which will produce a distinct swinging/bouncing effect. | Object | No | All | yes |
| `WigglySpringConfigWithDuration ` <sup>4.0.0+</sup> | The configuration defines the "Wiggly" (swaying) spring animation, which completes the animation within 550ms and will have a distinct oscillation effect (underdamping) | Object | No | All | yes |
| `EasingFunctionFactory`  | A type definition in the library, serving as a factory function for creating easing functions | object | No | All | yes |
| `DynamicColorIOS` | designed to be used within Reanimated. It's a way to define colors that automatically adapt to light and dark mode on iOS | object | No |  iOS | no |


## 6. Known Issues

## 7. Others

## 8. License

This project is licensed under [The MIT License (MIT)](https://github.com/software-mansion/react-native-reanimated/blob/main/LICENSE).