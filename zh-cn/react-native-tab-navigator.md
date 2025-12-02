> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-tab-navigator</code> </h1>
</p>

请到三方库的 Releases 发布地址查看配套的版本信息：

| Version                        | Package Name                             | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -----------
| <=0.3.4@deprecated | @react-native-oh-tpl/react-native-tab-navigator  | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-tab-navigator) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-tab-navigator/releases) | 0.72  |
| 0.3.4 | @react-native-ohos/react-native-tab-navigator  | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-tab-navigator) | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-tab-navigator/releases) | 0.72  |
| 0.4.0 | @react-native-ohos/react-native-tab-navigator  | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-tab-navigator) | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-tab-navigator/releases) | 0.77  |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-tab-navigator
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-tab-navigator
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```ts
import React, { useState } from "react";
import { View, StyleSheet, Text, Image } from "react-native";
import TabNavigator from "react-native-tab-navigator";

const HOME_IMAGE = [
  require("../assets/tab-navigator/home_unselected.svg"),
  require("../assets/tab-navigator/home_selected.svg"),
];
const PROFILE_IMAGE = [
  require("../assets/tab-navigator/profile_unselected.svg"),
  require("../assets/tab-navigator/profile_selected.svg"),
];

const App = () => {
  const [selectedTab, setSelectedTab] = useState("home");
  return (
    <View style={styles.container}>
      <TabNavigator style={styles.tabContainer}>
        <TabNavigator.Item
          selected={selectedTab === "home"}
          title="Home"
          selectedTitleStyle={{ color: "#3496f0" }}
          renderIcon={() => (
            <Image source={HOME_IMAGE[0]} style={styles.iconSize} />
          )}
          renderSelectedIcon={() => (
            <Image source={HOME_IMAGE[1]} style={styles.iconSize} />
          )}
          onPress={() => setSelectedTab("home")}
        >
          <Home />
        </TabNavigator.Item>
        <TabNavigator.Item
          selected={selectedTab === "profile"}
          title="Profile"
          selectedTitleStyle={{ color: "#3496f0" }}
          renderIcon={() => (
            <Image source={PROFILE_IMAGE[0]} style={styles.iconSize} />
          )}
          renderSelectedIcon={() => (
            <Image source={PROFILE_IMAGE[1]} style={styles.iconSize} />
          )}
          onPress={() => setSelectedTab("profile")}
        >
          <Profile />
        </TabNavigator.Item>
      </TabNavigator>
    </View>
  );
};

function Home() {
  return (
    <View style={styles.tabContainer}>
      <Text style={styles.welcome}>Home</Text>
    </View>
  );
}

function Profile() {
  return (
    <View style={styles.tabContainer}>
      <Text style={styles.welcome}>Profile</Text>
    </View>
  );
}

export default App;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：
1. RNOH：0.72.26; SDK：HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio: 5.0.3.300SP2; ROM：3.0.0.25;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release; IDE: DevEco Studio 6.0.0.858; ROM：6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### TabNavigator props

| Name              | Description                     | Type           | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------- | -------------- | -------- | ----------- | ----------------- |
| sceneStyle        | 定义渲染场景的样式       | object (style) | No       | iOS/Android | Yes               |
| tabBarStyle       | 定义TabBar的样式         | object (style) | No       | iOS/Android | Yes               |
| tabBarShadowStyle | 定义tabBar的阴影样式  | object (style) | No       | iOS/Android | Yes               |
| hidesTabTouch     | 禁用Tab的onPress透明度 | boolean        | No       | iOS/Android | Yes               |

### TabNavigator.Item props

| Name               | Description                                        | Type             | Required | Platform    | HarmonyOS Support |
| ------------------ | -------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| renderIcon         | 返回Item图标                                  | function         | No       | iOS/Android | Yes               |
| renderSelectedIcon | 返回选中的Item图标                         | function         | No       | iOS/Android | Yes               |
| badgeText          | Item徽章的文本                                | string or number | No       | iOS/Android | Yes               |
| renderBadge        | 返回Item徽章                                 | function         | No       | iOS/Android | Yes               |
| title              | Item标题                                         | string           | No       | iOS/Android | Yes               |
| titleStyle         | Item标题的样式                             | style            | No       | iOS/Android | Yes               |
| selectedTitleStyle | 选中Item标题的样式                    | style            | No       | iOS/Android | Yes               |
| tabStyle           | tab的样式                                    | style            | No       | iOS/Android | Yes               |
| selected           | 返回item是否被选中                | boolean          | No       | iOS/Android | Yes               |
| onPress            | Item的onPress方法                            | function         | No       | iOS/Android | Yes               |
| allowFontScaling   | 允许标题字体缩放                       | boolean          | No       | iOS/Android | Yes               |
| accessible         | 指示此item是否为辅助功能元素 | boolean          | No       | iOS/Android | Yes               |
| accessibilityLabel | 覆盖屏幕阅读器的文本                   | string           | No       | iOS/Android | Yes               |
| testID             | 用于在端到端测试中定位此item       | string           | No       | iOS/Android | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ptomasroos/react-native-tab-navigator/blob/master/LICENSE) ，请自由地享受和参与开源。

