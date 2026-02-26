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

本项目基于 [@react-native-ohos/elements](https://github.com/react-navigation/react-navigation/tree/6.x/packages/elements) 开发。

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/elements`，具体版本所属关系如下：
| 三方库名称    | 三方库版本    | 发布信息     | 支持RN版本    | Autolink     | 编译API版本     | 社区基线版本    | npm地址                |
| ------------ | ------------ | ------------------------------ | ------------- | ------------- |------------------------ | ------------- | ------------- |
| @react-native-ohos/elements | ~2.4.0    | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-navigation/releases) | 0.82.* | 否 | API12+ | 2.6.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/elements) | 
| @react-native-ohos/elements | ~2.3.9    | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-navigation/releases) | 0.77.* | 否 | API12+ | 2.3.8 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/elements) ||
| @react-native-oh-tpl/elements | <=1.3.21-0.1.4 | [Github Releases](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/elements/releases) | 0.72   |    否 | API12+ | 1.3.20 | [Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/elements) |
## 1.安装与使用

进入到工程目录并输入以下命令：

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


下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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
## 2. 约束与限制

### 2.1. 兼容性

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[ @react-native-ohos/elements Releases](https://gitcode.com/openharmony-sig/rntpc_react-navigation/releases)

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS 5.1.1 Release SDK; IDE: DevEco Studio 5.1.1 Release; ROM: 5.0.1.120;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
3. RNOH: 0.82.1;  SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 3.属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，更多使用详情请查看 [react-navigation/elements 的文档介绍](https://reactnavigation.org/docs/elements)

**Header Props**

| Name                                    | Description                                          | Type                | Required | Platform | HarmonyOS Support |
|-----------------------------------------|------------------------------------------------------|---------------------|----------|----------|-------------------|
| headerTitle                             | 字符串或返回要用作标题的 React 元素的函数                             |              string       | no       | all      | yes               |
| headerTitleAlign                        | 如何对齐标题                                               | 'left'&#124;'center' | no       | all      | yes               |
| headerTitleAllowFontScaling             | 标题字体是否应缩放以遵循文本大小的无障碍设置                               | boolean             | no       | all      | yes               |
| headerLeft                              | 返回要在标题左侧显示的 React 元素的函数                              | function            | no       | all      | yes               |
| headerRight                             | 返回要在标题右侧显示的 React 元素的函数                              | function            | no       | all      | yes               |
| headerShadowVisible                     | 是否隐藏标题的高度阴影（安卓）或底部边框（iOS）                            | boolean             | no       | all      | yes               |
| headerStyle                             | 标题的样式对象，可在此指定自定义背景颜色                                 | object              | no       | all      | yes               |
| headerTitleStyle                        | 标题组件的样式对象                                            | object              | no       | all      | yes               |
| headerLeftContainerStyle                | 自定义标题左侧组件容器的样式，例如添加内边距                               | object              | no       | all      | yes               |
| headerRightContainerStyle               | 自定义标题右侧组件容器的样式，例如添加内边距                               | object              | no       | all      | yes               |
| headerTitleContainerStyle               | 自定义标题标题组件容器的样式，例如添加内边距                               | object              | no       | all      | yes               |
| headerBackgroundContainerStyle          | 标题背景元素容器的样式对象                                        | object              | no       | all      | yes               |
| headerTintColor                         | 标题的着色颜色                                              | string              | no       | all      | yes               |
| headerPressColor                        | 材质涟漪效果的颜色（仅限安卓 5.0 及以上）                              | string              | no       | Android  | no                |
| headerPressOpacity                      | 标题按钮的按下透明度（安卓 5.0 以下和 iOS）                           | number              | no       | all      | yes               |
| headerTransparent                       | 默认为 false，若为 true，标题将没有背景，除非通过 headerBackground 显式提供 | boolean             | no       | all      | yes               |
| headerBackground                        | 返回用作标题背景的 React 元素的函数                                | function            | no       | all      | yes               |
| headerStatusBarHeight                   | 为适配半透明状态栏在标题顶部添加的额外内边距                               | number              | no       | all      | yes               |
| headerSearchBarOptions<sup>2.3.8+</sup> | 标题搜索栏的选项                                             | object | no | all | yes |
| HeaderButton<sup>2.3.8+</sup>           | 用于在标题中显示按钮的组件                                        | function | no | all | yes |
| Button<sup>2.3.8+</sup>                 | 渲染按钮的组件                                              | function | no | all | yes |
| Label<sup>2.3.8+</sup>                  | 标签组件用于渲染小段文本                                         | function | no | all | yes |
| HeaderButtonRef<sup>2.6.0+</sup>                 | HeaderButton可以拿到内部的ref                                         | function | no | all | yes |
| PlatformPressableRef<sup>2.6.0+</sup>                 | PlatformPressableRef可以拿到内部的ref                                         | function | no | all | yes |

**Header Components Props**

| Name               | Description                                        | Type     | Required | Platform | HarmonyOS Support |
|--------------------|----------------------------------------------------|----------|----------|----------|-------------------|
| HeaderBackground   | 用于包含标题背景样式（如背景色和阴影）的组件                             | function | no       | all      | yes               |
| HeaderTitle        | 用于显示标题栏标题文本的组件，它是 headerTitle 的默认组件，接受与 Text 相同的属性 | function | no       | all      | yes               |
| HeaderBackButton   | 用于显示标题栏返回按钮的组件，它是栈导航器中 headerLeft 的默认组件            | function | no       | all      | yes               |
| MissingIcon        | 渲染缺失图标符号的组件，可作为图标缺失时的备用显示                          | function | no       | all      | yes               |
| PlatformPressable  | 在 Pressable 基础上提供平台差异处理抽象的组件                       | function | no       | all      | yes               |
| ResourceSavingView | 通过利用 removeClippedSubviews 提升非活动屏幕性能的组件            | function | no       | all      | yes               |

**Utilities**

| Name                   | Description                                                                                                       | Type     | Required | Platform | HarmonyOS Support |
|------------------------|-------------------------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| SafeAreaProviderCompat | 对 react-native-safe-area-context 中 SafeAreaProvider 组件的封装，包含初始值 | function | no       | all      | yes               |
| HeaderBackContext      | React 上下文，可用于获取父屏幕的返回标题  | function | no       | all      | yes               |
| HeaderShownContext     | React 上下文，可用于检查父屏幕中标题栏是否可见 | function | no       | all      | yes               |
| HeaderHeightContext    | React 上下文，可用于获取父屏幕中最邻近可见标题栏的高度 | function | no       | all      | yes               |
| useHeaderHeight        | 钩子函数，返回父屏幕中最邻近可见标题栏的高度 | function | no       | all      | yes               |
| getDefaultHeaderHeight | 返回默认标题栏高度的辅助工具 | function | no       | all      | yes               |
| getHeaderTitle         | 返回标题栏中使用的标题文本的辅助工具 | function | no       | all      | yes               |


## 4.遗留问题

## 5.其他

示例代码依赖以下三方库，请查看对应文档：
+ [@react-navigation/stack](/zh-cn/react-navigation-stack.md)
+ [@react-navigation/native](/zh-cn/react-navigation-native.md)
  
## 6.开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/main/packages/elements/LICENSE) ，请自由地享受和参与开源。