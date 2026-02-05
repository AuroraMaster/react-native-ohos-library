> 模板版本：v0.2.2

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

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/native-stack`，具体版本所属关系如下：

| 三方库名称    | 三方库版本    | 发布信息     | 支持RN版本    | Autolink     | 编译API版本     | 社区基线版本    | npm地址                |
| ------------ | ------------ | ------------------------------ | ------------- | ------------- |------------------------ | ------------- | ------------- |
| @react-native-ohos/native-stack | ~7.4.0     | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-navigation/releases) | 0.82 | 否 | API12+ | 7.3.22 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/native-stack) | 
| @react-native-ohos/native-stack | ~7.3.11    | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-navigation/releases) | 0.77 | 否 | API12+ | 7.3.10 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/native-stack) | 
| @react-native-oh-tpl/native-stack |  6.9.26-0.0.2   | [Github Releases](https://github.com/react-native-oh-library/react-navigation/releases) | 0.72 | 否 | API12+ | 6.9.26 | [Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/native-stack) |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

### **npm**

```bash
# for RN0.72
npm install @react-native-oh-tpl/native-stack

# for RN0.77/82
npm install @react-native-ohos/native-stack
```

### **yarn**

```bash
# for RN0.72
yarn install @react-native-oh-tpl/native-stack

# for RN0.77/82
yarn install @react-native-ohos/native-stack
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

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

本库依赖以下三方库，请查看对应文档：
+ [react-native-screens](/zh-cn/react-native-screens.md)
+ [native](/zh-cn/react-navigation-native.md)
+ [elements](/zh-cn/react-navigation-elements.md)
+ [react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)

本库 HarmonyOS 侧实现依赖react-native-safe-area-context 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[react-native-safe-area-context 文档的 Link 章节](/zh-cn/react-native-safe-area-context.md#link)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在下述版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;
3. RNOH：0.82.1; SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1 Release; ROM:6.0.0.120 SP7;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，更多属性详情请查看 [react-navigation/native-stack 的文档介绍](https://reactnavigation.org/docs/native-stack-navigator)

**Props**
| Name                              | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| --------------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| id                                | 为导航器设置一个可选的唯一标识符。该 ID 可用于在子导航器中通过 navigation.getParent 方法引用此导航器 | string | no       | all      | yes               |
| initialRouteName                  | 指定导航器首次加载时要渲染的初始路由名称. | string | no       | all      | yes               |
| screenOptions                     | 为此导航器中所有屏幕配置默认的选项对象，用于统一设置屏幕的呈现方式.     | object | no       | all      | yes               |
| layout<sup>7.3.10+</sup>          | 布局是一个包裹导航器的包装器。它可以通过包装器为导航器增强额外的用户界面。与手动在导航器外部添加包装器不同，布局回调中的代码可以访问导航器的状态、配置选项等信息。 | object | no       | all      | yes               |
| screenLayout<sup>7.3.10+</sup>    | 屏幕布局是导航器中每个屏幕的包装器。它可以更便捷地为导航器中的所有屏幕提供错误边界和 Suspense 回退内容，或者为每个屏幕包裹额外的用户界面。 | object | no       | all      | yes               |
| screenListeners<sup>7.3.10+</sup> | 你可以向导航器组件传递一个名为 screenListeners 的属性，在此处可以为此导航器中所有屏幕的事件指定监听器。 | object | no       | all      | yes               |

**Options & screenOptions**

| Name                                                        | Description                                                  | Type                                                         | Required | Platform     | HarmonyOS Support |
| ----------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ------------ | ----------------- |
| title                                                       | 可用作headerTitle回退的字符串.        | string                                                       | no       | all          | yes               |
| headerBackButtonMenuEnabled                                 | 布尔值，指示在长按 iOS 14 及以上版本的返回按钮时是否显示菜单，默认为 true | boolean                                                      | no       | iOS          | no                |
| headerBackVisible                                           | 返回按钮在标题栏中是否可见。如果已指定 headerLeft，可以使用此属性在 headerLeft 旁边显示返回按钮. | boolean                                                      | no       | Android,iOS  | no                |
| headerBackTitle                                             | iOS 上返回按钮使用的标题字符串。默认为上一个场景的标题，如果空间不足则为 "Back"。使用 headerBackTitleVisible: false 可隐藏.  | string                                                       | no       | iOS          | no                |
| headerBackTitleStyle                                        | 标题栏返回标题的样式对象.                          | object                                                       | no       | iOS          | no                |
| headerBackImageSource                                       | 在标题栏中显示为返回按钮图标的图像. | string                                                       | no       | all          | yes               |
| headerLargeStyle                                            | 显示大标题时的标题栏样式.             | object                                                       | no       | iOS          | no                |
| headerLargeTitle                                            | 是否启用大标题，滚动时折叠为常规标题. | string                                                       | no       | iOS          | no                |
| headerLargeTitleShadowVisible                               | 显示大标题时标题栏的投影是否可见. | boolean                                                      | no       | iOS          | no                |
| headerLargeTitleStyle                                       | 标题栏中大标题的样式对象.                      | object                                                       | no       | iOS          | no                |
| headerShown                                                 | 是否显示标题栏。默认显示标题栏。设置为 false 可隐藏标题栏. | boolean                                                      | no       | all          | yes               |
| headerStyle                                                 | 标题栏的样式对象.                                     | object                                                       | no       | all          | yes               |
| headerShadowVisible                                         | 是否隐藏标题上的标高阴影 (Android) 或底部边框 (iOS)。 | object                                                       | no       | Android，iOS | yes               |
| headerTransparent                                           | 指示导航栏是否半透明的布尔值. | boolean                                                      | no       | all          | yes               |
| headerBlurEffect                                            | 半透明标题的模糊效果。 headerTransparent 选项需要设置为 true 才能正常工作. | string                                                       | no       | iOS          | no                |
| headerBackground                                            | 返回一个 React 元素以呈现为标题背景的函数。这对于使用图像或渐变等背景非常有用. | function                                                     | no       | all          | yes               |
| headerTintColor                                             | 标题的色调颜色。更改后退按钮和标题的颜色. | string                                                       | no       | all          | yes               |
| headerLeft                                                  | 返回一个 React 元素以显示在标题左侧的函数。这取代了后退按钮。请参阅 headerBackVisible 以显示左侧元素的后退按钮. | function                                                     | no       | all          | yes               |
| headerRight                                                 | 返回一个 React 元素以显示在标题右侧的函数. | function                                                     | no       | all          | yes               |
| headerTitle                                                 | 字符串或返回要由标头使用的 React 元素的函数。默认为屏幕的标题或名称. | string&#124;function                                         | no       | all          | yes               |
| headerTitleAlign                                            | 如何对齐标题标题。在 iOS 以外的平台上默认为左对齐。iOS 不支持。它始终以 iOS 为中心，无法更改. | 'left'&#124;'right'                                          | no       | Android      | yes               |
| headerTitleStyle                                            | 标题的样式对象.                               | object                                                       | no       | all          | yes               |
| headerSearchBarOptions                                      | 在 iOS 上呈现本机搜索栏的选项.                | object                                                       | no       | Android，iOS | no                |
| header                                                      | 使用自定义标头代替默认标头.          | function                                                     | no       | all          | no                |
| statusBarAnimation                                          | 设置状态栏动画（类似于 StatusBar 组件）。默认在 iOS 上淡入淡出，在 Android 上不淡入淡出. | 'fade'&#124;'none'&#124;'slide'                              | no       | Android，iOS | no                |
| statusBarHidden                                             | 状态栏是否应在此屏幕上隐藏.      | boolean                                                      | no       | Android，iOS | no                |
| statusBarStyle                                              | 设置状态栏颜色（类似于 StatusBar 组件）。默认为自动. | string                                                       | no       | Android，iOS | no                |
| statusBarColor                                              | 设置状态栏颜色（类似于 StatusBar 组件）。默认为初始状态栏颜色。 | string                                                       | no       | Android      | no                |
| statusBarTranslucent                                        | 设置状态栏的半透明度（类似于StatusBar组件）。默认为 false. | boolean                                                      | no       | Android      | no                |
| contentStyle                                                | 场景内容的样式对象.                          | object                                                       | no       | all          | yes               |
| customAnimationOnGesture<sup>deprecated from 7.3.10 </sup>> | 关闭手势是否应使用提供给动画道具的动画。默认为 false | boolean                                                      | no       | iOS          | no                |
| fullScreenGestureEnabled                                    | 关闭手势是否适用于整个屏幕。使用手势来关闭此选项会产生与 simple_push 相同的过渡动画。可以通过设置 customAnimationOnGesture 属性来更改此行为。由于平台限制，无法实现默认的 iOS 动画。默认为 false。 | boolean                                                      | no       | iOS          | no                |
| gestureEnabled                                              | 是否可以使用手势关闭此屏幕。默认为 true。 | boolean                                                      | no       | iOS          | no                |
| animationTypeForReplace                                     | 当此屏幕替换另一个屏幕时要使用的动画类型。默认为弹出。 | 'push'&#124;'pop'                                            | no       | Android，iOS | no                |
| animation                                                   | 按下或弹出时屏幕应如何呈现动画。         | 'default'&#124;'fade'&#124;'fade_from_bottom'&#124;'simple_push'&#124;'slide_from_bottom'&#124;'slide_from_right'&#124;'slide_from_left'&#124;'none' | no       | Android,iOS  | no                |
| presentation                                                | 画面应该如何呈现。                          | 'card'&#124;'modal'&#124;'transparentModal'&#124;'containedModal'&#124;'fullScreenModal'&#124;'formSheet' | no       | Android，iOS | partially('card'/'transparentModal')         |
| orientation                                                 | 屏幕使用的显示方向。               | 'default'&#124;'all'&#124;'portrait'&#124;'portrait_up'&#124;'portrait_down'&#124;'landscape'&#124;'landscape_left'&#124;'landscape_left' | no       | Android，iOS | no                |
| autoHideHomeIndicator                                       | 指示主页指示器是否应该保持隐藏的布尔值。默认为 false。 | boolean                                                      | no       | iOS          | no                |
| gestureDirection                                            | 设置滑动以关闭屏幕的方向。 | 'vertical '&#124;'horizontal '                               | no       | iOS          | no                |
| animationDuration                                           | 更改 iOS 上的 slip_from_bottom、fade_from_bottom、fade 和 simple_push 过渡的持续时间（以毫秒为单位）。默认为 350。 | number                                                       | no       | iOS          | no                |
| navigationBarColor                                          | 设置导航栏颜色。默认为初始状态栏颜色。 | string                                                       | no       | Android      | no                |
| navigationBarHidden                                         | 指示是否应隐藏导航栏的布尔值。默认为 false。 | boolean                                                      | no       | Android      | no                |
| freezeOnBlur                                                | 布尔值，指示是否阻止非活动屏幕重新渲染。默认为 false。当react-native-screens包中的enableFreeze()在应用程序顶部运行时，默认为true。 | boolean                                                      | no       | Android,iOS  | no                |
| headerBackButtonDisplayMode<sup>7.3.10+</sup>               | 后退按钮如何显示图标和标题。                 | 'default' \| 'generic' \| 'minimal '                         | no       | iOS          | yes               |
| animationMatchesGesture<sup>7.3.10+</sup>                   | 要解除的手势是否应使用提供给动画道具的动画。默认为false。不会影响以模式呈现的屏幕的行为。 | boolean                                                      | no       | iOS          | no                |
| sheetElevation<sup>7.3.10+</sup>                            | 仅当演示文稿设置为formSheet时才有效。<br/>描述底部工作表阴影高度的整数值，影响底部工作表的阴影高度 | number                                                       | no       | Android      | no                |
| sheetExpandsWhenScrolledToEdge<sup>7.3.10+</sup>            | 仅当演示文稿设置为formSheet时才有效。<br/>控制工作表在滚动时是否应展开到更大的悬停位置。 | boolean                                                      | no       | iOS          | no                |
| sheetCornerRadius<sup>7.3.10+</sup>                         | 仅当演示文稿设置为formSheet时才有效。<br/>工作表尝试渲染时使用的圆角半径。 | number                                                       | no       | Android,iOS  | no                |
| sheetInitialDetentIndex<sup>7.3.10+</sup>                   | 仅当演示文稿设置为formSheet时才有效。<br/>工作表打开后应展开到的悬停位置的索引。 | number                                                       | no       | Android,iOS  | no                |
| sheetGrabberVisible<sup>7.3.10+</sup>                       | 仅当演示文稿设置为formSheet时才有效。<br/>布尔值，指示工作表顶部是否显示抓取器。 | boolean                                                      | no       | iOS          | no                |
| sheetLargestUndimmedDetentIndex<sup>7.3.10+</sup>           | 仅当演示文稿设置为formSheet时才有效。<br/>工作表下方视图不会被调暗的最大悬停位置索引。 | 'none' \| 'last'                                             | no       | Android,iOS  | no                |

**Events**

| Name            | Description                                                                      | Type     | Required | Platform | HarmonyOS Support |
|-----------------|----------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| transitionStart | 当当前屏幕的过渡动画开始时，会触发此事件。 | function | no       | all      | no                |
| transitionEnd   | 当当前屏幕的过渡动画结束时，会触发此事件。   | function | no       | all      | no                |

**Hooks<sup>7.3.10+</sup>**

| Name                    | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| useAnimatedHeaderHeight | 钩子返回一个表示标题高度的动画值。 | function | no       | all      | yes               |

## 遗留问题

- [ ] react-native-screens功能缺失，导致headerSearchBarOptions等属性功能无法实现：[issue#25](https://github.com/react-native-oh-library/react-navigation/issues/25)
- [ ] V7.3.10 鸿蒙侧未实现formSheet，导致presentation的formSheet未鸿蒙化：[issue#2](https://gitcode.com/openharmony-sig/rntpc_react-navigation/issues/2)
- [ ] V7.3.10 animationMatchesGesture 因依赖三方库react-native-screens而未实现鸿蒙化: [issue#3](https://gitcode.com/openharmony-sig/rntpc_react-navigation/issues/3)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/main/packages/native-stack/LICENSE) ，请自由地享受和参与开源。