> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/slider</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/react-native-slider">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20web|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/callstack/react-native-slider/blob/main/LICENSE.md">
        <img src="https://img.shields.io/npm/l/@react-native-community/slider.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-slider)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
|-----------------------------| ------------------------------------------------------------ | ---------- |
| <= 4.4.3-0.3.4@deprecated   | [@react-native-oh-tpl/slider Releases(deprecated)](https://github.com/react-native-oh-library/react-native-slider/releases) | 0.72       |
| 4.4.4                       | [@react-native-ohos/slider Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-slider/releases) | 0.72       |
| 5.0.1                       | [@react-native-ohos/slider Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-slider/releases) | 0.77       |
| 5.1.2                     | [@react-native-ohos/slider Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-slider/releases)               | 0.82       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/slider
```

#### **yarn**

```bash
yarn add @react-native-ohos/slider
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

> [!TIP] When using the thumbImage attribute, please ensure that the imported image path is correct. You can check whether the image has been packaged into the static resource directory under the path harmony/entry/src/main/resources/rawfile/assets. If it does not exist, the file directory where the image is placed is incorrect.

```js
import Slider from "@react-native-community/slider"
import { View } from 'react-native'

export default function SliderExample() {
    return (
        <View style={{ backgroundColor: 'red', width: 200, height: 100 }}>
            <Slider
                style={{ width: 200, height: 40 }}
                minimumValue={0}
                maximumValue={1}
                minimumTrackTintColor="#FFFFFF"
                maximumTrackTintColor="#000000"
            />
        </View>
    );
};
```

## Link

|                                      | Is supported autolink  | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~5.1.2                              |  No              |  0.82     |
| ~5.0.1                              |  No              |  0.77     |
| ~4.4.4                               |  Yes             |  0.72     |
| <= 4.4.3-0.3.4@deprecated            |  No              |  0.72     |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

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

    "@react-native-ohos/slider": "file:../../node_modules/@react-native-ohos/slider/harmony/slider.har"
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

### 3. Configuring CMakeLists and Introducing SliderPackge

> If you are using version <= 4.4.3-0.3.4, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/slider/src/main/cpp" ./slider)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_slider)
# RNOH_END: link_packages
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "SliderPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SliderPackage>(ctx)
    };
}
```

### 4.Introducing slider Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { RNCSlider, SLIDER_TYPE } from "@react-native-ohos/slider"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === SLIDER_TYPE) {
+   RNCSlider({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag,
+   })
+ }
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
+ SLIDER_TYPE
  ];
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

Verified successfully in the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
4. RNOH: 0.82.1; SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1 Release; ROM:6.0.0.120 SP7

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name   | Description       | Type     | Required | Platform     | HarmonyOS Support |
| ----------------------- | ------------------------ | -------------------------------------------- | ---- | ------------ | ----------------- |
| `style`         | Used to style and layout the `Slider`. See `StyleSheet.js` and `ViewStylePropTypes.js` for more info.    | View.style  | No   | All      | yes       |
| `disabled`      | If true the user won't be able to move the slider.<br/>Default value is false. | bool    | No   | All      | yes       |
| `maximumValue`      | Initial maximum value of the slider.<br/>Default value is 1.                      | number      | No   | All      | yes       |
| `minimumTrackTintColor` | The color used for the track to the left of the button.<br/>Overrides the default blue gradient image on iOS.  | [color](https://reactnative.dev/docs/colors) | No   | All      | yes       |
| `minimumValue`      | Initial minimum value of the slider.<br/>Default value is 0.       | number      | No   | All      | yes       |
| `lowerLimit`        | Slide lower limit. The user won't be able to slide below this limit.              | number      | No   | Android, iOS | yes      |
| `upperLimit`        | Slide upper limit. The user won't be able to slide above this limit.              | number      | No   | Android, iOS | yes        |
| `onSlidingStart`    | Callback that is called when the user picks up the slider.<br/>The initial value is passed as an argument to the callback handler.       | function    | No   | All      | yes       |
| `onSlidingComplete`     | Callback that is called when the user releases the slider, regardless if the value has changed.<br/>The current value is passed as an argument to the callback handler.    | function    | No   | All      | yes       |
| `onValueChange`     | Callback continuously called while the user is dragging the slider.| function    | No   | All      | yes       |
| `step`          | Step value of the slider. The value should be between 0 and (maximumValue - minimumValue). Default value is 0.<br/>On Windows OS the default value is 1% of slider's range (from `minimumValue` to `maximumValue`).       | number      | No   | All      | yes       |
| `maximumTrackTintColor` | The color used for the track to the right of the button.<br/>Overrides the default gray gradient image on iOS.        | [color](https://reactnative.dev/docs/colors) | No   | All      | yes       |
| `value`         | Write-only property representing the value of the slider. Can be used to programmatically control the position of the thumb. Entered once at the beginning still acts as an initial value. Changing the value programmatically does not trigger any event.<br/>The value should be between minimumValue and maximumValue, which default to 0 and 1 respectively. Default value is 0.<br/>_This is not a controlled component_, you don't need to update the value during dragging. | number      | No   | All      | yes       |
| `tapToSeek`         | Permits tapping on the slider track to set the thumb position.<br/>Defaults to false on iOS. No effect on Android or Windows.       | bool    | No   | iOS      | no        |
| `inverted`      | Reverses the direction of the slider.<br/>Default value is false.  | bool    | No   | All      | yes       |
| `vertical`      | Changes the orientation of the slider to vertical, if set to `true`.<br/>Default value is false.   | bool    | No   | Windows      | yes       |
| `thumbTintColor`    | Color of the foreground switch grip.<br/>**NOTE:** This prop will override the `thumbImage` prop set, meaning that if both `thumbImage` and `thumbTintColor` will be set, image used for the thumb may not be displayed correctly!| [color](https://reactnative.dev/docs/colors) | No   | Android      | yes       |
| `maximumTrackImage`     | Assigns a maximum track image. Only static images are supported. The leftmost pixel of the image will be stretched to fill the track.              | Image<br/>.propTypes<br/>.source         | No   | iOS      | no        |
| `minimumTrackImage`     | Assigns a minimum track image. Only static images are supported. The rightmost pixel of the image will be stretched to fill the track.             | Image<br/>.propTypes<br/>.source         | No   | iOS      | no        |
| `thumbImage`        | Sets an image for the thumb. Only static images are supported. Needs to be a URI of a local or network image; base64-encoded SVG is not supported.     | Image<br/>.propTypes<br/>.source         | No   | All      | yes       |
| `trackImage`        | Assigns a single image for the track. Only static images are supported. The center pixel of the image will be stretched to fill the track.         | Image<br/>.propTypes<br/>.source         | No   | iOS      | no        |
| `ref`           | Reference object. | MutableRefObject                     | No   | web      | no        |
| `View`          | [Inherited `View` props...](https://github.com/facebook/react-native-website/blob/master/docs/view.md#props)      |         |      |      |  |
| `StepMarker`<sup>5.0.1+</sup> | Component to be rendered for each step on the track,<br/> with the possibility to change the styling, when thumb is at that given step. | FC\<MarkerProps\> | No | iOS, Android, Windows | yes |
| `renderStepNumber`<sup>5.0.1+</sup> | Turns on the displaying of numbers of steps.<br/>Numbers of steps are displayed under the track. | bool | No | iOS, Android, Windows | yes |

## StepMarker<sup>5.0.1+</sup>

Your custom component rendered for every step on the Slider, both the thumb and the rest of steps along the Slider's whole length. This StepMarker prop accepts your custom component and provides it with the following parameters:

| Name         | Description                                                  | Type    | Required | Platform              | HarmonyOS Support |
| ------------ | ------------------------------------------------------------ | ------- | -------- | --------------------- | ----------------- |
| stepMarked   | Indicates whether that custom step is the one that the thum is currently on. If user drags or clicks on that step, thumb will be moved there and the stepMarked parameter will be set to true. Use it, to differentiate between rendering your custom thumb component, or your custom step marker. | boolean | No       | iOS, Android, Windows | yes               |
| currentValue | Contains the `number` type saying at which value of the Slider the thumb currently is. Use it, for example, to render the Slider value on every step marker, or to render different step marker's variant depending on the Thumb position. | number  | No       | iOS, Android, Windows | yes               |
| index        | Contains the index at which this exact instantiation of your custom step marker was rendered at. Use it if you would like to render step number within the step marker, or, for example, if you want to render many variants of step marker depending on their positions along the Slider's width. | number  | No       | iOS, Android, Windows | yes               |
| min          | Minimum value of the Slider. It is equal to minimumValue and has the same default if not set. | number  | No       | iOS, Android, Windows | yes               |
| max          | Maximum value of the Slider. It is equal to maximumValue and has the same default if not set. | number  | No       | iOS, Android, Windows | yes               |

## Known Issues

- [x] upperLimit 和 lowerLimit 只对数值生效，滑动限制不生效: [issue#2](https://github.com/react-native-oh-library/react-native-slider/issues/2)
- [ ] 不支持滑轨设置图片: [issue#3](https://github.com/react-native-oh-library/react-native-slider/issues/3)
- [ ] 未适配无障碍: [issue#9](https://github.com/react-native-oh-library/react-native-slider/issues/9)
- [ ] 不支持点击滑块轨道来设置拇指位置，不支持指定最大轨迹图像，不支持分配最小轨道图像: [issue#10](https://github.com/react-native-oh-library/react-native-slider/issues/10)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/callstack/react-native-slider/blob/main/LICENSE.md).
