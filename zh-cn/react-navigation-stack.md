> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/stack)

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/stack`，具体版本所属关系如下：

| Version                        | Package Name                             | Repository                                                   | Release                                                      | Version for RN |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 6.4.0 | @react-native-oh-tpl/stack  | [Github](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/stack) | [Github Releases](https://github.com/react-native-oh-library/react-navigation/releases) | 0.72       |
| 7.2.11                        | @react-native-ohos/stack | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-navigation/tree/br_rnoh0.77/packages/stack) | [GitCode Releases]() | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：


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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。
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
本库依赖以下三方库，请查看对应文档：
+ [@react-navigation/native](/zh-cn/react-navigation-native.md)
+ [@react-native-ohos/react-native-gesture-handler](/zh-cn/react-native-gesture-handler.md)
+ [@react-native-ohos/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)
+ [react-native-screens](/zh-cn/react-native-screens.md)

本库 HarmonyOS 侧实现依赖@react-native-ohos/react-native-gesture-handler、@react-native-ohos/react-native-safe-area-context 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-ohos/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)、[@react-native-ohos/react-native-safe-area-context 文档](/zh-cn/react-native-safe-area-context.md)进行引入

## 约束与限制
### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在下述版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，更多属性详情请查看 [react-navigation/stack 的文档介绍](https://reactnavigation.org/docs/stack-navigator)


**Props**

| Name                                          | Description                                                  | Type                                | Required | Platform    | HarmonyOS Support |
| --------------------------------------------- | ------------------------------------------------------------ | ----------------------------------- | -------- | ----------- | ----------------- |
| id                                            | 可选属性，为导航器提供唯一标识符，可通过 navigation.getParent 在子导航器中引用此导航器 | string                              | no       | all         | yes               |
| initialRouteName                              | 设置导航器首次加载时要渲染的路由名称 | string                              | no       | all         | yes               |
| screenOptions                                 | 为导航器中的屏幕设置默认选项     | object                              | no       | all         | yes               |
| detachInactiveScreens                         | 布尔值，用于指示是否应从视图层次结构中分离非活动屏幕以节省内存，默认为true. | boolean                             | no       | Android,iOS | no                |
| layout<sup>7.2.10+</sup>                      | 布局是导航器的包装。它可以用于通过包装器添加额外的UI来增强导航器。与手动在导航器周围添加包装器的不同之处在于，布局回调中的代码可以访问导航器的状态、选项等。 | object                              | no       | all         | yes               |
| screenLayout<sup>7.2.10+</sup>                | 屏幕布局是导航器中每个屏幕的包装。它可以更容易地为导航器中的所有屏幕提供错误边界和悬念回退等功能，或者用额外的UI包裹每个屏幕。 | object                              | no       | all         | yes               |
| screenListeners<sup>7.2.10+</sup>             | 可以将名为“screenListeners”的道具传递给导航器组件，在那里可以为此导航器的所有屏幕中的事件指定监听器。 | object                              | no       | all         | yes               |
| headerBackButtonDisplayMode<sup>7.2.10+</sup> | 后退按钮如何显示图标和标题。                | 'default' \| 'generic' \| 'minimal' | no       | all         | yes               |

**Options & screenOptions**

| Name                                                     | Description                                                  | Type                                        | Required | Platform    | HarmonyOS Support |
| -------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------- | -------- | ----------- | ----------------- |
| title                                                    | 可用作headerTitle回退的字符串。       | string                                      | no       | all         | yes               |
| cardShadowEnabled                                        | 使用此道具可以在过渡过程中产生可见的阴影。默认为true。 | boolean                                     | no       | all         | yes               |
| cardOverlayEnabled                                       | 使用此道具可以在过渡期间在卡片下方看到半透明的深色覆盖层。在Android上默认为true，在iOS上默认为false。 | boolean                                     | no       | all         | yes               |
| cardOverlay                                              | 函数返回一个React元素，以显示为卡片的覆盖层。使用此功能时，请确保将cardOverlayEnabled设置为true。 | fucntion                                    | no       | all         | yes               |
| cardStyle                                                | 堆栈中卡片的样式对象。您可以在此处提供自定义背景颜色来代替默认背景。 | object                                      | no       | all         | yes               |
| presentation                                             | 这是一个快捷方式选项，它配置了几个选项来配置渲染和过渡的样式。 | 'card'&#124;'modal'&#124;'transparentModal' | no       | all         | yes               |
| animationEnabled<sup>deprecated  from 7.2.10</sup>       | 是否应在屏幕上启用过渡动画。如果将其设置为false，则推或弹出时屏幕将不会动画。在iOS和Android上默认为true，在Web上默认为false。 | boolean                                     | no       | all         | yes               |
| animationTypeForReplace                                  | 当此屏幕替换另一个屏幕时使用的动画类型。 | 'push'&#124;'pop'                           | no       | all         | yes               |
| gestureEnabled                                           | 是否可以使用手势关闭此屏幕。         | boolean                                     | no       | Android,iOS | yes               |
| gestureResponseDistance                                  | 用于覆盖从屏幕边缘开始的触摸距离的数字，以识别手势。 | number                                      | no       | Android,iOS | yes               |
| gestureVelocityImpact                                    | 决定手势速度相关性的数字。默认值为0.3。 | number                                      | no       | Android,iOS | yes               |
| gestureDirection                                         | 手势的方向。                                   | string                                      | no       | Android,iOS | yes               |
| transitionSpec                                           | 屏幕转换的配置对象。              | object                                      | no       | all         | yes               |
| cardStyleInterpolator                                    | 卡片各部分的插入样式。           | object                                      | no       | all         | yes               |
| headerStyleInterpolators                                 | 页眉各部分的插值样式。         | object                                      | no       | all         | yes               |
| keyboardHandlingEnabled                                  | 如果为false，则从该屏幕导航到新屏幕时，键盘不会自动关闭。默认为true。 | boolean                                     | no       | all         | yes               |
| detachPreviousScreen                                     | 布尔值，用于指示是否从视图层次结构中分离上一个屏幕以节省内存。如果需要通过活动屏幕查看上一个屏幕，请将其设置为false。仅适用于detachInactiveScreen未设置为false的情况。 | boolean                                     | no       | all         | no                |
| freezeOnBlur                                             | 布尔值，指示是否阻止非活动屏幕重新渲染。默认为false。当在应用程序顶部运行react native screens包中的enableFreeze（）时，默认为true。 | boolean                                     | no       | all         | no                |
| header                                                   | 要使用的自定义标头，而不是默认标头。         | function                                    | no       | all         | yes               |
| headerMode                                               | 指定导航栏的渲染方式，可选值为 'float'（浮动）或 'screen'（屏幕）                 | 'float'&#124;'screen'                       | no       | all         | yes               |
| headerShown                                              | 控制是否显示导航栏，设置为 false 可隐藏导航栏，默认显示 | boolean                                     | no       | all         | yes               |
| headerBackAllowFontScaling                               | 返回按钮标题字体是否根据系统文字大小设置进行缩放，默认为 false | boolean                                     | no       | all         | yes               |
| headerBackAccessibilityLabel                             | 返回按钮的无障碍访问标签文本              | string                                      | no       | all         | yes               |
| headerBackImage                                          | 返回自定义返回按钮图片的函数，接收 tintColor 参数，默认使用平台特定的返回图标 | function                                    | no       | all         | yes               |
| headerBackTitle                                          | iOS平台上返回按钮显示的标题文字，默认为上一个页面的 headerTitle | string                                      | no       | all         | yes               |
| headerBackTitleVisible<sup>deprecated  from 7.2.10</sup> | 控制返回按钮标题是否可见，可覆盖系统默认设置 | boolean                                     | no       | all         | yes               |
| headerTruncatedBackTitle                                 | 当 headerBackTitle 文字过长无法完整显示时使用的截断标题，默认为 "Back"  | string                                      | no       | all         | yes               |
| headerBackTitleStyle                                     | 返回按钮标题的样式对象                             | object                                      | no       | all         | yes               |

**Events**
| Name                               | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ---------------------------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| transitionStart                    | 在当前页面的转场动画‌开始‌时触发 | function | no       | all      | yes               |
| transitionEnd                      | 在当前页面的转场动画‌结束‌时触发 | function | no       | all      | yes               |
| gestureStart                       | 在当前页面的滑动手势‌开始‌时触发 | function | no       | all      | yes               |
| gestureEnd                         | 在当前页面的滑动手势‌结束‌时触发（例如：页面成功被滑动手势关闭） | function | no       | all      | yes               |
| gestureCancel                      | 在当前页面的滑动手势被‌取消‌时触发（例如：页面没有被滑动手势关闭） | function | no       | all      | yes               |
| useCardAnimation<sup>7.2.10+</sup> | 此挂钩返回与屏幕动画相关的值。  | function | no       | all      | yes               |

## 遗留问题

- [ ] TextInput组件可以穿透下个页面点击。[issues#37](https://github.com/react-native-oh-library/react-navigation/issues/37)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/main/packages/stack/LICENSE) ，请自由地享受和参与开源。
