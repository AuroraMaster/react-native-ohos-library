> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-navigation/native-stack</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/main/packages/native-stack">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/main/packages/native-stack/LICENSE">
         <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/native-stack)

The repository for this third-party library has been migrated to Gitcode, and it now supports direct download from npm. The new package name is: `@react-native-ohos/native-stack`. The specific version relationships are as follows:

| Version                        | Package Name                             | Repository                                                   | Release                                                      | Version for RN |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 6.9.26 | @react-native-oh-tpl/native-stack  | [Github](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/native-stack) | [Github Releases](https://github.com/react-native-oh-library/react-navigation/releases) | 0.72       |
| 7.3.11                        | @react-native-ohos/native-stack | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-navigation/tree/br_rnoh0.77/packages/native-stack) | [GitCode Releases]() | 0.77       |

For older versions that have not been released to npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

### **npm**

```bash
# for RN0.72
npm install @react-native-oh-tpl/native-stack

# for RN0.77
npm install @react-native-ohos/native-stack
```

### **yarn**

```bash
# for RN0.72
yarn install @react-native-oh-tpl/native-stack

# for RN0.77
yarn install @react-native-ohos/native-stack
```

<!-- tabs:end -->

The following code demonstrates the basic usage scenarios of this library:

```tsx
import * as React from 'react';
import { Button, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import { enableScreens } from "react-native-screens";
enableScreens(false);

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
        headerTintColor: 'white',
        headerStyle: { backgroundColor: 'tomato' },
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

## Link

This library relies on the following third-party libraries, please refer to the corresponding documentation:
+ [react-native-screens](/zh-cn/react-native-screens.md)
+ [native](/zh-cn/react-navigation-native.md)
+ [elements](/zh-cn/react-navigation-elements.md)
+ [react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)

The HarmonyOS implementation of this library relies on the native code of react-native-safe-area-context. If the library has already been introduced in the HarmonyOS project, there is no need to introduce it again. You can skip the steps in this chapter and use it directly.

If not introduced, please refer to [Link chapter of document react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md#link)for introduction

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following version:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

The following attributes have been verified. For more details on the attributes, please refer to [document  react-navigation/native-stack](https://reactnavigation.org/docs/native-stack-navigator)

**Props**
| Name             | Description                                                                                                                       | Type   | Required | Platform | HarmonyOS Support |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------|--------|----------|----------|-------------------|
| id               | Optional unique ID for the navigator. This can be used with navigation.getParent to refer to this navigator in a child navigator. | string | no       | all      | yes               |
| initialRouteName | The name of the route to render on first load of the navigator.                                                                   | string | no       | all      | yes               |
| screenOptions    | Default options to use for the screens in the navigator.                                                                          | object | no       | all      | yes               |
| layout<sup>7.3.10+</sup>          | A  layout is a wrapper around the navigator. It can be useful for augmenting the  navigators with additional UI with a wrapper.The difference from adding a  wrapper around the navigator manually is that the code in a layout callback  has access to the navigator's state, options etc. | object | no       | all      | yes               |
| screenLayout<sup>7.3.10+</sup>    | A  screen layout is a wrapper around each screen in the navigator. It makes it  easier to provide things such as an error boundary and suspense fallback for  all screens in the navigator, or wrap each screen with additional UI. | object | no       | all      | yes               |
| screenListeners<sup>7.3.10+</sup> | You can pass a prop named `screenListeners` to the navigator component, where you can specify listeners for events from all screens for this navigator. | object | no       | all      | yes               |

**Options & screenOptions**
| Name                          | Description                                                                                                                                                                                                                                                                                                                                  | Type                                                                                                                                     | Required | Platform    | HarmonyOS Support |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|----------|-------------|-------------------|
| title                         | String that can be used as a fallback for headerTitle.                                                                                                                                                                                                                                                                                       | string                                                                                                                                   | no       | all         | yes               |
| headerBackButtonMenuEnabled   | Boolean indicating whether to show the menu on longPress of iOS >= 14 back button. Defaults to true.                                                                                                                                                                                                                                         | boolean                                                                                                                                  | no       | iOS         | no                |
| headerBackVisible             | Whether the back button is visible in the header. You can use it to show a back button alongside headerLeft if you have specified it.                                                                                                                                                                                                        | boolean                                                                                                                                  | no       | Android,iOS | no                |
| headerBackTitle               | Title string used by the back button on iOS. Defaults to the previous scene's title, or "Back" if there's not enough space. Use headerBackTitleVisible: false to hide it.                                                                                                                                                                    | string                                                                                                                                   | no       | iOS         | no                |
| headerBackTitleStyle          | Style object for header back title.                                                                                                                                                                                                                                                                                                          | object                                                                                                                                   | no       | iOS         | no                |
| headerBackImageSource         | Image to display in the header as the icon in the back button.                                                                                                                                                                                                                                                                               | string                                                                                                                                   | no       | all         | yes               |
| headerLargeStyle              | Style of the header when a large title is shown.                                                                                                                                                                                                                                                                                             | object                                                                                                                                   | no       | iOS         | no                |
| headerLargeTitle              | Whether to enable header with large title which collapses to regular header on scroll.                                                                                                                                                                                                                                                       | string                                                                                                                                   | no       | iOS         | no                |
| headerLargeTitleShadowVisible | Whether drop shadow of header is visible when a large title is shown.                                                                                                                                                                                                                                                                        | boolean                                                                                                                                  | no       | iOS         | no                |
| headerLargeTitleStyle         | Style object for large title in header.                                                                                                                                                                                                                                                                                                      | object                                                                                                                                   | no       | iOS         | no                |
| headerShown                   | Whether to show the header. The header is shown by default. Setting this to false hides the header.                                                                                                                                                                                                                                          | boolean                                                                                                                                  | no       | all         | yes               |
| headerStyle                   | Style object for header.                                                                                                                                                                                                                                                                                             | object                                                                                                                                   | no       | all         | yes               |
| headerShadowVisible           | Whether to hide the elevation shadow (Android) or the bottom border (iOS) on the header.                                                                                                                                                                                                                                                     | object                                                                                                                                   | no       | Android，iOS | yes               |
| headerTransparent             | Boolean indicating whether the navigation bar is translucent.                                                                                                                                                                                                                                                                                | boolean                                                                                                                                  | no       | all         | yes               |
| headerBlurEffect              | Blur effect for the translucent header. The headerTransparent option needs to be set to true for this to work.                                                                                                                                                                                                                               | string                                                                                                                                   | no       | iOS         | no                |
| headerBackground              | Function which returns a React Element to render as the background of the header. This is useful for using backgrounds such as an image or a gradient.                                                                                                                                                                                       | function                                                                                                                                 | no       | all         | yes               |
| headerTintColor               | Tint color for the header. Changes the color of back button and title.                                                                                                                                                                                                                                                                       | string                                                                                                                                   | no       | all         | yes               |
| headerLeft                    | Function which returns a React Element to display on the left side of the header. This replaces the back button. See headerBackVisible to show the back button along side left element.                                                                                                                                                      | function                                                                                                                                 | no       | all         | yes               |
| headerRight                   | Function which returns a React Element to display on the right side of the header.                                                                                                                                                                                                                                                           | function                                                                                                                                 | no       | all         | yes               |
| headerTitle                   | String or a function that returns a React Element to be used by the header. Defaults to title or name of the screen.                                                                                                                                                                                                                         | string&#124;function                                                                                                                          | no       | all         | yes               |
| headerTitleAlign              | How to align the header title.Defaults to left on platforms other than iOS.Not supported on iOS. It's always center on iOS and cannot be changed.                                                                                                                                                                                            | 'left'&#124;'right'                                                                                                                            | no       | Android     | yes               |
| headerTitleStyle              | Style object for header title.                                                                                                                                                                                                                                                                                                               | object                                                                                                                                   | no       | all         | yes               |
| headerSearchBarOptions        | Options to render a native search bar on iOS.                                                                                                                                                                                                                                                                                                | object                                                                                                                                   | no       | Android，iOS | no                |
| header                        | Custom header to use instead of the default header.                                                                                                                                                                                                                                                                                          | function                                                                                                                                 | no       | all         | no                |
| statusBarAnimation            | Sets the status bar animation (similar to the StatusBar component). Defaults to fade on iOS and none on Android.                                                                                                                                                                                                                             | 'fade'&#124;'none'&#124;'slide'                                                                                                           | no       | Android，iOS | no                |
| statusBarHidden               | Whether the status bar should be hidden on this screen.                                                                                                                                                                                                                                                                                      | boolean                                                                                                                                  | no       | Android，iOS | no                |
| statusBarStyle                | Sets the status bar color (similar to the StatusBar component). Defaults to auto.                                                                                                                                                                                                                                                            | string                                                                                                                                   | no       | Android，iOS | no                |
| statusBarColor                | Sets the status bar color (similar to the StatusBar component). Defaults to initial status bar color.                                                                                                                                                                                                                                        | string                                                                                                                                   | no       | Android     | no                |
| statusBarTranslucent          | Sets the translucency of the status bar (similar to the StatusBar component). Defaults to false.                                                                                                                                                                                                                                             | boolean                                                                                                                                  | no       | Android     | no                |
| contentStyle                  | Style object for the scene content.                                                                                                                                                                                                                                                                                                          | object                                                                                                                                   | no       | all         | yes               |
| customAnimationOnGesture<sup>deprecated from 7.3.10 </sup>> | Whether the gesture to dismiss should use animation provided to animation prop. Defaults to false. | boolean                                                      | no       | iOS          | no                |
| fullScreenGestureEnabled      | Whether the gesture to dismiss should work on the whole screen. Using gesture to dismiss with this option results in the same transition animation as simple_push. This behavior can be changed by setting customAnimationOnGesture prop. Achieving the default iOS animation isn't possible due to platform limitations. Defaults to false. | boolean                                                                                                                                  | no       | iOS         | no                |
| gestureEnabled                | Whether you can use gestures to dismiss this screen. Defaults to true.                                                                                                                                                                                                                                                                       | boolean                                                                                                                                  | no       | iOS         | no                |
| animationTypeForReplace       | The type of animation to use when this screen replaces another screen. Defaults to pop.                                                                                                                                                                                                                                                      | 'push'&#124;'pop'                                                                                                                         | no       | Android，iOS | no                |
| animation                     | How the screen should animate when pushed or popped.                                                                                                                                                                                                                                                                                         | 'default'&#124;'fade'&#124;'fade_from_bottom'&#124;'fade_from_bottom'&#124;'simple_push'&#124;'slide_from_bottom'&#124;'slide_from_right'&#124;'slide_from_left'&#124;'none'      | no       | Android,iOS | no                |
| presentation                  | How should the screen be presented.                                                                                                                                                                                                                                                                                                          | 'card'&#124;'modal'&#124;'transparentModal'&#124;'containedModal'&#124;'containedModal'&#124;'fullScreenModal'&#124;'formSheet'           | no       | Android，iOS | partially('card'/'transparentModal')        |
| orientation                   | The display orientation to use for the screen.                                                                                                                                                                                                                                                                                               | 'default'&#124;'all'&#124;'portrait'&#124;'portrait_up'&#124;'portrait_down'&#124;'landscape'&#124;'landscape_left'&#124;'landscape_left' | no       | Android，iOS | no                |
| autoHideHomeIndicator         | Boolean indicating whether the home indicator should prefer to stay hidden. Defaults to false.                                                                                                                                                                                                                                               | boolean                                                                                                                                  | no       | iOS         | no                |
| gestureDirection              | Sets the direction in which you should swipe to dismiss the screen.                                                                                                                                                                                                                                                                          | 'vertical '&#124;'horizontal '                                                                                                            | no       | iOS         | no                |
| animationDuration             | Changes the duration (in milliseconds) of slide_from_bottom, fade_from_bottom, fade and simple_push transitions on iOS. Defaults to 350.                                                                                                                                                                                                     | number                                                                                                                                  | no       | iOS         | no                |
| navigationBarColor            | Sets the navigation bar color. Defaults to initial status bar color.                                                                                                                                                                                                                                                                         | string                                                                                                                                   | no       | Android     | no                |
| navigationBarHidden           | Boolean indicating whether the navigation bar should be hidden. Defaults to false.                                                                                                                                                                                                                                                           | boolean                                                                                                                                  | no       | Android     | no                |
| freezeOnBlur                  | Boolean indicating whether to prevent inactive screens from re-rendering. Defaults to false. Defaults to true when enableFreeze() from react-native-screens package is run at the top of the application.                                                                                                                                    | boolean                                                                                                                                  | no       | Android,iOS | no                |
| headerBackButtonDisplayMode<sup>7.3.10+</sup>               | How the back button displays icon and title.                 | 'default' \| 'generic' \| 'minimal '                         | no       | iOS          | yes               |
| animationMatchesGesture<sup>7.3.10+</sup>                   | Whether  the gesture to dismiss should use animation provided to animation prop.  Defaults to false. Doesn't affect the behavior of screens presented modally. | boolean                                                      | no       | iOS          | no                |
| sheetElevation<sup>7.3.10+</sup>                            | Works only when presentation is set to formSheet.<br/>Integer value describing elevation of the sheet, impacting shadow on the top edge of the sheet. | number                                                       | no       | Android      | no                |
| sheetExpandsWhenScrolledToEdge<sup>7.3.10+</sup>            | Works only when presentation is set to formSheet.<br/>Whether the sheet should expand to larger detent when scrolling. | boolean                                                      | no       | iOS          | no                |
| sheetCornerRadius<sup>7.3.10+</sup>                         | Works only when presentation is set to formSheet.<br/>The corner radius that the sheet will try to render with. | number                                                       | no       | Android,iOS  | no                |
| sheetInitialDetentIndex<sup>7.3.10+</sup>                   | Works only when presentation is set to formSheet.<br/>Index of the detent the sheet should expand to after being opened. | number                                                       | no       | Android,iOS  | no                |
| sheetGrabberVisible<sup>7.3.10+</sup>                       | Works only when presentation is set to formSheet.<br/>Boolean indicating whether the sheet shows a grabber at the top. | boolean                                                      | no       | iOS          | no                |
| sheetLargestUndimmedDetentIndex<sup>7.3.10+</sup>           | Works only when presentation is set to formSheet.<br/>The largest sheet detent for which a view underneath won't be dimmed. | 'none' \| 'last'                                             | no       | Android,iOS  | no                |

**Events**

| Name            | Description                                                                      | Type     | Required | Platform | HarmonyOS Support |
|-----------------|----------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| transitionStart | This event is fired when the transition animation starts for the current screen. | function | no       | all      | no                |
| transitionEnd   | This event is fired when the transition animation ends for the current screen.   | function | no       | all      | no                |

**Hooks<sup>7.3.10+</sup>**

| Name                    | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| useAnimatedHeaderHeight | The hook returns an animated value representing the height of the header. | function | no       | all      | yes               |

## Known Issues

- [ ] Function react-native-screens is missing, resulting in the inability to implement attribute functions such as headerSearchBarOptions：[issue#25](https://github.com/react-native-oh-library/react-navigation/issues/25)
- [ ] V7.3.10 Hongmeng side did not implement formSheet, resulting in the formSheet of the presentation not being Hongmeng standardized：[issue#2](https://gitcode.com/openharmony-sig/rntpc_react-navigation/issues/2)
- [ ] V7.3.10 AnimationMatchesGesture did not implement Harmonyization due to dependency on third-party library react-native-screen: [issue#3](https://gitcode.com/openharmony-sig/rntpc_react-navigation/issues/3)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/main/packages/native-stack/LICENSE).