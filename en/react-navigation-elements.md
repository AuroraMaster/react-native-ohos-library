> 模板版本：v0.4.0

<p align="center">
  <h1 align="center"> <code>@react-navigation/elements</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/main/packages/elements">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/main/packages/elements/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

This project is developed based on [@react-native-ohos/elements](https://github.com/react-navigation/react-navigation/tree/6.x/packages/elements).

This third-party library has been migrated to GitCode and can be installed directly from npm. The package name is: `@react-native-ohos/elements`. Version mapping is as follows:
| Package Name | Version | Release Notes | Supported RN Version | Autolink | Build API Version | Community Baseline Version | npm |
| --- | --- | --- | --- | --- | --- | --- | --- |
| @react-native-ohos/elements | ~2.4.0 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-navigation/releases) | 0.82.* | No | API12+ | 2.6.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/elements) |
| @react-native-ohos/elements | ~2.3.9 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-navigation/releases) | 0.77.* | No | API12+ | 2.3.8 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/elements) |
| @react-native-oh-tpl/elements | <=1.3.21-0.1.4 | [Github Releases](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/elements/releases) | 0.72   |    No | API12+ | 1.3.20 | [Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/elements) |

## 1. Installation & Usage

In your project directory, run:

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/elements

# 0.77/0.82
npm install @react-native-ohos/elements
```

```bash
# 0.72
yarn add @react-native-oh-tpl/elements

# 0.77/0.82
yarn add @react-native-ohos/elements
```

<!-- tabs:end -->


The code below shows a basic usage scenario:

> [!WARNING] The import name stays the same when using this library.

```js
import { Header, getHeaderTitle } from "@react-navigation/elements";
import { createStackNavigator } from "@react-navigation/stack"
import { NavigationContainer } from "@react-navigation/native";
import { Text, View } from 'react-native';


const Stack = createStackNavigator();

function HomeScreen() {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Home Screen</Text>
        </View>
    );
}

export function NavigationElements() {
    return (
        <NavigationContainer>
            <Stack.Navigator
                screenOptions={{
                    header: ({ options, route }) => (
                        <Header {...options} title={getHeaderTitle(options, route.name)} headerStyle={{ backgroundColor: 'red' }} />
                    ),
                }}
            >
                <Stack.Screen name="Home" component={HomeScreen} />
            </Stack.Navigator>
        </NavigationContainer>
    );
}

export default NavigationElements;
```

## 2. Constraints & Limitations

### 2.1. Compatibility

Please check the Release version mapping at the corresponding releases page:
[ @react-native-ohos/elements Releases](https://gitcode.com/openharmony-sig/rntpc_react-navigation/releases)

This document is verified on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS 5.1.1 Release SDK; IDE: DevEco Studio 5.1.1 Release; ROM: 5.0.1.120;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
3. RNOH: 0.82.1;  SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 3. Props

> [!TIP] The "Platform" column indicates platforms supported by the original third-party library.

> [!TIP] In the "HarmonyOS Support" column, **yes** means the property is supported on HarmonyOS, **no** means not supported, and **partially** means partially supported. Usage is cross-platform consistent, with behavior aligned to iOS or Android.

The following props have been verified. For more details, see [react-navigation/elements documentation](https://reactnavigation.org/docs/elements).

**Header Props**

| Name                                    | Description                                                                                                                | Type                | Required | Platform | HarmonyOS Support |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------|---------------------|----------|----------|-------------------|
| headerTitle                             | String or a function that returns a React Element to be used by the header.                                                | string              | no       | all      | yes               |
| headerTitleAlign                        | How to align the header title                                                                                              | 'left'&#124;'center' | no       | all      | yes               |
| headerTitleAllowFontScaling             | Whether header title font should scale to respect Text Size accessibility settings.                                        | boolean             | no       | all      | yes               |
| headerLeft                              | Function which returns a React Element to display on the left side of the header.                                          | function            | no       | all      | yes               |
| headerRight                             | Function which returns a React Element to display on the right side of the header.                                         | function            | no       | all      | yes               |
| headerShadowVisible                     | Whether to hide the elevation shadow (Android) or the bottom border (iOS) on the header.                                   | boolean             | no       | all      | yes               |
| headerStyle                             | Style object for the header. You can specify a custom background color here                                                | object              | no       | all      | yes               |
| headerTitleStyle                        | Style object for the title component                                                                                       | object              | no       | all      | yes               |
| headerLeftContainerStyle                | Customize the style for the container of the headerLeft component, for example to add padding.                             | object              | no       | all      | yes               |
| headerRightContainerStyle               | Customize the style for the container of the headerRight component, for example to add padding.                            | object              | no       | all      | yes               |
| headerTitleContainerStyle               | Customize the style for the container of the headerTitle component, for example to add padding.                            | object              | no       | all      | yes               |
| headerBackgroundContainerStyle          | Style object for the container of the headerBackground element.                                                            | object              | no       | all      | yes               |
| headerTintColor                         | Tint color for the header                                                                                                  | string              | no       | all      | yes               |
| headerPressColor                        | Color for material ripple (Android >= 5.0 only)                                                                            | string              | no       | Android  | no                |
| headerPressOpacity                      | Press opacity for the buttons in header (Android < 5.0, and iOS)                                                           | number              | no       | all      | yes               |
| headerTransparent                       | Defaults to false. If true, the header will not have a background unless you explicitly provide it with headerBackground.  | boolean             | no       | all      | yes               |
| headerBackground                        | Function which returns a React Element to render as the background of the header.                                          | function            | no       | all      | yes               |
| headerStatusBarHeight                   | Extra padding to add at the top of header to account for translucent status bar.                                           | number              | no       | all      | yes               |
| headerSearchBarOptions<sup>2.3.8+</sup> | Options for the search bar in the header.                                                                                  | object              | no       | all      | yes               |
| HeaderButton<sup>2.3.8+</sup>           | A component used to show a button in header.                                                                               | function            | no       | all      | yes               |
| Button<sup>2.3.8+</sup>                 | A component that renders a button.                                                                                         | function            | no       | all      | yes               |
| Label<sup>2.3.8+</sup>                  | The Label component is used to render small text.                                                                          | function            | no       | all      | yes               |
| HeaderButtonRef<sup>2.6.0+</sup>                         | HeaderButton can get the internal ref                                                                                      | function            | no       | all      | yes               |
| PlatformPressableRef<sup>2.6.0+</sup>                    | PlatformPressableRef can get the internal ref                                                                                 | function            | no       | all      | yes               |

**Header Components Props**

| Name               | Description                                                                                                                  | Type     | Required | Platform | HarmonyOS Support |
|--------------------|------------------------------------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| HeaderBackground   | A component containing the styles used in the background of the header, such as the background color and shadow.             | function | no       | all      | yes               |
| HeaderTitle        | A component used to show the title text in header. It's the default for headerTitle. It accepts the same props as a Text.    | function | no       | all      | yes               |
| HeaderBackButton   | A component used to show the back button header. It's the default for headerLeft in the stack navigator.                     | function | no       | all      | yes               |
| MissingIcon        | A component that renders a missing icon symbol. It can be used as a fallback for icons to show that there's a missing icon.  | function | no       | all      | yes               |
| PlatformPressable  | A component which provides an abstraction on top of Pressable to handle platform differences.                                | function | no       | all      | yes               |
| ResourceSavingView | A component which aids in improving performance for inactive screens by utilizing removeClippedSubviews.                     | function | no       | all      | yes               |

**Utilities**

| Name                   | Description                                                                                                        | Type     | Required | Platform | HarmonyOS Support |
|------------------------|--------------------------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| SafeAreaProviderCompat | A wrapper over the SafeAreaProvider component from `react-native-safe-area-context` which includes initial values. | function | no       | all      | yes               |
| HeaderBackContext      | React context that can be used to get the back title of the parent screen.                                         | function | no       | all      | yes               |
| HeaderShownContext     | React context that can be used to check if a header is visible in a parent screen.                                 | function | no       | all      | yes               |
| HeaderHeightContext    | React context that can be used to get the height of the nearest visible header in a parent screen.                 | function | no       | all      | yes               |
| useHeaderHeight        | Hook that returns the height of the nearest visible header in the parent screen.                                   | function | no       | all      | yes               |
| getDefaultHeaderHeight | Helper that returns the default header height.                                                                     | function | no       | all      | yes               |
| getHeaderTitle         | Helper that returns the title text to use in header.                                                                | function | no       | all      | yes               |

## 4. Known Issues

## 5. Other

The example code depends on the following third-party libraries. See the related docs:
+ [@react-navigation/stack](/zh-cn/react-navigation-stack.md)
+ [@react-navigation/native](/zh-cn/react-navigation-native.md)
  
## 6. License

This project is licensed under [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/main/packages/elements/LICENSE). Feel free to use it and contribute.