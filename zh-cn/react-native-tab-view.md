> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-navigation/tree/sig)

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-tab-view`，具体版本所属关系如下：

| Version                        | Package Name       | Repository          |  Release            |Supported RN Version  |
| ------------------------------ | ----------------   | ------------------- | ------------------- | -------------------- |
| 3.5.2  | @react-native-oh-tpl/react-native-tab-view | [Github](https://github.com/react-native-oh-library/react-navigation) | [Github Releases](https://github.com/react-native-oh-library/react-navigation/releases) | 0.72 |
| 4.0.11 | @react-native-ohos/react-native-tab-view   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-navigation/tree/master/packages/react-native-tab-view) | [GitCode Releases]() | 0.77 |

## 安装与使用

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-pager-view 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-pager-view 文档的 Link 章节](/zh-cn/react-native-pager-view.md#link)进行引入

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

在以下版本验证通过：

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.1 Release SDK; IDE：DevEco Studio 5.1.1.840; ROM：6.0.0;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.1 Release SDK; IDE：DevEco Studio 5.1.1.840; ROM：6.0.0;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**TabView**：选项卡组件
| Name                                                 | Description                                                  | Type                              | Required | Platform | HarmonyOS Support |
| ---------------------------------------------------- | ------------------------------------------------------------ | --------------------------------- | -------- | -------- | ----------------- |
| navigationState                                      | 标签页视图的状态                                              | fucntion                          | yes      | all      | yes               |
| onIndexChange                                        | 标签切换时调用的回调函数，接收新标签的索引作为参数。调用时需要更新导航状态，否则更改将被丢弃 | function                          | yes      | all      | yes               |
| renderScene                                          | 返回要渲染为标签页面的React元素的回调函数                     | function                          | yes      | all      | yes               |
| renderTabBar                                         | 返回要用作标签栏的自定义React元素的回调函数                   | function                          | no       | all      | yes               |
| tabBarPosition                                       | 标签栏在标签页视图中的位置                                    | 'top'&#124;'bottom'               | no       | all      | yes               |
| lazy                                                 | 接收当前路由对象并返回布尔值的函数，指示是否延迟渲染场景       | function                          | no       | all      | yes               |
| lazyPreloadDistance                                  | 当启用`lazy`时，可指定应预加载多少相邻路由。此值默认为`0`，表示延迟页面在进入视口时加载 | number                            | no       | all      | yes               |
| renderLazyPlaceholder                                | 返回要为尚未渲染的路由渲染的自定义React元素的回调函数。接收包含路由的对象作为参数。还需要启用`lazy`属性 | string                            | no       | all      | yes               |
| keyboardDismissMode                                  | 指示键盘是否响应拖拽手势而关闭的字符串                        | 'auto'&#124;'on-drag'&#124;'none' | no       | all      | yes               |
| swipeEnabled                                         | 指示是否启用手势滑动的布尔值。默认启用手势滑动。传递`false`将禁用手势滑动，但用户仍可通过按下标签栏切换标签 | boolean                           | no       | all      | yes               |
| animationEnabled                                     | 切换标签时启用动画。默认为true                                | boolean                           | no       | all      | yes               |
| onSwipeStart                                         | 手势滑动开始时调用的回调函数，即用户触摸屏幕并移动时           | boolean                           | no       | all      | yes               |
| onSwipeEnd                                           | 手势滑动结束时调用的回调函数，即用户在滑动手势后从屏幕抬起手指时 | boolean                           | no       | all      | yes               |
| initialLayout                                        | 包含屏幕初始高度和宽度的对象。传递此对象将提高初始渲染性能     | object                            | no       | all      | yes               |
| overScrollMode                                       | 用于覆盖页面滚动器的overScroll模式默认值。可以是`auto`、`always`或`never`（仅Android） | 'auto'&#124;'always'&#124;'never' | no       | Android  | yes               |
| sceneContainerStyle<sup>deprecated from 4.0.11</sup> | 应用于包装每个屏幕的视图的样式。可传递此属性以覆盖某些默认样式，如溢出裁剪 | object                            | no       | all      | yes               |
| pagerStyle                                           | 应用于包装所有场景的页面视图的样式                            | object                            | no       | all      | yes               |
| style                                                | 应用于标签页视图容器的样式                                    | object                            | no       | all      | yes               |
| options<sup>4.0.11+</sup>                            | -                                                            | Record<string, TabDescriptor<T>>  | no       | all      | yes               |
| commonOptions<sup>4.0.11+</sup>                      | -                                                            | TabDescriptor<T>                  | no       | all      | yes               |
| direction<sup>4.0.11+</sup>                          | 布局的书写方向                                                | LocaleDirection                   | no       | all      | yes               |

**TabBar**：选项卡标签栏
| Name                                                   | Description                                                  | Type                             | Required | Platform | HarmonyOS Support |
| ------------------------------------------------------ | ------------------------------------------------------------ | -------------------------------- | -------- | -------- | ----------------- |
| getLabelText<sup>deprecated from 4.0.11</sup>          | 接收当前路由对象并返回标签文本的函数。默认使用`route.title` | function                         | no       | all      | yes               |
| getAccessible<sup>deprecated from 4.0.11</sup>         | 接收当前路由对象并返回布尔值的函数，指示是否将标签标记为`accessible`。默认为`true` | function                         | no       | all      | yes               |
| getAccessibilityLabel<sup>deprecated from 4.0.11</sup> | 接收当前路由对象并返回标签按钮的无障碍标签的函数。如果指定了`route.accessibilityLabel`则默认使用，否则使用路由标题 | function                         | no       | all      | yes               |
| renderIcon<sup>deprecated from 4.0.11</sup>            | 接收当前路由对象、聚焦状态和颜色并返回要用作图标的自定义React元素的函数 | function                         | no       | all      | yes               |
| renderLabel<sup>deprecated from 4.0.11</sup>           | 接收当前路由对象、聚焦状态和颜色并返回要用作标签的自定义React元素的函数 | function                         | no       | all      | yes               |
| renderTabBarItem                                       | 接收`TabBarItemProps`对象并返回要用作标签按钮的自定义React元素的函数 | function                         | no       | all      | yes               |
| renderIndicator                                        | 接收当前路由对象并返回要用作标签指示器的自定义React元素的函数 | function                         | no       | all      | yes               |
| renderBadge<sup>deprecated from 4.0.11</sup>           | 接收当前路由对象并返回要用作徽章的自定义React元素的函数     | function                         | no       | all      | yes               |
| onTabPress                                             | 标签按下时执行的函数。接收按下标签的场景，可用于滚动到顶部等操作 | function                         | no       | all      | yes               |
| onTabLongPress                                         | 标签长按时执行的函数，用于显示包含更多选项的菜单等操作       | function                         | no       | all      | yes               |
| activeColor                                            | 活动标签中图标和标签的自定义颜色                              | string                           | no       | all      | yes               |
| inactiveColor                                          | 非活动标签中图标和标签的自定义颜色                            | string                           | no       | all      | yes               |
| pressColor                                             | Material涟漪效果的颜色（仅Android >= 5.0）                   | string                           | no       | Android  | no                |
| pressOpacity                                           | 按下标签的不透明度（仅iOS和Android < 5.0）                   | number                           | no       | all      | yes               |
| scrollEnabled                                          | 指示是否使标签栏可滚动的布尔值                                | boolean                          | no       | all      | yes               |
| bounces                                                | 指示标签栏滚动时是否具有弹跳效果的布尔值                      | boolean                          | no       | iOS      | no                |
| tabStyle                                               | 应用于标签栏中各个标签项的样式                                | object                           | no       | all      | yes               |
| indicatorStyle                                         | 应用于活动指示器的样式                                        | object                           | no       | all      | yes               |
| indicatorContainerStyle                                | 应用于指示器容器视图的样式                                    | object                           | no       | all      | yes               |
| labelStyle<sup>deprecated from 4.0.11</sup>            | 应用于标签项标签的样式                                        | object                           | no       | all      | yes               |
| contentContainerStyle                                  | 应用于标签内部容器的样式                                      | object                           | no       | all      | yes               |
| style (TabBar)                                         | 应用于标签栏容器的样式                                        | object                           | no       | all      | yes               |
| gap                                                    | 定义标签之间的间距                                            | number                           | no       | all      | yes               |
| direction<sup>4.0.11+</sup>                            | 布局的书写方向                                                | LocaleDirection                  | no       | all      | yes               |
| layout<sup>4.0.11+</sup>                               | -                                                            | Layout                           | no       | all      | yes               |
| options<sup>4.0.11+</sup>                              | -                                                            | Record<string, TabDescriptor<T>> | no       | all      | yes               |
## 遗留问题

- [x] 已解决： 页面滑动时，有概率卡在中间，无法自动回正[issue#5](https://github.com/react-native-oh-library/react-navigation/issues/5)
- [ ] TabBar中的bounces属性，不生效，无法实现滚动回弹效果[issue#34](https://github.com/react-native-oh-library/react-navigation/issues/34)

## 其他

- TabBar中的pressColor属性，不生效，无法实现按下更改颜色。 pressColor属性，是专门为Android平台设计的，这个属性在PlatformPressable中直接传递，在IOS上，pressColor属性没有直接对应的实现，IOS使用不同的机制来处理触摸反馈。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/main/packages/react-native-tab-view/LICENSE) ，请自由地享受和参与开源。