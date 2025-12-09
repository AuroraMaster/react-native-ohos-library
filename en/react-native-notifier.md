> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-notifier</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/seniv/react-native-notifier">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/seniv/react-native-notifier/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/seniv/react-native-notifier)

The repository of this third-party library is on Github and supports direct download from npm. The specific version ownership relationship is as follows:


| Version | Package Name                                                    | Repository | Release | Support RN version |
| ---------- | ------------------------------------------------------------ | ---------- |  ---------- |  ---------- |
| 2.0.0 | react-native-notifier | [Github](https://github.com/seniv/react-native-notifier)|[Github Releases](https://github.com/seniv/react-native-notifier/releases)|0.72       |
| 3.0.0| react-native-notifier  | [Github](https://github.com/seniv/react-native-notifier) |[Github Releases](https://github.com/seniv/react-native-notifier/releases) | 0.77       |

## Installation and Usage

Go to the project directory and execute the following instruction:

#### **npm**

```bash
#0.72
npm install react-native-notifier@2.0.0

#0.77
npm install react-native-notifier@3.0.0-rc.5
```

#### **yarn**

```bash
#0.72
yarn add react-native-notifier@2.0.0

#0.77
yarn add react-native-notifier@3.0.0-rc.5
```

The following code shows the basic use scenario of the repository:

```js
import * as React from "react";
import { View, Text, SafeAreaView, TouchableOpacity } from "react-native";

import { Notifier, NotifierWrapper } from "react-native-notifier";

import { GestureHandlerRootView } from "react-native-gesture-handler";

export const Notifier = () => {
  return (
    <>
      <SafeAreaView style={{ flex: 1 }}>
        <GestureHandlerRootView style={{ flex: 1 }}>
          <NotifierWrapper>
            <TouchableOpacity
              style={{
                alignItems: "center",
                borderRadius: 5,
                marginHorizontal: 10,
                backgroundColor: "#007BFF",
                padding: 15,
                marginTop: 10,
                marginBottom: 10,
              }}
              onPress={() =>
                Notifier.showNotification({
                  title: "basic tests",
                  description: "basic tests",
                })
              }
            >
              <Text>onPress</Text>
            </TouchableOpacity>
          </NotifierWrapper>
        </GestureHandlerRootView>
      </SafeAreaView>
    </>
  );
};
```

## Link

The HarmonyOS implementation of this library depends on the native code from react-native-gesture-handler. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [react-native-gesture-handler](/en/react-native-gesture-handler.md) to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.28; SDK: HarmonyOS-NEXT-DB1 5.0.0.31; IDE: DevEco Studio 5.0.3.500; ROM: 3.0.0.25;
2. RNOH: 0.77.18; SDK: HarmonyOS-5.1.1.208(API19); IDE: DevEco Studio 5.1.1.830; ROM: 6.0.0.112 SP12;

## Properties

For details, see [react-native-notifier docs](https://github.com/seniv/react-native-notifier)

Both `NotifierWrapper` and `NotifierRoot` receive the same props.

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                      | Description                                                                                                                                                                                                                                              | Type      | Required | Platform | HarmonyOS Support |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | -------- | -------- | ----------------- |
| omitGlobalMethodsHookup   | If set to `true`, global `Notifier` methods will not control this component. It's useful in case you have more than one `NotifierWrapper` or `NotifierRoot` rendered. If enabled, the only way to display notifications is using refs.                   | Boolean   | yes      | All      | No                |
| useRNScreensOverlay       | use `FullWindowOverlay` component from `react-native-screens` library. If `true`, Notifier will be rendered above NativeStackNavigation modals and RN Modal on iOS. This Option will work only if `react-native-screens` library is installed. iOS Only. | Boolean   | yes      | iOS      | No                |
| rnScreensOverlayViewStyle | Style that will be used for RN View that is inside of FullWindowOverlay. iOS Only.                                                                                                                                                                       | ViewStyle | yes      | iOS      | No                |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| showNotification  | Show notification with params.<br/>2.0.0: showNotification<ComponentType extends ElementType = typeof NotificationComponent,>(params: ShowNotificationParams<ComponentType>): void; <br/>3.0.0-rc.5: showNotification<ComponentType extends ElementType = typeof NotificationComponent,>(params: ShowNotificationParams<ComponentType>): ShowNotificationReturnType<ComponentType>; | Function  | yes | All      | yes |
| updateNotification<sup>3.0.0-rc.5+</sup> | Update currently visible notification. | Function | yes | All | yes |
| shakeNotification<sup>3.0.0-rc.5+</sup> | Shakes currently visible notification to attract the user's attention. | Function | yes | All | yes |
| isNotificationVisible<sup>3.0.0-rc.5+</sup> | Is any notification currently visible. | Function | yes | All | yes |
| hideNotification  |Hide notification and run callback function when notification completely hidden. | Function  | yes | All      | yes |
| clearQueue  |Clear [notifications queue](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#queue-mode) and optionally hide currently displayed notification. Might be useful to run after logout, after which queued notifications should not be displayed.| Function  | yes | All      | yes |
| updateById<sup>3.0.0-rc.5+</sup> |Update notification by ID, if visible - will be updated immediately,if it waits in the queue - it will be updated in the queue and will be displayed with updated parameters.| Function | yes | All | yes |
| shakeById<sup>3.0.0-rc.5+</sup> |Shakes notification by ID to attract the user's attention.| Function | yes | All | yes |
| isVisibleById<sup>3.0.0-rc.5+</sup> |Is notification with provided ID currently visible.| Function | yes | All | yes |
| hideById<sup>3.0.0-rc.5+</sup> |Hide notification by ID.| Function | yes | All | yes |

### `showNotification`

```
Notifier.showNotification(params: object);
```

`params`

| Name                | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| title  | Title of notification. Passed to Component. | String| Yes | All  |Yes  |
| description |Description of notification. Passed to Component. | String | Yes | All    | Yes    |
| duration |Time after notification will disappear. Set to 0 to not hide notification automatically  | Number | No |All    | Yes   
| Component |Component of the notification body. You can use one of the [bin components](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#components), or your [custom component](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#custom-component).  | Component | No |All    | Yes   
| componentProps | Additional props that are passed to Component. See all available props of built-in components in the [components section](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Fseniv%2Freact-native-notifier%2Ftree%2Fmain%3Ftab%3Dreadme-ov-file%23components).<br/>2.0.0:  componentProps?: Omit<React.ComponentProps<ComponentType>, 'title' \| 'description'>;<br />3.0.0-rc.5: componentProps?: Omit<React.ComponentProps<ComponentType>, keyof NotifierComponentProps>; | Object | No | All | Yes | 
| containerStyle | Styles Object that will be used in container.<br />2.0.0:  containerStyle?: ContainerStyleParam;<br />3.0.0-rc.5: containerStyle?: AnimatedViewProps['style']; | bool | No | All | Yes |
| containerStyle |tyles Object or a Function that will receive translateY: Animated.Value as first parameter and should return Styles that will be used in container. Using this parameter it is possible to create[ your own animations of the notification](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#custom-animations).   | bool |No | All    | Yes   
| containerProps | 	Props of Animated Container  | Object |No | All    | Yes  
| queueMode | Determines the order in which notifications are shown. Read more in the [Queue Mode](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#queue-mode) section.  | String |No | All    | Yes  
| swipeEnabled<sup>deprecated from 3.0.0-rc.5+</sup> | Can notification be hidden by swiping it out | bool | No | All | Yes |
| animationDuration | How fast notification will appear/disappear | Number |No | All    | Yes  
| showAnimationDuration | How fast notification will appear.   | Number |No | All    | Yes  
| hideAnimationDuration	 | How fast notification will disappear.| Number |No | All    | Yes 
| easing | Animation easing. Details:[easing](https://reactnative.dev/docs/easing)  | Easing |No | All    | Yes   
| showEasing | Show Animation easing.| Easing |No | All    | Yes   
| hideEasing |Hide Animation easing. | Easing |No | All    | Yes   
| onShown | Function called when entering animation is finished | () => void |No | All    | Yes  
| onStartHiding | Function called when notification started hiding | () => void |No | All    | Yes  
| onHidden |Function called when notification completely hidden | () => void |No | All    | Yes  
| onPress | Function called when user press on notification | () => void |No | All    | Yes  
| hideOnPress | Should notification hide when user press on it| Boolean |No | All    | Yes  
| swipePixelsToClose	 | How many pixels user should swipe-up notification to dismiss it | Number |No | All    | Yes  
| swipeEasing	 | Animation easing after user finished swiping | Easing |No | All    | Yes  
| swipeAnimationDuration	 | How fast should be animation after user finished swiping | Number |No | All    | Yes  
| translucentStatusBar<sup>deprecated from 3.0.0-rc.5+</sup> | Add additional top padding that equals to StatusBar.currentHeight. Android Only. | Number | No | Android | No |
| duplicateBehavior<sup>3.0.0-rc.5+</sup> | What to do if notification with the same ID(!) already shown. | String | No | All | Yes |
| id<sup>3.0.0-rc.5+</sup> | A manually provided ID. If supplied, it overrides any generation strategy. If notification with the same ID already shown, result of the `showNotification` will depend on `duplicateBehavior` parameter. | String \| Number | No | All | Yes |
| idStrategy<sup>3.0.0-rc.5+</sup> | Specifies how the ID should be generated if none is manually provided. | String | No | All | Yes |
| animationFunction<sup>3.0.0-rc.5+</sup> | Function that receives object with various `Animated.Value` and should return Styles that will be used to animate the notification. When set, result of the function will replace default animation. This function will be called only once. | Function | No | All | Yes |
| ignoreSafeAreaInsets<sup>3.0.0-rc.5+</sup> | Ignores offsets from `useSafeAreaInsets` hook | Boolean | No | All | Yes |
| ignoreKeyboard<sup>3.0.0-rc.5+</sup> | Ignores the keyboard completely. Treats the keyboard as if it is always closed. | Boolean | No | All | Yes |
| ignoreKeyboardHeight<sup>3.0.0-rc.5+</sup> | Ignores keyboard height offset (when use bottom positions) | Boolean | No | All | Yes |
| additionalKeyboardOffset<sup>3.0.0-rc.5+</sup> | Additional bottom offset when keyboard is visible. | Number | No | All | Yes |
| additionalOffsets<sup>3.0.0-rc.5+</sup> | Offsets in addition to the safeAreaInsets. When keyboard is open and `ignoreKeyboard != true`, `bottom` offset will be ignored and `additionalKeyboardOffset` will be used instead. | Object | No | All | Yes |
| position<sup>3.0.0-rc.5+</sup> | Position of the notification | String | No | All | Yes |
| enterFrom<sup>3.0.0-rc.5+</sup> | Direction from which notification will appear | String | No | All | Yes |
| exitTo<sup>3.0.0-rc.5+</sup> | Direction to which notification will slide to hide | String | No | All | Yes |
| shakingConfig<sup>3.0.0-rc.5+</sup> | Config of the shaking animation. Moves the notification from `minValue` to `maxValue` `numberOfRepeats` times in horizontal or vertical direction. `useNativeDriver` is `true` by default, but it can be disabled. | Object | No | All | Yes |
| useRNScreensOverlay<sup>3.0.0-rc.5+</sup> | use FullWindowOverlay component from react-native-screens library | Boolean | No | iOS | Yes |
| rnScreensOverlayViewStyle<sup>3.0.0-rc.5+</sup> | Style that will be used for RN View that is inside of FullWindowOverlay | Object | No | iOS | Yes |

### `updateNotification`<sup>3.0.0-rc.5+</sup>
```
Notifier.updateNotification(params: object);
```

`params`

| Name                | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| title  | Title of notification. Passed to Component. | String| No | All  |Yes  |
| description |Description of notification. Passed to Component. | String | No | All    | Yes    |
| Component |Component of the notification body. You can use one of the [bin components](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#components), or your [custom component](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#custom-component).  | ComponentType | No |All    | Yes   |
| componentProps | Additional props that are passed to Component. See all available props of built-in components in the [components section](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#components).  | Object | No |All    | No   |
| idStrategy | Specifies how the ID should be generated if none is manually provided. | String | No |All | Yes |
| containerStyle |Styles Object that will be used in container.   | Object |No | All    | Yes   |
| animationFunction |Function that receives object with various `Animated.Value` and should return Styles that will be used to animate the notification. When set, result of the function will replace default animation. This function will be called only once. | Function |No | All | Yes |
| containerProps | 	Props of Animated Container  | Object |No | All    | Yes  |
| showAnimationConfig | Config of the function that runs the "showing" animation. `timing` or `spring` method can be used. `useNativeDriver` is `true` by default, but it can be disabled. | Object |No | All | Yes |
| hideAnimationConfig | Config of the function that runs the "hiding" animation. `timing` or `spring` method can be used. `useNativeDriver` is `true` by default, but it can be disabled. | Object |No | All | Yes |
| swipeOutAnimationConfig | Config of the function that runs animation that hides notification after it was swiped-out. `timing` or `spring` method can be used. `useNativeDriver` is `true` by default, but it can be disabled. | Object |No | All | Yes |
| resetSwipeAnimationConfig | Config of the function that runs animation that returns the notification back to "shown" position after it was moved/swiped by the user. `timing` or `spring` method can be used. `useNativeDriver` is `true` by default, but it can be disabled. | Object |No | All | Yes |
| onShown | Function called when entering animation is finished | () => void |No | All    | Yes  |
| onStartHiding | Function called when notification started hiding | () => void |No | All    | Yes  |
| onHidden |Function called when notification completely hidden | () => void |No | All    | Yes  |
| onPress | Function called when user press on notification | () => void |No | All    | Yes  |
| hideOnPress | Should notification hide when user press on it| Boolean |No | All    | Yes  |
| swipePixelsToClose	 | How many pixels user should swipe-up notification to dismiss it | Number |No | All    | Yes  |
| duration	| Time after notification will disappear. Set to `0` to not hide notification automatically | Number |No | All | Yes |
| ignoreSafeAreaInsets	| Ignores offsets from `useSafeAreaInsets` hook | Boolean |No | All | Yes |
| ignoreKeyboard	| Ignores the keyboard completely. Treats the keyboard as if it is always closed. | Boolean |No | All | Yes |
| ignoreKeyboardHeight	| Ignores keyboard height offset (when use bottom positions) | Boolean |No | All | Yes |
| additionalKeyboardOffset	| Additional bottom offset when keyboard is visible. | Number |No | All | Yes |
| additionalOffsets	| Offsets in addition to the safeAreaInsets. When keyboard is open and `ignoreKeyboard != true`, `bottom` offset will be ignored and `additionalKeyboardOffset` will be used instead. | Object |No | All | Yes |
| position	| Position of the notification | String |No | All | Yes |
| enterFrom	| Direction from which notification will appear | String |No | All | Yes |
| exitTo	| Direction to which notification will slide to hide | String |No | All | Yes |
| swipeDirection	| Direction in which notification can be swiped out | String |No | All | Yes |
| shakingConfig	| Config of the shaking animation. Moves the notification from `minValue` to `maxValue` `numberOfRepeats` times in horizontal or vertical direction. `useNativeDriver` is `true` by default, but it can be disabled. | Object |No | All | Yes |
| useRNScreensOverlay	| use FullWindowOverlay component from react-native-screens library | Boolean |No | iOS | Yes |
| rnScreensOverlayViewStyle	| Style that will be used for RN View that is inside of FullWindowOverlay | Object |No | iOS | Yes |


### `updateById`<sup>3.0.0-rc.5+</sup>
```
Notifier.updateById(id: string | number, params: object);
```

`params`

| Name                | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| title  | Title of notification. Passed to Component. | String| No | All  |Yes  |
| description |Description of notification. Passed to Component. | String | No | All    | Yes    |
| Component |Component of the notification body. You can use one of the [bin components](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#components), or your [custom component](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#custom-component).  | ComponentType | No |All    | Yes   |
| componentProps | Additional props that are passed to Component. See all available props of built-in components in the [components section](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#components).  | Object | No |All    | No   |
| idStrategy | Specifies how the ID should be generated if none is manually provided. | String | No |All | Yes |
| containerStyle |Styles Object that will be used in container.   | Object |No | All    | Yes   |
| animationFunction |Function that receives object with various `Animated.Value` and should return Styles that will be used to animate the notification. When set, result of the function will replace default animation. This function will be called only once. | Function |No | All | Yes |
| containerProps | 	Props of Animated Container  | Object |No | All    | Yes  |
| showAnimationConfig | Config of the function that runs the "showing" animation. `timing` or `spring` method can be used. `useNativeDriver` is `true` by default, but it can be disabled. | Object |No | All | Yes |
| hideAnimationConfig | Config of the function that runs the "hiding" animation. `timing` or `spring` method can be used. `useNativeDriver` is `true` by default, but it can be disabled. | Object |No | All | Yes |
| swipeOutAnimationConfig | Config of the function that runs animation that hides notification after it was swiped-out. `timing` or `spring` method can be used. `useNativeDriver` is `true` by default, but it can be disabled. | Object |No | All | Yes |
| resetSwipeAnimationConfig | Config of the function that runs animation that returns the notification back to "shown" position after it was moved/swiped by the user. `timing` or `spring` method can be used. `useNativeDriver` is `true` by default, but it can be disabled. | Object |No | All | Yes |
| onShown | Function called when entering animation is finished | () => void |No | All    | Yes  |
| onStartHiding | Function called when notification started hiding | () => void |No | All    | Yes  |
| onHidden |Function called when notification completely hidden | () => void |No | All    | Yes  |
| onPress | Function called when user press on notification | () => void |No | All    | Yes  |
| hideOnPress | Should notification hide when user press on it| Boolean |No | All    | Yes  |
| swipePixelsToClose	 | How many pixels user should swipe-up notification to dismiss it | Number |No | All    | Yes  |
| duration	| Time after notification will disappear. Set to `0` to not hide notification automatically | Number |No | All | Yes |
| ignoreSafeAreaInsets	| Ignores offsets from `useSafeAreaInsets` hook | Boolean |No | All | Yes |
| ignoreKeyboard	| Ignores the keyboard completely. Treats the keyboard as if it is always closed. | Boolean |No | All | Yes |
| ignoreKeyboardHeight	| Ignores keyboard height offset (when use bottom positions) | Boolean |No | All | Yes |
| additionalKeyboardOffset	| Additional bottom offset when keyboard is visible. | Number |No | All | Yes |
| additionalOffsets	| Offsets in addition to the safeAreaInsets. When keyboard is open and `ignoreKeyboard != true`, `bottom` offset will be ignored and `additionalKeyboardOffset` will be used instead. | Object |No | All | Yes |
| position	| Position of the notification | String |No | All | Yes |
| enterFrom	| Direction from which notification will appear | String |No | All | Yes |
| exitTo	| Direction to which notification will slide to hide | String |No | All | Yes |
| swipeDirection	| Direction in which notification can be swiped out | String |No | All | Yes |
| shakingConfig	| Config of the shaking animation. Moves the notification from `minValue` to `maxValue` `numberOfRepeats` times in horizontal or vertical direction. `useNativeDriver` is `true` by default, but it can be disabled. | Object |No | All | Yes |
| useRNScreensOverlay	| use FullWindowOverlay component from react-native-screens library | Boolean |No | iOS | Yes |
| rnScreensOverlayViewStyle	| Style that will be used for RN View that is inside of FullWindowOverlay | Object |No | iOS | Yes |


### `shakeNotification`<sup>3.0.0-rc.5+</sup>
```
Notifier.shakeNotification(resetTimer?: boolean);
```

### `isNotificationVisible`<sup>3.0.0-rc.5+</sup>
```
Notifier.isNotificationVisible();
```


### `hideNotification`

```
Notifier.hideNotification(onHiddenCallback?: (result: Animated.EndResult) => void);
```

### `clearQueue`

```
Notifier.clearQueue(hideDisplayedNotification?: boolean);
```

### `shakeById`<sup>3.0.0-rc.5+</sup>
```
Notifier.shakeById(id: string | number, resetTimer?: boolean);
```

### `isVisibleById`<sup>3.0.0-rc.5+</sup>
```
Notifier.isVisibleById(id: string | number);
```
### `hideById`<sup>3.0.0-rc.5+</sup>
```
Notifier.hideById(id: string | number, onHidden?: Animated.EndCallback);
```

## Queue Mode

Queue mode is used to define the order in which the notification appears in case other notifications are being displayed at the moment.

For example, if you have some important information like chat messages and you want the user to see all the notifications, then you can use `standby` mode. Or if you want to display something like an error message, then you can use `reset` mode.

By default, `reset` mode is used, which means every new notification clears the queue and gets displayed immediately.

In most cases, you will probably use only `reset` or `standby` modes.

All possible modes:
| Mode | Effect |  
| ------------------- | ------------------------------------ |
| reset | Clear notification queue and immediately display the new notification. Used by default.
| standby | Add notification to the end of the queue.
| next | Put notification in the first place in the queue. Will be shown right after the current notification disappears.
| immediate | Similar to next, but also it will hide currently displayed notification.

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### `NotifierComponents.Notification`

Currently, there are 2 components out of the box. If none of them fits your needs, then you can easily create your [Custom Component].

| Name | Type | Default |  Description |  Platform | HarmonyOS Support  |
| ---- | ----------- | ---- |  -------- |  ---- |  -------- | 
| title  | String | null  | Title of notification. | All | Yes
| description  | String | null  | Description of notification. | All | Yes
| ViewWithOffsets<sup>3.0.0-rc.5+</sup> | Function | null | Provides a container view with safe area boundaries | All | Yes |
| componentProps.type<sup>3.0.0-rc.5+</sup> | String | null | If set, the icon, icon background color, and border color will be determined by the provided type. | All | Yes |
| componentProps.useTypeColorForTitle<sup>3.0.0-rc.5+</sup> | Boolean | false | When `true`, the title color is automatically derived from the `type` prop. | All | Yes |
| componentProps.useTypeColorForDescription<sup>3.0.0-rc.5+</sup> | Boolean | false | When `true`, the description color is automatically derived from the `type` prop. | All | Yes |
| componentProps.iconSource<sup>3.0.0-rc.5+</sup> | ImageSourcePropType | depends on `type` | The icon source passed to the `<Image />` component as the `source` prop.If not specified, a default icon is used based on the `type`. | All | Yes |
| componentProps.safeAreaStyle<sup>3.0.0-rc.5+</sup> | ViewStyle | null | Style for the outermost container of the toast. | All | Yes |
| componentProps.iconContainerStyle<sup>3.0.0-rc.5+</sup> | TextStyle | null | Style for the icon container, useful for adjusting background color or size. | All | Yes |
| componentProps.iconStyle<sup>3.0.0-rc.5+</sup> | ImageStyle | null | Style for the icon `<Image />` itself, useful for adjusting icon color or size. | All | Yes |
| componentProps.textContainerStyle<sup>3.0.0-rc.5+</sup> | TextStyle | null | Style for the text container wrapping both title and description. | All | Yes |
| componentProps.titleStyle  | TextStyle | null  | The style to use for rendering title. | All | Yes
| componentProps.descriptionStyle  | TextStyle | null  |The style to use for rendering description. | All | Yes
| componentProps.imageSource  | Object | null  | Passed to <Image /> as source param. | All | Yes
| componentProps.imageStyle  | ImageStyle | null  | The style to use for rendering image. | All | Yes
| componentProps.containerStyle  | ViewStyle | null  | The style to use for notification container. | All | Yes
| componentProps.ContainerComponent  | Component | SafeAreaView  | A container of the component. Set it in case you use different SafeAreaView than the standard | All | Yes
| componentProps.maxTitleLines  | number | null  | The maximum number of lines to use for rendering title. | All | Yes
| componentProps.maxDescriptionLines  | number | null  | The maximum number of lines to use for rendering description. | All | Yes

### `NotifierComponents.Alert`

| Name | Type | Default |  Description | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- |  -------- | ---- |  -------- |
| title  | String | null  | Title of notification. |  All | Yes
| description  | String | null  | Description of notification. |  All | Yes
| componentProps.titleStyle  | TextStyle | null  | The style to use for rendering title. |  All | Yes
| ViewWithOffsets<sup>3.0.0-rc.5+</sup> | Function | null | Provides a container view with safe area boundaries | All | Yes |
| componentProps.type<sup>3.0.0-rc.5+</sup> | String | 'success' | Background color will be changed depending on the type. Available values: `error`(red), `success`(green), `warn`(orange) and `info`(blue). | All | Yes |
| componentProps.descriptionStyle  | TextStyle | null  |The style to use for rendering description. |  All | Yes
|componentProps.alertType  | String | 'success'  |Background color will be changed depending on the type. Available values: error(red), success(green), warn(orange) and info(blue). |  All | Yes
| componentProps.backgroundColor | String | null  | While the background of the alert depends on alertType, you can also set the other color you want. |  All | Yes
| componentProps.textColor  | String | 'white'  | Color of title and description. |  All | Yes
| componentProps.ContainerComponent  | Component | SafeAreaView  | A container of the component. Set it in case you use different SafeAreaView than the standard |  All | Yes
| componentProps.maxTitleLines  | number | null  | The maximum number of lines to use for rendering title. |  All | Yes
| componentProps.maxDescriptionLines  | number | null  | The maximum number of lines to use for rendering description. | All | Yes

### `NotifierComponents.SimpleToast`<sup>3.0.0-rc.5+</sup>

| Name                              | Type              | Default         | Description                                                  | HarmonyOS Support | Platform |
| --------------------------------- | ----------------- | --------------- | ------------------------------------------------------------ | ----------------- | -------- |
| title                             | String            | null            | Title of notification.                                       | Yes               | All      |
| ViewWithOffsets                   | Function          | null            | Provides a container view with safe area boundaries          | Yes               | All      |
| componentProps.titleStyle         | TextStyle         | null            | The style to use for rendering title                         | Yes               | All      |
| componentProps.safeAreaStyle      | ViewStyle         | null            | The style to use for safe area container.                    | Yes               | All      |
| componentProps.containerStyle     | ViewStyle         | null            | The style to use for toast content container.                | Yes               | All      |
| componentProps.maxTitleLines      | Number            | null            | The maximum number of lines to use for rendering title.      | Yes               | All      |
| componentProps.ContainerComponent | React.ElementType | ViewWithOffsets | A container of the component. Set it in case you use different SafeAreaView than the custom `ViewWithOffsets` | Yes               | All      |

### `NotifierComponents.Toast`<sup>3.0.0-rc.5+</sup>

| Name                                      | Type                | Default           | Description                                                  | Platform | HarmonyOS Support |
| ----------------------------------------- | ------------------- | ----------------- | ------------------------------------------------------------ | -------- | ----------------- |
| title                                     | String              | null              | Title of notification.                                       | All      | Yes               |
| description                               | String              | null              | Description of notification.                                 | All      | Yes               |
| ViewWithOffsets                           | Function            | null              | Provides a container view with safe area boundaries          | All      | Yes               |
| componentProps.type                       | String              | null              | If set, the icon and icon background color will be determined by the provided type. | All      | Yes               |
| componentProps.useTypeColorForTitle       | Boolean             | false             | When `true`, the title color is automatically derived from the `type` prop. | All      | Yes               |
| componentProps.useTypeColorForDescription | Boolean             | false             | When `true`, the description color is automatically derived from the `type` prop. | All      | Yes               |
| componentProps.maxTitleLines              | Number              | null              | The maximum number of lines for rendering the title text.    | All      | Yes               |
| componentProps.maxDescriptionLinesYes     | Number              | null              | The maximum number of lines for rendering the description text. | All      | Yes               |
| componentProps.iconSource                 | ImageSourcePropType | depends on `type` | The icon source passed to the `<Image />` component as the `source` prop.If not specified, a default icon is used based on the `type`. | All      | Yes               |
| componentProps.safeAreaStyle              | ViewStyle           | null              | Style for the safe area container of the toast.              | All      | Yes               |
| componentProps.containerStyle             | ViewStyle           | null              | Style for the toast content container, often used to modify background color,shadows, padding, or margin. | All      | Yes               |
| componentProps.iconContainerStyle         | TextStyle           | null              | Style for the icon container, useful for adjusting background color or size. | All      | Yes               |
| componentProps.iconStyle                  | ImageStyle          | null              | Style for the icon `<Image />` itself, useful for adjusting icon color or size. | All      | Yes               |
| componentProps.textContainerStyle         | TextStyle           | null              | Style for the text container wrapping both title and description. | All      | Yes               |
| componentProps.titleStyle                 | TextStyle           | null              | Style for the title text.                                    | All      | Yes               |
| componentProps.descriptionStyle           | TextStyle           | null              | Style for the description text.                              | All      | Yes               |
| componentProps.ContainerComponent         | React.ElementType   | ViewWithOffsets   | A custom container component. If used, it replaces the default `ViewWithOffsets` provided by the library. | All      | Yes               |

## Known Issues

- [ ] useRNScreensOverlay,rnScreensOverlayViewStyle ,It relies on react-native-screens and is not yet compatible with harmonyOS
- [ ] componentProps{needsOffscreenAlphaCompositing}, Not supported on harmonyOS
## Others

- omitGlobalMethodsHookup 源库 Properties 未生效 问题：[issues#102](https://github.com/seniv/react-native-notifier/issues/102)

## License

This project is licensed under [The MIT License (MIT)](https://github.com/seniv/react-native-notifier/blob/main/LICENSE).

