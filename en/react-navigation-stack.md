> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-navigation/stack</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/main/packages/stack">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/main/packages/stack/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/stack)

The repository for this third-party library has been migrated to Gitcode, and it now supports direct download from npm. The new package name is: `@react-native-ohos/stack`. The specific version relationships are as follows:

| Version                        | Package Name                             | Repository                                                   | Release                                                      | Version for RN |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 6.4.0 | @react-native-oh-tpl/stack  | [Github](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/stack) | [Github Releases](https://github.com/react-native-oh-library/react-navigation/releases) | 0.72       |
| 7.2.11                        | @react-native-ohos/stack | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-navigation/tree/br_rnoh0.77/packages/stack) | [GitCode Releases]() | 0.77       |

For older versions that have not been released to npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
# for RN0.72
npm install @react-native-oh-tpl/stack

# for RN0.77
npm install @react-native-ohos/stack
```

#### **yarn**

```bash
# for RN0.72
yarn install @react-native-oh-tpl/stack

# for RN0.77
yarn install @react-native-ohos/stack
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.
```js
import * as React from 'react';
import { Button, Text, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';



const HomeStack = createStackNavigator();

function HomeScreen({ navigation }) {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Home screen</Text>
            <Button
                title="Go to Details"
                onPress={() => navigation.navigate('Details')}
            />
        </View>
    );
}

function DetailsScreen({ navigation }) {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Details!</Text>
            <Button
                title="Go back"
                onPress={() => navigation.goBack()}
            />
        </View>
    );
}



export default function App() {
    return (
        <NavigationContainer>
            <HomeStack.Navigator>
                <HomeStack.Screen name="Home" component={HomeScreen} />
                <HomeStack.Screen name="Details" component={DetailsScreen} />
            </HomeStack.Navigator>
        </NavigationContainer>
    );
}
```

## Link
This repository depends on the following libraries, please refer to the corresponding documentation:
+ [@react-navigation/native](/en/react-navigation-native.md)
+ [@react-native-ohos/react-native-gesture-handler](/en/react-native-gesture-handler.md)
+ [@react-native-ohos/react-native-safe-area-context](/en/react-native-safe-area-context.md)
+ [react-native-screens](/en/react-native-screens.md)

The HarmonyOS implementation of this library depends on the native code from @react-native-ohos/react-native-gesture-handler、@react-native-ohos/react-native-safe-area-context. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-ohos/react-native-gesture-handler](/en/react-native-gesture-handler.md)、[@react-native-ohos/react-native-safe-area-context](/en/react-native-safe-area-context.md) to add it to your project.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following version:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-navigation/stack](https://reactnavigation.org/docs/stack-navigator)


**Props**

| Name                  | Description                                                                                                                                                                        | Type    | Required | Platform    | HarmonyOS Support |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| id                    | Optional unique ID for the navigator. This can be used with navigation.getParent to refer to this navigator in a child navigator.                                                  | string  | no       | all         | yes               |
| initialRouteName      | The name of the route to render on first load of the navigator.                                                                                                                    | string  | no       | all         | yes               |
| screenOptions         | Default options to use for the screens in the navigator.                                                                                                                           | object  | no       | all         | yes               |
| detachInactiveScreens | Boolean used to indicate whether inactive screens should be detached from the view hierarchy to save memory. This enables integration with react-native-screens. Defaults to true. | boolean | no       | Android,iOS | no                |
| layout<sup>7.2.10+</sup>                      | A layout is a wrapper around the navigator. It can be useful for augmenting the navigators with additional UI with a wrapper.The difference from adding a wrapper around the navigator manually is that the code in a layout callback has access to the navigator's state, options etc. | object                              | no       | all         | yes               |
| screenLayout<sup>7.2.10+</sup>                | A screen layout is a wrapper around each screen in the navigator. It makes it easier to provide things such as an error boundary and suspense fallback for all screens in the navigator, or wrap each screen with additional UI. | object                              | no       | all         | yes               |
| screenListeners<sup>7.2.10+</sup>             | You can pass a prop named `screenListeners` to the navigator component, where you can specify listeners for events from all screens for this navigator. | object                              | no       | all         | yes               |
| headerBackButtonDisplayMode<sup>7.2.10+</sup> | How  the back button displays icon and title.                | 'default' \| 'generic' \| 'minimal' | no       | all         | yes               |

**Options & screenOptions**

| Name                         | Description                                                                                                                                                                                                                                                                                                               | Type                                        | Required | Platform    | HarmonyOS Support |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- | -------- | ----------- | ----------------- |
| title                        | String that can be used as a fallback for headerTitle.                                                                                                                                                                                                                                                                    | string                                      | no       | all         | yes               |
| cardShadowEnabled            | Use this prop to have visible shadows during transitions. Defaults to true.                                                                                                                                                                                                                                               | boolean                                     | no       | all         | yes               |
| cardOverlayEnabled           | Use this prop to have a semi-transparent dark overlay visible under the card during transitions. Defaults to true on Android and false on iOS.                                                                                                                                                                            | boolean                                     | no       | all         | yes               |
| cardOverlay                  | Function which returns a React Element to display as the overlay for the card. Make sure to set cardOverlayEnabled to true when using this.                                                                                                                                                                               | fucntion                                    | no       | all         | yes               |
| cardStyle                    | Style object for the card in stack. You can provide a custom background color to use instead of the default background here.                                                                                                                                                                                              | object                                      | no       | all         | yes               |
| presentation                 | This is shortcut option which configures several options to configure the style for rendering and transitions.                                                                                                                                                                                                            | 'card'&#124;'modal'&#124;'transparentModal' | no       | all         | yes               |
| animationEnabled<sup>deprecated  from 7.2.10</sup>       | Whether transition animation should be enabled on the screen. If you set it to false, the screen won't animate when pushing or popping. Defaults to true on iOS and Android, false on Web. | boolean                                     | no       | all         | yes               |
| animationTypeForReplace      | The type of animation to use when this screen replaces another screen.                                                                                                                                                                                                                                                    | 'push'&#124;'pop'                           | no       | all         | yes               |
| gestureEnabled               | Whether you can use gestures to dismiss this screen.                                                                                                                                                                                                                                                                      | boolean                                     | no       | Android,iOS | yes               |
| gestureResponseDistance      | Number to override the distance of touch start from the edge of the screen to recognize gestures.                                                                                                                                                                                                                         | number                                      | no       | Android,iOS | yes               |
| gestureVelocityImpact        | Number which determines the relevance of velocity for the gesture. Defaults to 0.3.                                                                                                                                                                                                                                       | number                                      | no       | Android,iOS | yes               |
| gestureDirection             | Direction of the gestures.                                                                                                                                                                                                                                                                                                | string                                      | no       | Android,iOS | yes               |
| transitionSpec               | Configuration object for the screen transition.                                                                                                                                                                                                                                                                           | object                                      | no       | all         | yes               |
| cardStyleInterpolator        | Interpolated styles for various parts of the card.                                                                                                                                                                                                                                                                        | object                                      | no       | all         | yes               |
| headerStyleInterpolators                                 | Interpolated styles for various parts of the header.         | object                                      | no       | all         | yes               |
| keyboardHandlingEnabled      | If false, the keyboard will NOT automatically dismiss when navigating to a new screen from this screen. Defaults to true.                                                                                                                                                                                                 | boolean                                     | no       | all         | yes               |
| detachPreviousScreen         | Boolean used to indicate whether to detach the previous screen from the view hierarchy to save memory. Set it to false if you need the previous screen to be seen through the active screen. Only applicable if detachInactiveScreens isn't set to false.                                                                 | boolean                                     | no       | all         | no                |
| freezeOnBlur                 | Boolean indicating whether to prevent inactive screens from re-rendering. Defaults to false. Defaults to true when enableFreeze() from react-native-screens package is run at the top of the application.                                                                                                                 | boolean                                     | no       | all         | no                |
| header                       | Custom header to use instead of the default header.                                                                                                                                                                                                                                                                       | function                                    | no       | all         | yes               |
| headerMode                   | Specifies how the header should be rendered.                                                                                                                                                                                                                                                                              | 'float'&#124;'screen'                       | no       | all         | yes               |
| headerShown                  | Whether to show or hide the header for the screen. The header is shown by default. Setting this to false hides the header.                                                                                                                                                                                                | boolean                                     | no       | all         | yes               |
| headerBackAllowFontScaling   | Whether back button title font should scale to respect Text Size accessibility settings. Defaults to false.                                                                                                                                                                                                               | boolean                                     | no       | all         | yes               |
| headerBackAccessibilityLabel | Accessibility label for the header back button.                                                                                                                                                                                                                                                                           | string                                      | no       | all         | yes               |
| headerBackImage              | Function which returns a React Element to display custom image in header's back button. When a function is used, it receives the tintColor in it's argument object. Defaults to Image component with back image source, which is the default back icon image for the platform (a chevron on iOS and an arrow on Android). | function                                    | no       | all         | yes               |
| headerBackTitle              | Title string used by the back button on iOS. Defaults to the previous scene's headerTitle.                                                                                                                                                                                                                                | string                                      | no       | all         | yes               |
| headerBackTitleVisible<sup>deprecated  from 7.2.10</sup> | A reasonable default is supplied for whether the back button title should be visible or not, but if you want to override that you can use true or false in this option. | boolean                                     | no       | all         | yes               |
| headerTruncatedBackTitle     | Title string used by the back button when headerBackTitle doesn't fit on the screen. "Back" by default.                                                                                                                                                                                                                   | string                                      | no       | all         | yes               |
| headerBackTitleStyle         | Style object for the back title.                                                                                                                                                                                                                                                                                          | object                                      | no       | all         | yes               |

**Events**
| Name            | Description                                                                                                                    | Type     | Required | Platform | HarmonyOS Support |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| transitionStart | This event is fired when the transition animation starts for the current screen.                                               | function | no       | all      | yes               |
| transitionEnd   | This event is fired when the transition animation ends for the current screen.                                                 | function | no       | all      | yes               |
| gestureStart    | This event is fired when the swipe gesture starts for the current screen.                                                      | function | no       | all      | yes               |
| gestureEnd      | This event is fired when the swipe gesture ends for the current screen. e.g. a screen was successfully dismissed.              | function | no       | all      | yes               |
| gestureCancel   | This event is fired when the swipe gesture is cancelled for the current screen. e.g. a screen wasn't dismissed by the gesture. | function | no       | all      | yes               |
| useCardAnimation<sup>7.2.10+</sup> | This hook returns values related to the screen's animation.  | function | no       | all      | yes               |
## Known Issues
- [ ] The TextInput component can allow click events to pass through to the underlying elements.[issues#37](https://github.com/react-native-oh-library/react-navigation/issues/37)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/stack/LICENSE).
