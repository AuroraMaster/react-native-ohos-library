> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-oh-tpl/react-native-screens</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-screens">
        <img src="https://img.shields.io/badge/platforms-iOS%20|%20Android%20|%20tvOS%20|%20Windows%20|%20Web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/software-mansion/react-native-screens/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-harmony-screens)

## Installation and Usage

### 3.34.0
The implementation of this library depends on the native  code from @react-navigation/native and @react-navigation/native-stack and @react-native-oh-tpl/react-native-safe-area-context and @react-native-oh-tpl/react-native-gesture-handler. If this library is included into your application, there is no need to include it again; you can skip the steps in this section and use it directly.

Note: If the `@react-native-oh-tpl/native-stack` library has been introduced, please uninstall it. Otherwise, this library will fail to be referenced and cannot be used.

If it is not included, follow the guide provided in [@react-navigation/native](/en/react-navigation-native.md) and [@react-native-oh-tpl/react-native-safe-area-context](/en/react-native-safe-area-context.md) and [@react-native-oh-tpl/react-native-gesture-handler](/en/react-native-gesture-handler.md) to add it to your project.

### 3.34.1
The implementation of this library depends on the native  code from @react-navigation/native and @react-navigation/native-stack and @react-native-ohos/react-native-safe-area-context and @react-native-ohos/react-native-gesture-handler and @react-native-ohos/react-native-reanimated. If this library is included into your application, there is no need to include it again; you can skip the steps in this section and use it directly.

Note: If the `@react-native-oh-tpl/native-stack，@react-native-ohos/native-stack` library has been introduced, please uninstall it. Otherwise, this library will fail to be referenced and cannot be used.

If it is not included, follow the guide provided in [@react-navigation/native](/en/react-navigation-native.md) and [@react-native-ohos/react-native-safe-area-context](/en/react-native-safe-area-context.md) and [@react-native-ohos/react-native-gesture-handler](/en/react-native-gesture-handler.md)  and [@react-native-ohos/react-native-reanimated](/en/react-native-reanimated.md) to add it to your project.

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 3.34.0@deprecated  | [@react-native-oh-tpl/react-native-screens Releases(deprecated)](https://github.com/react-native-oh-library/react-native-harmony-screens/releases) | 0.72       |
| 3.34.1             | [@react-native-ohos/react-native-screens Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-screens/releases)   | 0.72       |
| 4.8.1              | [@react-native-ohos/react-native-screens Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-screens/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Go to the project directory and execute the following instruction:
#### **npm**

```bash
# 0.72
npm install @react-native-ohos/react-native-screens@3.34.1-X.X.X
npm install @react-navigation/native-stack@6.9.13

# 0.77
npm install @react-native-ohos/react-native-screens@4.8.1-X.X.X
npm install @react-navigation/native-stack@7.2.0
```

#### **yarn**

```bash
# 0.72
yarn install @react-native-ohos/react-native-screens@3.34.1-X.X.X
yarn install @react-navigation/native-stack@6.9.13

# 0.77
yarn install @react-native-ohos/react-native-screens@4.8.1-X.X.X
yarn install @react-navigation/native-stack@7.2.0
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from 'react';
import { Button, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import { enableScreens } from "react-native-screens";
enableScreens(true);

function HomeScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button
        title="Go to Profile"
        onPress={() => navigation.navigate('Profile')}
      />
    </View>
  );
}

function ProfileScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button
        title="Go to Notifications"
        onPress={() => navigation.navigate('Notifications')}
      />
      <Button title="Go back" onPress={() => navigation.goBack()} />
    </View>
  );
}

function NotificationsScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button
        title="Go to Settings"
        onPress={() => navigation.navigate('Settings')}
      />
      <Button title="Go back" onPress={() => navigation.goBack()} />
    </View>
  );
}

function SettingsScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button title="Go back" onPress={() => navigation.goBack()} />
    </View>
  );
}

const Stack = createNativeStackNavigator();

function MyStack() {
  return (
    <Stack.Navigator
      initialRouteName="Home"
      screenOptions={{
        headerTintColor: '#999999',
        headerStyle: { backgroundColor: '#ff00ff' },
      }}
    >
      <Stack.Screen name="Home" component={HomeScreen} />
      <Stack.Screen name="Notifications" component={NotificationsScreen} />
      <Stack.Screen name="Profile" component={ProfileScreen} />
      <Stack.Screen name="Settings" component={SettingsScreen} />
    </Stack.Navigator>
  );
}

export default function App() {
  return (
    <NavigationContainer>
      <MyStack />
    </NavigationContainer>
  );
}

```


## Use Codegen

Version >= @react-native-ohos/react-native-screens@3.34.1, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-screens@3.34.1 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:../node_modules/@rnoh/react-native-harmony/harmony/react_native_openharmony.har"
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
    "@rnoh/react-native-openharmony": "file:../../node_modules/@rnoh/react-native-harmony/harmony/react_native_openharmony.har",
    "@react-native-ohos/react-native-screens": "file:../../node_modules/@react-native-ohos/react-native-screens/harmony/screens.har"
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

### 3. Configuring CMakeLists and Introducing Package

> V3.34.1 requires configuring CMakeLists and importing RnohReactNativeHarmonyScreensPackage.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
+ set(OH_MODULES_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES_DIR}/@react-native-ohos/react-native-screens/src/main/cpp" ./rnoh_screens)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_screens)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp`, add:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "RnohReactNativeHarmonyScreensPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+        std::make_shared<rnoh::RnohReactNativeHarmonyScreensPackage>(ctx),
    };
}
```

### 4. Introducing Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { componentBuilder } from "@react-native-ohos/react-native-screens"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
  Stack() {
+    componentBuilder(ctx)
  }
  ...
}
...
```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added. 

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
+ "RNSScreen", 
+ "RNSFullWindowOverlay", 
+ "RNSModalScreen", 
+ "RNSScreenContainer", 
+ "RNSScreenNavigationContainer", 
+ "RNSScreenStack", 
+ "RNSScreenStackHeaderSubview", 
+ "RNSSearchBar", 
+ "RNSScreenStackHeaderConfig", 
+ "RNSScreenStackHeaderSubview"
];
```

### 5. Introducing Package to ArkTS

Open `src/main/ets/RNOHPackagesFactory.ets`, add:

```diff
import type { RNPackageContext, RNPackage } from '@rnoh/react-native-openharmony';
+ import RnohReactNativeHarmonyScreensPackage from '@react-native-ohos/react-native-screens';

export function createRNOHPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+    new RnohReactNativeHarmonyScreensPackage(ctx),
  ];
}

```

### 6. Running

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

Verified successfully in the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 5.1.0.150 (API Version 12); IDE: DevEco Studio 5.1.1.830; ROM: 5.1.0.150;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 5.0.0.71(API Version 12 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 5.1.0.150;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                                      | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| --------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| enableScreens                                             | Support native and its React Native View                               | function | No       | iOS Android | Yes               |
| enableFreeze                                              | Support for react-freeze, using ReactSuspende mechanism to prevent partial rendering of React component tree  | function | No       | iOS Android | Yes               |
| createNativeStackNavigator                                | Provides screen switching capabilities.                                          | function | No       | iOS Android | NO                |
| NativeStackNavigationProp                                 | Encapsulates the property of page switching.                                          | object   | No       | iOS Android | Yes               |
| NativeStackNavigationOptions                              | Encapsulates the property settings of the navigation bar.                                          | object   | No       | iOS Android | NO                |
| FullWindowOverlay                                         | A component that allows placing its child components above other components.                    | object   | No       | iOS Android | NO                |
| SearchBarProps                                            | Encapsulates the property settings of the search bar.                                        | object   | No       | iOS Android | NO                |
| SearchBarCommands                                         | Encapsulates the operations of the search bar.                                            | object   | No       | iOS Android | NO                |
| useTransitionProgress                                     | Provides an animation interpolator for screen transitions.                                    | function | No       | iOS Android | NO                |
| userReanimatedTransitionProgress ReanimatedScreenProvider | Frame callback called during screen transitions, used for react-native-reanimated 2.0 and above, encapsulated with **ReanimatedScreenProvider**.| function | No       | iOS Android | NO                |
| userHeaderHeight                                          | Calculates the height of the static header bar. This value changes when the screen orientation changes.    | function | No       | iOS Android | NO                |
| userAnimatedHeaderHeight                                  | Dynamically calculates the height of the header bar. This value changes with each view layout change.      | function | No       | iOS Android | NO                |
| onAppear                                 | A callback that gets called when the current screen appears        | function | No       | iOS Android |   Yes |
| onDisappear                              | A callback that gets called when the current screen disappears.    | function | No       | iOS Android |   Yes |
| onWillAppear                             | A callback that gets called when the current screen will appear       | function | No       | iOS Android |   Yes |
| onWillDisappear                          | A callback that gets called when the current screen will disappear       | function | No       | iOS Android |   Yes |
| fullScreenSwipeEnabled                   | Boolean indicating whether the swipe gesture should work on whole screen         | property | No       | iOS Android |   Yes |
| gestureEnabled                           |  Whether you can use gestures to dismiss this screen | property | No       | iOS Android |   Yes |
| statusBarColor                           | Sets the status bar color       | property | No       | iOS Android |   No  |
| screenOrientation                        | In which orientation should the screen appear     | property | No       | iOS Android |   Yes |
| statusBarStyle                           | Sets the status bar color       | property | No       | iOS Android |   Yes |
| statusBarTranslucent                     | Sets the translucency of the status bar       | property | No       | iOS Android | Yes |
| statusBarHidden			   | Whether the status bar should be hidden on this screen       | property | No       | iOS Android |   Yes |
| gestureResponseDistance                  |  Use it to restrict the distance from the edges of screen in which the gesture should be recognized      | property | No       | iOS Android |   Yes |
| stackPresentation                        | how should the screen be presented       | property | No       | iOS Android |   Yes |
| stackAnimation                           | ow the screen should appear/disappear when pushed or popped at the top of the stack       | property | No       | iOS Android |   Yes |
| replaceAnimation                         | How should the screen replacing another screen animate       | property | No       | iOS Android |   Yes |
| backgroundColor                          | Controls the color of the navigation header       | property | No       | iOS Android |   Yes |
| hidden                           | When set to true the header will be hidden while the parent Screen is on the top of the stack       | property | No       | iOS Android |   Yes |
| translucent                      | Boolean indicating whether the navigation bar is translucent       | property | No       | iOS Android |   Yes |
| hideBackButton                   | Boolean indicating whether to hide the back button in header      | property | No       | iOS Android |   Yes |
| backTitle                        | Title to display in the back button.       | property | No       | iOS Android |   Yes |
| backTitleFontSize                | Allows for customizing font size to be used for back button title    | property | No       | iOS Android |   Yes |
| backTitleVisible                 |  Whether the back button title should be visible or nots    | property | No       | iOS Android |   Yes |
| backTitleVisible<sup>4.8.1</sup>                 |  Whether the back button title should be visible or nots    | property | No       | iOS Android |   No |
| title                            | String that can be displayed in the header as a fallback for `headerTitle`       | property | No       | iOS Android |   Yes |
| titleFontSize                    | Customize the size of the font to be used for the title.        | property | No       | iOS Android |   Yes |
| titleFontWeight                  | Customize the weight of the font to be used for the title.       | property | No       | iOS Android |   Yes |
| titleColor                       | Allows for setting text color of the title | property | No       | iOS Android |   Yes |
| type                             | Subtitle type      | property | No       | iOS Android |   Yes |
| onSearchFocus                    | Search bar focus       | function | No       | iOS Android |   Yes |
| onSearchBlur                     | Search bar loses focus       | function | No       | iOS Android |   Yes |
| onSearchButtonPress              | A callback that gets called when the search button is pressed       | function | No       | iOS Android |   Yes |
| onCancelButtonPress              | A callback that gets called when the cancel button is pressed       | function | No       | iOS Android |   Yes |
| onChangeText                     | A callback that gets called when the text changes       | function | No       | iOS Android |   Yes |
| cancelButtonText                 | The text to be used instead of default `Cancel` button text       | property | No       | iOS Android |   Yes |
| barTintColor                     | The search field background color       | property | No       | iOS Android |   Yes |
| tintColor                        | The color for the cursor caret and cancel button text       | property | No       | iOS Android |   Yes |
| textColor                        | text color       | property | No       | iOS Android |   Yes |
| inputType                        | Sets type of the input. Defaults to `text`.       | property | No       | iOS Android |   Yes |
| onClose                          | A callback that gets called when search bar is closed       | function | No       | iOS Android |   Yes |
| onOpen                           | A callback that gets called when search bar is opened       | function | No       | iOS Android |   Yes |
| headerIconColor                  | The search and close icon color shown in the header       | property | No       | iOS Android |   Yes |
| shouldShowHintSearchIcon         | Show the search hint icon when search bar is focused       | property | No       | iOS Android |   Yes |
| blurEffect<sup>4.8.1</sup>       | Blur effect to be applied to the header.       | property | No       | iOS  |   Yes |
| tintColor<sup>4.8.1</sup>         | The color for the cursor caret and cancel button text       | property | No       | iOS  |   Yes |
| color<sup>4.8.1</sup>         | Controls the color of items rendered on the header. This includes back icon, back text (iOS only) and title text. If you want the title to have different color use titleColor property.       | property | No       | iOS Android |   Yes |
| hideWhenScrolling<sup>4.8.1</sup>         | Boolean indicating whether to hide the search bar when scrolling. Defaults to `true`.        | property | No       | iOS  |   No |
| largeTitle<sup>4.8.1</sup>         | When set to `true`, it makes the title display using the large title effect.       | property | No       | iOS  |   No |
| largeTitleFontFamily<sup>4.8.1</sup>          | Customize font family to be used for the large title.       | property | No       | iOS  |   No |
| largeTitleFontSize<sup>4.8.1</sup>         | Customize the size of the font to be used for the large title.       | property | No       | iOS  |   No |
| largeTitleFontWeight<sup>4.8.1</sup>         | Customize the weight of the font to be used for the large title.       | property | No       | iOS  |   No |
| largeTitleHideShadow<sup>4.8.1</sup>         | Boolean that allows for disabling drop shadow under navigation header when the edge of any scrollable content reaches the matching edge of the navigation bar.       | property | No       | iOS  |   No |
| largeTitleColor<sup>4.8.1</sup>         | Customize the color to be used for the large title. By default uses the `titleColor` property.       | property | No       | iOS  |   No |
| autoCapitalize<sup>4.8.1</sup>         |  Controls whether the text is automatically auto-capitalized as it is entered by the user.      | property | No       | iOS Android  |   No |
| placement<sup>4.8.1</sup>         | Placement of the search bar in the navigation bar.       | property | No       | iOS  |   No |
| obscureBackground<sup>4.8.1</sup>         |  Boolean indicating whether to obscure the underlying content with semi-transparent overlay. Defaults to `true`.        | property | No       | iOS  |   No |
| hideNavigationBar<sup>4.8.1</sup>         |  Boolean indicating whether to hide the navigation bar during searching. Defaults to `true`.      | property | No       | iOS  |   No |
| disableBackButtonOverride<sup>4.8.1</sup>         |  Default behavior is to prevent screen from going back when search bar is open (`disableBackButtonOverride: false`). If you don't want this to happen set `disableBackButtonOverride` to `true`.      | property | No       | Android  |   No |
| customAnimationOnSwipe<sup>4.8.1</sup>         | Boolean indicating that swipe dismissal should trigger animation provided by `stackAnimation`. Defaults to `false`.       | property | No       | iOS  |   No |
| fullScreenSwipeShadowEnabled<sup>4.8.1</sup>         | Boolean indicating whether the full screen dismiss gesture has shadow under view during transition. The gesture uses custom transition and thus doesn't have a shadow by default. When enabled, a custom shadow view is added during the transition which tries to mimic the default iOS shadow. Defaults to `true`.       | property | No       | iOS  |   No |
| homeIndicatorHidden<sup>4.8.1</sup>         |  Whether the home indicator should be hidden on this screen. Defaults to `false`.      | property | No       | iOS  |   No |
| statusBarAnimation<sup>4.8.1</sup>         | Sets the status bar animation (similar to the `StatusBar` component). Requires enabling (or deleting) `View controller-based status bar appearance` in your Info.plist file.  On Android, this prop considers the transition of changing status bar color . There will be no animation if `none` provided.       | property | No       | iOS Android |   No |
| transitionDuration<sup>4.8.1</sup>         | Changes the duration (in milliseconds) of `slide_from_bottom`, `fade_from_bottom`, `fade` and `simple_push` transitions on iOS. Defaults to `500`. The duration of `default` and `flip` transitions isn't customizable.       | property | No       | iOS  |   No |
| hideKeyboardOnSwipe<sup>4.8.1</sup>         | Whether the keyboard should hide when swiping to the previous screen. Defaults to `false`.       | property | No       | iOS  |   No |
| disableBackButtonMenu<sup>4.8.1</sup>         | Boolean indicating whether to show the menu on longPress of iOS >= 14 back button.        | property | No       | iOS  |   No |
| backButtonDisplayMode<sup>4.8.1</sup>         | Enum value indicating display mode of **default** back button. It works on iOS >= 14, and is used only when none of: `backTitleFontFamily`, `backTitleFontSize`, `disableBackButtonMenu` or `backTitle` is set. Otherwise, when the button is customized, under the hood we use iOS native `backButtonItem` which overrides `backButtonDisplayMode`.       | property | No       | iOS  |   No |
| backButtonInCustomView<sup>4.8.1</sup>         |  Whether to show the back button with a custom left side of the header.      | property | No       | iOS  |   No |
| direction        | Controls whether the stack should be in `rtl` or `ltr` form.       | property | No       | iOS Android  |   No |
| topInsetEnabled<sup>4.8.1</sup>         | A flag to that lets you opt out of insetting the header. You may want to set this to `false` if you use an opaque status bar. Defaults to `true`.       | property | No       | Android  |   No |

## Known Issues
- [ ] The formSheet page is currently using a regular page, and the Context.openBindSheet system method used on this page has a misalignment of the binding position of the JS page, resulting in unresponsive button events. Need to be supplemented after system correction.  [issue#4](https://github.com/react-native-oh-library/react-native-harmony-screens/issues/4)

- [ ] RNSScreenFooter depends on formSheet. This function needs to be added after the formSheet function is implemented.  [issue#28](https://github.com/react-native-oh-library/react-native-harmony-screens/issues/28)

- [ ] GestureDetectorProvider cannot be referenced in the 77 environment according to the original library reference method, and requires system framework positioning processing。  [issue#29](https://github.com/react-native-oh-library/react-native-harmony-screens/issues/29)

- [ ] When different properties are set in Option in Screen and its subcomponents, the properties received by ETS side in 77 environment are lost. System framework positioning processing is required.  [issue#30](https://github.com/react-native-oh-library/react-native-harmony-screens/issues/30)

- [ ] sheetInitialDetent: Index of the detent the sheet should expand to after being opened. Attributes of the formsheet function. Not implemented
- [ ] sheetElevation: Integer value describing elevation of the sheet, impacting shadow on the top edge of the sheet.Attributes of the formsheet function. Not implemented
- [ ] sheetAllowedDetents:  Describes heights where a sheet can rest. Attributes of the formsheet function. Not implemented
- [ ] sheetLargestUndimmedDetent: The largest sheet detent for which a view underneath won't be dimmed. Attributes of the formsheet function. Not implemented
- [ ] sheetGrabberVisible: Boolean indicating whether the sheet shows a grabber at the top. Attributes of the formsheet function. Not implemented
- [ ] sheetCornerRadius: The corner radius that the sheet will try to render with. Attributes of the formsheet function. Not implemented
- [ ] sheetExpandsWhenScrolledToEdge: Whether the sheet should expand to larger detent when scrolling. Attributes of the formsheet function. Not implemented
- [ ] onSheetDetentChanged: A callback that gets called when the current screen is in `formSheet` presentation and its detent has changed. Callback for formsheet function. Not implemented

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/software-mansion/react-native-screens/blob/main/LICENSE).
