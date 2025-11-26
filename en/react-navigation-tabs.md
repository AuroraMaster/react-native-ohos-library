> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-navigation-tabs</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/tabs/tree/v2.7.0">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/tabs/blob/v2.7.0/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-navigation/tree/sig)

## Installation and Usage

Find the matching version information in the release address of a third-party library: 

| Third-party library version| Release information                                                     | Support RN version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.7.0      | [@react-native-oh-tpl/react-navigation-tabs Releases](https://github.com/react-native-oh-library/react-navigation/releases) | 0.72       |
| 2.7.1      | [@react-native-ohos/react-navigation-tabs Releases](https://gitcode.com/openharmony-sig/rntpc_react-navigation/tree/br_rnoh0.77) | 0.77       |

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
# V2.7.0
npm install @react-native-oh-tpl/react-navigation-tabs

# V2.7.1
npm install @react-native-ohos/react-navigation-tabs
```

#### **yarn**

```bash
# V2.7.0
yarn install @react-native-oh-tpl/react-navigation-tabs

# V2.7.1
yarn install @react-native-ohos/react-navigation-tabs
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from 'react';
import { createBottomTabNavigator } from 'react-navigation-tabs';
import MaterialIcons from 'react-native-vector-icons/MaterialIcons';
import Albums from './Shared/Albums';
import Article from './Shared/Article';
import Contacts from './Shared/Contacts';
// @ts-ignore
import TouchableBounce from 'react-native/Libraries/Components/Touchable/TouchableBounce';

const tabBarIcon =
  (name: string) =>
  ({ tintColor, horizontal }: { tintColor: string; horizontal: boolean }) => (
    <MaterialIcons name={name} color={tintColor} size={horizontal ? 17 : 24} />
  );

class AlbumsScreen extends React.Component {
  static navigationOptions = {
    title: '图片',
    tabBarLabel: 'Albums',
    tabBarIcon: tabBarIcon('photo-album'),
    tabBarButtonComponent: TouchableBounce
  };

  render() {
    return <Albums />;
  }
}

class ArticleScreen extends React.Component {
  static navigationOptions = {
    tabBarLabel: 'Article',
    tabBarIcon: tabBarIcon('chrome-reader-mode'),
    tabBarButtonComponent: TouchableBounce
  };

  render() {
    return <Article />;
  }
}

class ContactsScreen extends React.Component {
  static navigationOptions = {
    tabBarLabel: 'Contacts',
    tabBarIcon: tabBarIcon('contacts'),
    tabBarButtonComponent: TouchableBounce
  };

  render() {
    return <Contacts />;
  }
}

class BackHome extends React.Component {
  static navigationOptions = {
    tabBarLabel: 'Back',
    tabBarIcon: tabBarIcon('home'),
    tabBarButtonComponent: TouchableBounce,
    tabBarOnPress: ({ navigation, defaultHandler }) => {
      defaultHandler();
      navigation.navigate('Home');
    },
  };

  render(): React.ReactNode {
    return null;
  }
}

export default createBottomTabNavigator(
  {
    Albums: {
      screen: AlbumsScreen,
    },
    Article: {
      screen: ArticleScreen,
    },
    Contacts: {
      screen: ContactsScreen,
    },
    Back: {
      screen: BackHome,
    },
  },
  {
    initialRouteName: 'Albums',
    backBehavior: 'none',
    order: ['Albums', 'Contacts', 'Article', 'Back'],
    tabBarOptions: {
      backBehavior: 'history',
      inactiveBackgroundColor: '#851753ff', 
      activeBackgroundColor: '#f7eff3ff', 
      allowFontScaling: false,
      resetOnBlur: true,
      lazy: false,
      labelPosition: 'below-icon',
      inactiveTintColor: '#5355a1ff',
      activeTintColor: '#44c044ff',
      showIcon: false,
      adaptive: true,
      style: {
        height: 65,
        ppadding: 15,
      },
      labelStyle: {
        fontSize: 20,
      },
      tabStyle: {
        backgroundColor: '#e9f0f0ff',
      },
      safeAreaInset: {
        bottom: 'always',
        top: 'never',
      },
    },
  },
);
```

## Link

This repository depends on the following libraries, please refer to the corresponding documentation:

+ [react-native-pager-view](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-pager-view.md)
+ [react-native-tab-view](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-tab-view.md)
+ [react-native-gesture-handler](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-gesture-handler.md)
+ [react-native-reanimate](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-reanimated.md)
+ [react-native-safe-area-context](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-safe-area-context.md)
+ [react-native-screens](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-screens.md)

The HarmonyOS implementation of this library relies on the native code of the third-party libraries mentioned above. If the above libraries have already been introduced in the HarmonyOS project, there is no need to introduce them again. You can skip the steps in this chapter and use them directly.

If not introduced, please refer to the Link section of the corresponding document for introduction.

## Tip
This library relies on the ability of react native page view, which has been switched from ArkTS to CAPI. The transition animation function can only take effect normally after enabling CAPI configuration.

Please modify the configuration in the build function of src/main/ets/pages/index. ets in the entry directory.

```js
   RNApp({   
      rnInstanceConfig: {
       ...,
       //enableCAPIArchitecture Default is false and needs to be changed to true 
       enableCAPIArchitecture: true
      },
    ...
    })
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: 

| Third-party library version| Release information                                                     | Support RN version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.7.0      | [@react-native-oh-tpl/react-navigation-tabs Releases](https://github.com/react-native-oh-library/react-navigation/releases) | 0.72       |
| 2.7.1      | [@react-native-ohos/react-navigation-tabs Releases](https://gitcode.com/openharmony-sig/rntpc_react-navigation/tree/br_rnoh0.77) | 0.77       |


## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**createMaterialTopTabNavigator**：Create top label bar
| Name | Description| Type | Required | Platform | HarmonyOS Support |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|----------|----------|-------------------|
| RouteConfigs | The route configs object is a mapping from route name to a route config. | object | yes | all | yes |
| TabNavigatorConfig | Configure options for the top label navigator | object | no | all | yes |

**TabNavigatorConfig**：Top tab bar attribute configuration
| Name | Description| Type | Required | Platform | HarmonyOS Support |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|----------|----------|-------------------|
| initialRouteName | The routeName for the initial tab route when first loading. | string | no | all | yes |
| navigationOptions | Navigation options for the navigator itself, to configure a parent navigator. | object | no | all | yes |
| defaultNavigationOptions | Default navigation options to use for screens. | object | no | all | yes |
| order | Array of routeNames which defines the order of the tabs. | array | no | all | yes |
| paths | Provide a mapping of routeName to path config, which overrides the paths set in the routeConfigs. | object | no | all | yes |
| backBehavior |Pass initialRoute to return to initial tab. | 'none' &#124; 'initialRoute' &#124; 'history' &#124; 'order' &#124;| no | all | yes |
| tabBarPosition | Position of the tab bar. | 'top' &#124; 'bottom'| no | all | yes |
| swipeEnabled | Enable sliding tab switching. | boolean  | no | all | yes |
| lazy | Defaults to false. If true, tabs are rendered only when they are made active or on peek swipe. When false, all tabs are rendered immediately. | boolean | no | all | yes |
| lazyPlaceholderComponent | React component to render for routes that haven't been rendered yet. Receives an object containing the route as the argument. The lazy prop also needs to be enabled. | function | no | all | yes |
| initialLayout | Objects containing the initial width and height of the page. | object  | no | all | yes |
| pagerComponent | React component to use as the pager. The pager handles swipe gestures and page switching. By default we use react-native-gesture-handler for handling gestures. | function | no | all | no |
| swipeDistanceThreshold | Minimum distance threshold for sliding. | number  | no | all | no |
| swipeVelocityThreshold | Minimum sliding speed threshold. | number  | no | all | no |
| keyboardDismissMode | The keyboard closing method triggered by the drag gesture. | 'on-drag'&#124; 'none'  | no | all | yes |
| sceneContainerStyle | Set page container style.| object | no | all | yes|
| tabBarComponent | Optional, override the component to use as the tab bar.| function | no | all | yes|
| onSwipeStart | The callback function at the beginning of the sliding gesture. | function | no | all | yes |
| onSwipeEnd | The callback function at the end of the sliding gesture. | function | no | all | yes |
| tabBarOptions | An object with the following properties. | object | no | all | yes |

**navitgationOptions**：Top Navigation configuration items
| Name | Description| Type | Required | Platform | HarmonyOS Support |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| title | General Title. | string | no | all | yes |
| swipeEnabled | disable tab page sliding switching. | boolean | no | all | yes |
| tabBarIcon | Component for returning images. | funtion | no | all | yes |
| tabBarLabel | The name of the tab. | string | no | all | yes |
| tabBarAccessibilityLabel | Set accessible labels for label buttons.| string | no | all | yes |
| tabBarTestID | Label button ID.| string | no | all | yes |
| tabBarOnPress | click event. | funtion | no | all | yes |
| tabBarOnLongPress | long press event. | funtion | no | all | yes |

**tabBarOptions**：Top tab attribute configuration
| Name | Description| Type | Required | Platform | HarmonyOS Support |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| activeTintColor | Label and icon color of the active tab. | string | no | all | yes |
| inactiveTintColor | Label and icon color of the inactive tab. | string | no | all | yes |
| showIcon | Whether to show icon for tab, default is false. | boolean | no | all | yes |
| showLabel | Function which takes an object with the current route, focused status and color and returns a custom React Element to be used as a icon. | boolean | no | all | yes |
| upperCaseLabel | Whether to make label uppercase, default is true. | boolean | no | all | yes |
| pressColor | Color for material ripple (Android >= 5.0 only).| string | no | Android | no |
| pressOpacity | Opacity for pressed tab (iOS and Android < 5.0 only).| number | no | all | yes |
| scrollEnabled | Whether to enable scrollable tabs. | boolean | no | all | yes |
| tabStyle | Style object for the tab.| object | no | all | yes |
| indicatorStyle | Style object for the tab indicator (line at the bottom of the tab). | object | no | all | yes |
| labelStyle | Style object for the tab label. | object | no | all | yes |
| iconStyle | Style object for the tab icon. | object | no | all | yes |
| style | Style object for the tab bar. | object | no | all | yes |
| allowFontScaling | Whether label font should scale to respect Text Size accessibility settings, default is true. | boolean | no | all | yes |
| renderIndicator | Function which takes an object with the current route and returns a custom React Element to be used as a tab indicator.| function | no | all | yes |

**createBottomTabNavigator**：Create bottom label bar
| Name | Description| Type | Required | Platform | HarmonyOS Support |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|----------|----------|-------------------|
| RouteConfigs | The route configs object is a mapping from route name to a route config. | object | yes | all | yes |
| TabNavigatorConfig | Configure options for the bottom label navigator | object | yes | all | yes |


**TabNavigatorConfig**：Bottom tab bar attribute configuration
| Name | Description| Type | Required | Platform | HarmonyOS Support |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|----------|----------|-------------------|
| initialRouteName | The routeName for the initial tab route when first loading. | string | no | all | yes|
| navigationOptions | Navigation options for the navigator itself, to configure a parent navigator. | object | no | all | yes |
| defaultNavigationOptions| Default navigation options to use for screens.| object| no | all | yes |
| resetOnBlur | Reset the state of any nested navigators when switching away from a screen.| boolean | no | all | yes |
| order | Array of routeNames which defines the order of the tabs.| array | no | all | yes |
| paths | Provide a mapping of routeName to path config, which overrides the paths set in the routeConfigs. | object | no | all | yes |
| backBehavior |Pass initialRoute to return to initial tab. | 'none' &#124; 'initialRoute' &#124; 'history' &#124; 'order' &#124; | no | all | yes |
| lazy | Defaults to false. If true, tabs are rendered only when they are made active or on peek swipe. When false, all tabs are rendered immediately. | boolean | no | all | yes |
| tabBarComponent | Optional, override the component to use as the tab bar.| function | no | all | yes |
| tabBarOptions | An object with the following properties:. | object | no | all | yes |

**navitgationOptions**：Bottom Navigation configuration items
| Name | Description| Type | Required | Platform | HarmonyOS Support |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| title | General Title. | string | no | all | yes |
| tabBarVisible | Show/Hide bar. | boolean | no | all | yes |
| tabBarIcon | Component for returning images. | funtion | no | all | yes |
| tabBarLabel | The name of the tab. | string | no | all | yes |
| tabBarButtonComponent | Set custom label bar. | funtion | no | all | yes |
| tabBarAccessibilityLabel | Set accessible labels for label buttons.| string | no | all | yes |
| tabBarTestID | Label button ID.| string | no | all | yes |
| tabBarOnPress | click event. | funtion | no | all | yes |
| tabBarOnLongPress | long press event. | funtion | no | all | yes |


**tabBarOptions**：Bottom tab bar property configuration
| Name | Description| Type | Required | Platform | HarmonyOS Support |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| activeTintColor | Label and icon color of the active tab. | string | no | all | yes |
| activeBackgroundColor | Background color of the active tab. | string | no | all | yes |
| inactiveTintColor | Label and icon color of the inactive tab. | string | no | all | yes |
| inactiveBackgroundColor | Background color of the inactive tab. | string | no | all | yes |
| showLabel | Whether to show label for tab, default is true. | boolean | no | all | yes |
| showIcon | Whether to show icon for tab, default is true. | boolean | no | all | yes |
| style | Style object for the tab bar. | object | no | all | yes |
| labelStyle | Style object for the tab label. | object | no | all | yes|
| labelPosition | Where to show the tab label in relation to the tab icon. | 'beside-icon' &#124; 'below-icon' | no | all | yes |
| tabStyle | Style object for the tab. | object | no | all | yes |
| allowFontScaling | Whether label font should scale to respect Text Size accessibility settings, default is true. | boolean | no | all | yes |
| adaptive  | Should the tab icons and labels alignment change based on screen size? Defaults to true for iOS 11. If false, tab icons and labels align vertically all the time. When true, tab icons and labels align horizontally on tablet.. | boolean | no | ios | yes |
| safeAreaInset | Override the forceInset prop for <SafeAreaView>. | object | no | all | yes |
| keyboardHidesTabBar | Hide the tab bar when keyboard opens. | boolean | no | all  | yes |

## Known Issues

## Others
- The pressColor property in tabBarOptions does not take effect and cannot be pressed to change the color. The pressColor property is specifically designed for the Android platform and is directly passed in PlatformPrestable. On IOS, the pressColor property does not have a corresponding implementation, and IOS uses different mechanisms to handle touch feedback.

- The paginatComponent property in TabNavigatorConfig is not effective and cannot implement pagination functionality. The specific implementation of the renderPager property only exists on React native tab view versions 2.11.0-2.16.0, and has been abandoned on other versions.
  
- The swipeDistanceThreshold and swipeVelocityThreshold properties are directly passed from the source library to the TabView component, and the property functionality is implemented internally by the dependency library React native tab view, without processing the passed properties.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-navigation/tabs/blob/v2.7.0/LICENSE.md).