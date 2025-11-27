> Template Version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-tab-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/main/packages/react-native-tab-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20macos%20|%20web%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/main/packages/react-native-tab-view/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github Address](https://github.com/react-native-oh-library/react-navigation/tree/sig)

The repository for this third-party library has been migrated to Gitcode, and it now supports direct download from npm. The new package name is: `@react-native-ohos/react-native-tab-view`. The specific version relationships are as follows:

| Version                        | Package Name       | Repository          |  Release            |Supported RN Version  |
| ------------------------------ | ----------------   | ------------------- | ------------------- | -------------------- |
| 3.5.2  | @react-native-oh-tpl/react-native-tab-view | [Github](https://github.com/react-native-oh-library/react-navigation) | [Github Releases](https://github.com/react-native-oh-library/react-navigation/releases) | 0.72 |
| 4.0.11 | @react-native-ohos/react-native-tab-view   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-navigation/tree/master/packages/react-native-tab-view) | [GitCode Releases]() | 0.77 |

## Installation and Usage

For older versions not published to npm, please refer to the [Installation Guide](/en/tgz-usage.md) to install the tgz package.

Navigate to your project directory and enter the following commands:

<!-- tabs:start -->

#### **npm**

```bash
# V3.5.2
npm install @react-native-oh-tpl/react-native-tab-view

# V4.0.11
npm install @react-native-ohos/react-native-tab-view
```

#### **yarn**

```bash
# V3.5.2
yarn add @react-native-oh-tpl/react-native-tab-view

# V4.0.11
yarn add @react-native-ohos/react-native-tab-view
```

<!-- tabs:end -->

The following code demonstrates a basic usage scenario of this library:

> [!WARNING] The import library name remains unchanged during use.

```js
import React from "react";
import { View, Text, Dimensions, StyleSheet } from "react-native";
import {
  TabView,
  TabBar,
  SceneMap,
  NavigationState,
  SceneRendererProps,
} from "react-native-tab-view";

type State = NavigationState<{
  key: string,
  title: string,
}>;

const FirstRoute = () => (
  <View
    style={{
      alignItems: "center",
      padding: 10,
      margin: 10,
      width: "80%",
      height: "80%",
      flex: 1,
      backgroundColor: "#62BBD4",
    }}
  >
    <Text
      style={{
        width: "100%",
        height: "100%",
        fontWeight: "bold",
      }}
    >
      First tab
    </Text>
  </View>
);

const SecondRoute = () => (
  <View
    style={{
      alignItems: "center",
      padding: 10,
      margin: 10,
      width: "80%",
      height: "80%",
      flex: 1,
      backgroundColor: "#A0D44E",
    }}
  >
    <Text
      style={{
        width: "100%",
        height: "100%",
        fontWeight: "bold",
      }}
    >
      Second tab
    </Text>
  </View>
);

const renderScene = SceneMap({
  first: FirstRoute,
  second: SecondRoute,
});
const TabViewTest = () => {
  const initialLayout = { width: Dimensions.get("window").width };
  const [index, setIndex] = React.useState(0);
  const renderTabBar = (
    props: SceneRendererProps & { navigationState: State }
  ) => (
    <TabBar
      {...props}
      scrollEnabled={true}
      indicatorStyle={styles.indicator}
      style={styles.tabbar}
      labelStyle={styles.label}
      tabStyle={styles.tabStyle}
    />
  );

  const [routes] = React.useState([
    { key: "first", title: "First" },
    { key: "second", title: "Second" },
  ]);

  return (
    <TabView
      style={{
        flex: 1,
        width: 350,
        height: 200,
        margin: 10,
        backgroundColor: "#6D8585",
      }}
      navigationState={{ index, routes }}
      renderScene={renderScene}
      renderTabBar={renderTabBar}
      onIndexChange={setIndex}
      initialLayout={initialLayout}
    />
  );
};

export default TabViewTest;

const styles = StyleSheet.create({
  tabbar: {
    backgroundColor: "#3f51b5",
    height: 70,
    width: 350,
  },
  indicator: {
    backgroundColor: "#ffeb3b",
    width: 175,
    height: 5,
  },
  label: {
    fontWeight: "400",
    fontSize: 20,
    width: 100,
    height: 50,
    color: "black",
  },
  tabStyle: {
    height: 65,
    width: 175,
    backgroundColor: "#BAFDAD",
  },
});
```

## Link

The HarmonyOS implementation of this library depends on the native code of @react-native-oh-tpl/react-native-pager-view. If this library has already been introduced in the HarmonyOS project, there is no need to introduce it again. You can skip the steps in this chapter and use it directly.

If not introduced, please refer to the [Link chapter of the @react-native-oh-tpl/react-native-pager-view documentation](/en/react-native-pager-view.md#link) for introduction.

## Tip
This library relies on the capabilities of react-native-pager-view, which has switched from ArkTS to CAPI. The transition animation function can only take effect normally after enabling the CAPI configuration.

Please modify the configuration in the build function in entry/src/main/ets/pages/index.ets
```js
   RNApp({   
      rnInstanceConfig: {
       ...,
       // enableCAPIArchitecture defaults to false, needs to be changed to true
       enableCAPIArchitecture: true
      },
    ...
    })
```

## Constraints and Limitations

### Compatibility

To use this library, you need to use the correct React-Native and RNOH versions. Additionally, you need to use the matching DevEco Studio and phone ROM.

Please check the release version information in the release address of the third-party library: 

| Third-party Version | Release Information                                                                                                | Supported RN Version |
| ------------------- | ------------------------------------------------------------------------------------------------------------------ | -------------------- |
| 3.5.2               | [@react-native-oh-tpl/react-native-tab-view Releases](https://github.com/react-native-oh-library/react-navigation/releases/) | 0.72                 |
| 4.0.11              | [@react-native-ohos/react-native-tab-view Releases](https://gitcode.com/openharmony-sig/rntpc_react-navigation/tree/master/packages/react-native-tab-view)       | 0.77                 |

This document is verified based on the following versions:
1. RNOH:0.72.96; SDK:HarmonyOS 5.1.1 Release SDK; IDE:DevEco Studio 5.1.1.840; ROM:6.0.0;
2. RNOH:0.77.18; SDK:HarmonyOS 5.1.1 Release SDK; IDE:DevEco Studio 5.1.1.840; ROM:6.0.0;

## Props

> [!TIP] The "Platform" column indicates the platforms supported by the original third-party library for that prop.

> [!TIP] A value of "yes" in the "HarmonyOS Support" column indicates the prop is supported on the HarmonyOS platform; "no" indicates it is not supported; "partially" indicates partial support. The usage method is consistent across platforms, and the effect aligns with that on iOS or Android.

**TabView**: Tab view component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- | -------- | -------- | ----------------- |
| navigationState | State for the tab view. | function | yes | all | yes |
| onIndexChange | Callback which is called on tab change, receives the index of the new tab as argument. The navigation state needs to be updated when it's called, otherwise the change is dropped. | function | yes | all | yes |
| renderScene | Callback which returns a react element to render as the page for the tab. | function | yes | all | yes |
| renderTabBar | Callback which returns a custom React Element to use as the tab bar | function | no | all | yes |
| tabBarPosition | Position of the tab bar in the tab view. | 'top'&#124;'bottom' | no | all | yes |
| lazy | Function which takes an object with the current route and returns a boolean to indicate whether to lazily render the scenes. | function | no | all | yes |
| lazyPreloadDistance | When `lazy` is enabled, you can specify how many adjacent routes should be preloaded with this prop. This value defaults to `0` which means lazy pages are loaded as they come into the viewport. | number | no | all | yes |
| renderLazyPlaceholder | Callback which returns a custom React Element to render for routes that haven't been rendered yet. Receives an object containing the route as the argument. The `lazy` prop also needs to be enabled. | string | no | all | yes |
| keyboardDismissMode | String indicating whether the keyboard gets dismissed in response to a drag gesture. | 'auto'&#124;'on-drag'&#124;'none' | no | all | yes |
| swipeEnabled | Boolean indicating whether to enable swipe gestures. Swipe gestures are enabled by default. Passing `false` will disable swipe gestures, but the user can still switch tabs by pressing the tab bar. | boolean | no | all | yes |
| animationEnabled | Enables animation when changing tab. By default it's true. | boolean | no | all | yes |
| onSwipeStart | Callback which is called when the swipe gesture starts, i.e. the user touches the screen and moves it. | boolean | no | all | yes |
| onSwipeEnd | Callback which is called when the swipe gesture ends, i.e. the user lifts their finger from the screen after the swipe gesture. | boolean | no | all | yes |
| initialLayout | Object containing the initial height and width of the screens. Passing this will improve the initial rendering performance. | object | no | all | yes |
| overScrollMode | Used to override default value of pager's overScroll mode. Can be `auto`, `always` or `never` (Android only). | 'auto'&#124;'always'&#124;'never' | no | Android | yes |
| sceneContainerStyle<sup>deprecated from 4.0.11</sup> | Style to apply to the view wrapping each screen. You can pass this to override some default styles such as overflow clipping | object | no | all | yes |
| pagerStyle | Style to apply to the pager view wrapping all the scenes. | object | no | all | yes |
| style | Style to apply to the tab view container. | object | no | all | yes |
| options<sup>4.0.11+</sup> | - | Record<string, TabDescriptor<T>> | no | all | yes |
| commonOptions<sup>4.0.11+</sup> | - | TabDescriptor<T> | no | all | yes |
| direction<sup>4.0.11+</sup> | Writing direction of the layout. | LocaleDirection | no | all | yes |

**TabBar**: Tab bar component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- | -------- | -------- | ----------------- |
| getLabelText<sup>deprecated from 4.0.11</sup> | Function which takes an object with the current route and returns the label text for the tab. Uses `route.title` by default. | function | no | all | yes |
| getAccessible<sup>deprecated from 4.0.11</sup> | Function which takes an object with the current route and returns a boolean to indicate whether to mark a tab as `accessible`. Defaults to `true`. | function | no | all | yes |
| getAccessibilityLabel<sup>deprecated from 4.0.11</sup> | Function which takes an object with the current route and returns a accessibility label for the tab button. Uses `route.accessibilityLabel` by default if specified, otherwise uses the route title. | function | no | all | yes |
| renderIcon<sup>deprecated from 4.0.11</sup> | Function which takes an object with the current route, focused status and color and returns a custom React Element to be used as a icon. | function | no | all | yes |
| renderLabel<sup>deprecated from 4.0.11</sup> | Function which takes an object with the current route, focused status and color and returns a custom React Element to be used as a label. | function | no | all | yes |
| renderTabBarItem | Function which takes a `TabBarItemProps` object and returns a custom React Element to be used as a tab button. | function | no | all | yes |
| renderIndicator | Function which takes an object with the current route and returns a custom React Element to be used as a tab indicator. | function | no | all | yes |
| renderBadge<sup>deprecated from 4.0.11</sup> | Function which takes an object with the current route and returns a custom React Element to be used as a badge. | function | no | all | yes |
| onTabPress | Function to execute on tab press. It receives the scene for the pressed tab, useful for things like scroll to top. | function | no | all | yes |
| onTabLongPress | Function to execute on tab long press, use for things like showing a menu with more options | function | no | all | yes |
| activeColor | Custom color for icon and label in the active tab. | string | no | all | yes |
| inactiveColor | Custom color for icon and label in the inactive tab. | string | no | all | yes |
| pressColor | Color for material ripple (Android >= 5.0 only). | string | no | Android | no |
| pressOpacity | Opacity for pressed tab (iOS and Android < 5.0 only). | number | no | all | yes |
| scrollEnabled | Boolean indicating whether to make the tab bar scrollable. | boolean | no | all | yes |
| bounces | Boolean indicating whether the tab bar bounces when scrolling. | boolean | no | iOS | no |
| tabStyle | Style to apply to the individual tab items in the tab bar. | object | no | all | yes |
| indicatorStyle | Style to apply to the active indicator. | object | no | all | yes |
| indicatorContainerStyle | Style to apply to the container view for the indicator. | object | no | all | yes |
| labelStyle<sup>deprecated from 4.0.11</sup> | Style to apply to the tab item label. | object | no | all | yes |
| contentContainerStyle | Style to apply to the inner container for tabs. | object | no | all | yes |
| style (TabBar) | Style to apply to the tab bar container. | object | no | all | yes |
| gap | Define a spacing between tabs. | number | no | all | yes |
| direction<sup>4.0.11+</sup> | Writing direction of the layout. | LocaleDirection | no | all | yes |
| layout<sup>4.0.11+</sup> | - | Layout | no | all | yes |
| options<sup>4.0.11+</sup> | - | Record<string, TabDescriptor<T>> | no | all | yes |

## Known Issues

- [x] Resolved: When swiping pages, there is a probability of getting stuck in the middle and not automatically aligning [issue#5](https://github.com/react-native-oh-library/react-navigation/issues/5)
- [ ] The bounces property in TabBar does not take effect and cannot achieve the scroll bounce effect [issue#34](https://github.com/react-native-oh-library/react-navigation/issues/34)

## Others

- The pressColor property in TabBar does not take effect and cannot change color on press. The pressColor property is specifically designed for the Android platform. This property is passed directly in PlatformPressable. On IOS, the pressColor property has no direct corresponding implementation; IOS uses a different mechanism to handle touch feedback.

## License

This project is based on [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/main/packages/react-native-tab-view/LICENSE). Feel free to enjoy and participate in open source.