> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-navigation/bottom-tabs</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/bottom-tabs">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/bottom-tabs/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

| 三方库版本 | 支持RN版本 |
| ---------- | ---------- |
| 6.5.20     | 0.72       |
| 7.3.10     | 0.77       |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-navigation/bottom-tabs@6.5.20

# 0.77
npm install @react-navigation/bottom-tabs@7.3.10
```

#### **yarn**

```bash
# 0.72
yarn add @react-navigation/bottom-tabs@6.5.20

# 0.77
yarn add @react-navigation/bottom-tabs@7.3.10
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import { Text, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';

function HomeScreen() {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Home!</Text>
        </View>
    );
}

function SettingsScreen() {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Settings!</Text>
        </View>
    );
}

const Tab = createBottomTabNavigator();

export function NavigationBottomTabs() {
    return (
        <NavigationContainer>
            <Tab.Navigator>
                <Tab.Screen name="Home" component={HomeScreen} />
                <Tab.Screen name="Settings" component={SettingsScreen} />
            </Tab.Navigator>
        </NavigationContainer>
    );
}
```

## Link

本库依赖以下三方库，请查看对应文档：
+ [@react-navigation/native](/zh-cn/react-navigation-native.md)
+ [@react-native-oh-tpl/elements](/zh-cn/react-navigation-elements.md)
+ [@react-native-oh-library/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)

本库 HarmonyOS 侧实现依赖@react-native-oh-library/react-native-safe-area-context 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-library/react-native-safe-area-context 文档的 Link 章节](/zh-cn/react-native-safe-area-context.md#link)进行引入


## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.11; SDK: OpenHarmony(api11) 4.1.0.53; IDE: DevEco Studio 4.1.3.412; ROM: 2.0.0.52;
2. RNOH: 0.72.13; SDK: HarmonyOS NEXT Developer Preview1; IDE: DevEco Studio 4.1.3.500; ROM: 2.0.0.58;
3. RNOH: 0.72.20-CAPI: SDK: HarmonyOS NEXT Developer Beta1 B.0.18; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
4. RNOH: 0.72.27; SDK: HarmonyOS 5.1.1 Release SDK; IDE: DevEco Studio 5.1.1 Release; ROM: 5.0.1.120;
5. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，更多属性详情请查看 [react-navigation/bottom-tabs 的文档介绍](https://reactnavigation.org/docs/bottom-tab-navigator)

**Props**

| Name                  | Description                                                                                                                                                                        | Type                                                                     | Required | Platform    | HarmonyOS Support |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | -------- | ----------- | ----------------- |
| id                    | 导航器的可选唯一 ID。这可用于在子导航器中通过 navigation.getParent 引用此导航器。                    | string                                                                   | no       | all         | yes               |
| initialRouteName      | 导航器首次加载时要渲染的路由名称。	                                                       | string                                                                   | no       | all         | yes               |
| screenOptions         | 用于导航器中屏幕的默认选项。                                                           | object                                                                   | no       | all         | yes               |
| backBehavior          | 控制当在导航器中调用 goBack 时发生的行为（包括在 Android 上按下设备的返回键或执行返回手势）。                  | 'firstRoute'&#124;'initialRoute'&#124;'order'&#124;'history'&#124;'none' | no       | Android     | yes               |
| detachInactiveScreens | 用于指示是否应从视图层次结构中分离非活动屏幕以节省内存的布尔值。这实现了与 react-native-screens 的集成。默认为 true。 | boolean                                                                  | no       | Android,iOS | no                |
| sceneContainerStyle<sup>deprecated  from 7.3.10</sup>   | 包裹屏幕内容的组件的样式对象。                                                                                                                        | object                                                                   | no       | all         | yes               |
| tabBar                | 标签栏                                                                                                                                                                             | function                                                                 | no       | all         | yes               |
| layout<sup>7.3.10+</sup>                 | 布局，是导航器的包装器。                                                                                                                                      | object                                                                   | no       | all         | yes               |
| screenLayout<sup>7.3.10+</sup>           | 屏幕布局，是导航器中每个屏幕的包装器。                                                                                                                  | object                                                                   | no       | all         | yes               |
| screenListeners<sup>7.3.10+</sup>        | 用于监听此导航器所有屏幕事件的监听器。                                                                                                                         | object                                                                   | no       | all         | yes               |

**Options & screenOptions**

| Name                          | Description                                                                                                                                                                                               | Type                            | Required | Platform    | HarmonyOS Support |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- | -------- | ----------- | ----------------- |
| title                         | 通用标题，可用作 headerTitle 和 tabBarLabel 的回退值。。                                                                                  | string                          | no       | all         | yes               |
| tabBarLabel                   | 显示在标签栏中的标签标题字符串，或一个接收 { focused: boolean, color: string } 并返回 React.Node 的函数。                                                                         | function                        | no       | all         | yes               |
| tabBarShowLabel               | 标签文字是否应可见。默认为 true。                                                                                  | boolean                         | no       | all         | yes               |
| tabBarLabelPosition           | 标签是显示在图标下方还是图标旁边。                                                                                  | 'below-icon'&#124;'beside-icon' | no       | all         | yes               |
| tabBarLabelStyle              | 标签文字的样式对象。                                                                                  | object                          | no       | all         | yes               |
| tabBarIcon                    | 接收{ focused: boolean, color: string, size: number }并返回一个 React.Node 以在标签栏中显示的函数。                                                                                  | function                        | no       | all         | yes               |
| tabBarIconStyle               | 标签图标的样式对象。                                                                                  | object                          | no       | all         | yes               |
| tabBarBadge                   | 在标签图标徽章上显示的文本。接受字符串或数字。                                                                                  | string&#124;number              | no       | all         | yes               |
| tabBarBadgeStyle              | 标签图标上徽章的样式。您可以在此处指定背景颜色或文本颜色。                                                                                  | object                          | no       | all         | yes               |
| tabBarAccessibilityLabel      | 标签按钮的无障碍功能标签。                                                                                  | string                          | no       | all         | yes               |
| tabBarButton                  | 返回一个 React 元素作为标签栏按钮渲染的函数。                                                                                  | function                        | no       | all         | yes               |
| tabBarActiveTintColor         | 活动标签中图标和标签的颜色。                                                                                  | string                          | no       | all         | yes               |
| tabBarInactiveTintColor       | 非活动标签中图标和标签的颜色。                                                                                  | string                          | no       | all         | yes               |
| tabBarActiveBackgroundColor   | 活动标签的背景颜色。                                                                                  | string                          | no       | all         | yes               |
| tabBarInactiveBackgroundColor | 非活动标签的背景颜色。                                                                                  | string                          | no       | all         | yes               |
| tabBarHideOnKeyboard          | 键盘打开时是否隐藏标签栏。默认为 false。                                                                                  | boolean                         | no       | all         | yes               |
| tabBarItemStyle               | 标签项容器的样式对象。                                                                                  | object                          | no       | all         | yes               |
| tabBarStyle                   | 标签栏的样式对象。您可以在此处配置背景颜色等样式。                                                                                  | object                          | no       | all         | yes               |
| tabBarBackground              | 返回一个 React 元素用作标签栏背景的函数。                                                                                  | function                        | no       | all         | yes               |
| lazy                          | 此屏幕是否应在首次被访问时渲染。                                                                                  | boolean                         | no       | all         | yes               |
| unmountOnBlur<sup>deprecated  from 7.3.10</sup>                 | 在离开此屏幕时是否应卸载它。                                                                                                                                    | boolean                         | no       | all         | yes               |
| freezeOnBlur                  | 布尔值，指示是否防止非活动屏幕重新渲染。默认为 false。如果在应用程序顶部运行了来自 react-native-screens 包的 enableFreeze()，则默认为 true。 | boolean                         | no       | Android,iOS | no                |  |
| tabBarPosition<sup>7.3.10+</sup>                 | 标签栏的位置。                                                                                               | 'bottom'\| 'top' \| 'left' \| 'right'                         | no       | all | yes                |  |
| tabBarVariant<sup>7.3.10+</sup>                  | 标签栏的变体。Material 变体目前仅在 tabBarPosition 设置为 left 或 right 时受支持。 | 'uikit'\| 'material'  | no       | all | yes                |  |
| popToTopOnBlur<sup>7.3.10+</sup>                 | 布尔值，指示在离开此标签时，任何嵌套的堆栈是否应弹出到堆栈顶部。 | boolean               | no       | all | yes                |  |
| sceneStyle<sup>7.3.10+</sup>                     | 包裹屏幕内容的组件的样式对象。                                                              | object                | no       | all | yes                |  |

**Header related options**

| Name        | Description                                                                                                                | Type     | Required | Platform | HarmonyOS Support |
| ----------- | -------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| header      | 用于替代默认标题栏的自定义标题栏。                                                                       | function | no       | all      | yes               |
| headerShown | 是否显示或隐藏屏幕的标题栏。默认显示标题栏。将其设置为 false 会隐藏标题栏。 | boolean  | no       | all      | yes               |

**Events**

| Name         | Description                                                                                                            | Type     | Required | Platform | HarmonyOS Support |
| ------------ | ---------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| tabPress     | 当用户在标签栏中按下当前屏幕的标签按钮时触发此事件。                       | function | no       | all      | yes               |
| tabLongPress | 当用户在标签栏中长时间按下当前屏幕的标签按钮时触发此事件。 | function | no       | all      | yes               |

**Hooks**

| Name                    | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| useBottomTabBarHeight<sup>7.3.10+</sup>    | 此钩子返回底部标签栏的高度。默认情况下，屏幕内容不会延伸到标签栏下方。 | function | no       | all      | yes               |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/main/packages/bottom-tabs/LICENSE) ，请自由地享受和参与开源。