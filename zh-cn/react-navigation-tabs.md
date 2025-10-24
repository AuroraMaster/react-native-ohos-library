> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-navigation-tabs</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/tabs/tree/v2.7.0">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/tabs/blob/v2.7.0/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-navigation/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：


| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.7.0      | [@react-native-oh-tpl/react-navigation-tabs Releases](https://github.com/react-native-oh-library/react-navigation/releases) | 0.72       |
| 2.7.1      | [@react-native-ohos/react-navigation-tabs Releases](https://gitcode.com/openharmony-sig/rntpc_react-navigation/tree/br_rnoh0.77) | 0.77       |


对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。


进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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
      detachInactiveScreens: false,
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
本库依赖以下三方库,请查看对应文档：
+ [react-native-pager-view](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-pager-view.md)
+ [react-native-tab-view](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-tab-view.md)
+ [react-native-gesture-handler](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-gesture-handler.md)
+ [react-native-reanimate](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-reanimated.md)
+ [react-native-safe-area-context](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-safe-area-context.md)

本库HarmonyOS侧实现依赖上述三方库原生端代码，如已在HarmonyOS工程中引入过上述库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照对应文档的Link章节进行引入。

## Tip
本库依赖react-native-pager-view的能力，react-native-pager-view的能力已从ArkTS切换至CAPI。开启CAPI配置后过渡动画功能才能正常生效。

请在entry目录下的src/main/ets/pages/index.ets中的build函数中修改配置
```js
   RNApp({   
      rnInstanceConfig: {
       ...,
       //enableCAPIArchitecture 默认为false 需改成true 
       enableCAPIArchitecture: true
      },
    ...
    })
```




## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.7.0      | [@react-native-oh-tpl/react-navigation-tabs Releases](https://github.com/react-native-oh-library/react-navigation/releases) | 0.72       |
| 2.7.1      | [@react-native-ohos/react-navigation-tabs Releases](https://gitcode.com/openharmony-sig/rntpc_react-navigation/tree/br_rnoh0.77) | 0.77       |


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**createMaterialTopTabNavigator**：创建顶部标签栏
| Name | Description| Type | Required | Platform | HarmonyOS Support |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|----------|----------|-------------------|
| RouteConfigs | The route configs object is a mapping from route name to a route config. | object | yes | all | yes |
| TabNavigatorConfig | Configure options for the top label navigator | object | yes | all | yes |

**TabNavigatorConfig**：顶部标签栏属性配置
| Name | Description| Type | Required | Platform | HarmonyOS Support |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|----------|----------|-------------------|
| initialRouteName | The routeName for the initial tab route when first loading. | string | no | all | yes |
| navigationOptions| Navigation options for the navigator itself, to configure a parent navigator. | object | no | all | yes |
| defaultNavigationOptions | Default navigation options to use for screens. | object | no | all | yes |
| order | Array of routeNames which defines the order of the tabs. | array | no | all | yes |
| paths | Provide a mapping of routeName to path config, which overrides the paths set in the routeConfigs. | string | no | all | yes |
| backBehavior |Pass initialRoute to return to initial tab. | 'order' &#124; 'history' &#124; 'none' | no | all | yes |
| tabBarPosition | Position of the tab bar. | 'top' &#124; 'bottom'| no | all | yes |
| swipeEnabled | Whether to allow swiping between tabs.| boolean | no | all | yes |
| lazy | Defaults to false. If true, tabs are rendered only when they are made active or on peek swipe. When false, all tabs are rendered immediately. | boolean | no | all | yes |
| lazyPlaceholderComponent | React component to render for routes that haven't been rendered yet. Receives an object containing the route as the argument. The lazy prop also needs to be enabled. | function | no | all | yes               |
| initialLayout | Optional object containing the initial height and width, can be passed to prevent the one frame delay in react-native-tab-view rendering.| object | no | all | yes |
| pagerComponent | React component to use as the pager. The pager handles swipe gestures and page switching. By default we use react-native-gesture-handler for handling gestures. | function | no | all | no |
| tabBarComponent | Optional, override the component to use as the tab bar.| function | no | all | yes|
| tabBarOptions | An object with the following properties:. | object | no | all | yes |

**tabBarOptions**：顶部tab栏属性配置
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
| scrollEnabled | Boolean indicating whether to make the tab bar scrollable.| boolean | no | all | yes |
| renderIndicator | Function which takes an object with the current route and returns a custom React Element to be used as a tab indicator.| function | no | all | yes |

**createBottomTabNavigator**：创建底部标签栏
| Name | Description| Type | Required | Platform | HarmonyOS Support |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|----------|----------|-------------------|
| RouteConfigs | The route configs object is a mapping from route name to a route config. | object | yes | all | yes |
| BottomTabNavigatorConfig | Configure options for the bottom label navigator | object | yes | all | yes |


**BottomTabNavigatorConfig**：底部标签栏属性配置
| Name | Description| Type | Required | Platform | HarmonyOS Support |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|----------|----------|-------------------|
| initialRouteName | The routeName for the initial tab route when first loading. | string | no | all | yes|
| navigationOptions | Navigation options for the navigator itself, to configure a parent navigator. | object | no | all | yes |
| defaultNavigationOptions| Default navigation options to use for screens.| object| no | all | yes |
| resetOnBlur | Reset the state of any nested navigators when switching away from a screen.| boolean | no | all | yes |
| order | Array of routeNames which defines the order of the tabs.| array | no | all | yes |
| paths | Provide a mapping of routeName to path config, which overrides the paths set in the routeConfigs. | string | no | all | yes |
| backBehavior |Pass initialRoute to return to initial tab. | 'order' &#124; 'history' &#124; 'none' | no | all | yes |
| detachInactiveScreens | Boolean used to indicate whether inactive screens should be detached from the view hierarchy to save memory. | boolean | no | all | yes |
| lazy | Defaults to false. If true, tabs are rendered only when they are made active or on peek swipe. When false, all tabs are rendered immediately. | boolean | no | all | yes |
| tabBarComponent | Optional, override the component to use as the tab bar.| function | no | all | yes |
| tabBarOptions | An object with the following properties:. | object | no | all | yes |

**tabBarOptions**：底部tab栏属性配置
| Name | Description| Type | Required | Platform | HarmonyOS Support |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| activeTintColor | Label and icon color of the active tab. | string | no | all | yes |
| activeBackgroundColor | Background color of the active tab. | string | no | all | yes |
| inactiveTintColor | Label and icon color of the inactive tab. | string | no | all | yes |
| inactiveBackgroundColor | Background color of the inactive tab. | string | no | all | yes |
| showIcon | Whether to show icon for tab, default is true. | boolean | no | all | yes |
| showLabel | Whether to show label for tab, default is true. | boolean | no | all | yes |
| style | Style object for the tab bar. | object | no | all | yes |
| labelStyle | Style object for the tab label. | object | no | all | yes|
| labelPosition | Where to show the tab label in relation to the tab icon. | 'beside-icon' &#124; 'beside-icon' | no | all | yes |
| tabStyle | Style object for the tab. | object | no | all | yes |
| allowFontScaling | Whether label font should scale to respect Text Size accessibility settings, default is true. | boolean | no | all | yes |
| adaptive  | Should the tab icons and labels alignment change based on screen size. | boolean | no | all  | yes |
| safeAreaInset | Override the forceInset prop for <SafeAreaView>. | 'top' &#124; 'bottom' &#124; 'left' &#124;  'right'  'always' &#124; 'never' | no | all | yes |
| keyboardHidesTabBar | Hide the tab bar when keyboard opens. | boolean | no | all  | yes |

## 遗留问题

## 其他
- tabBarOptions中的pressColor属性，不生效，无法实现按下更改颜色。 pressColor属性，是专门为Android平台设计的，这个属性在PlatformPressable中直接传递，在IOS上，pressColor属性没有直接对应的实现，IOS使用不同的机制来处理触摸反馈。

- TabNavigatorConfig中的pagerComponent属性，不生效，无法实现分页功能。具体实现的renderPager属性只在react-native-tab-view 2.11.0-2.16.0版本上存在，其它版本上已废弃。
## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/tabs/blob/v2.7.0/LICENSE.md) ，请自由地享受和参与开源。