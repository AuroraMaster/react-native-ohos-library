> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-tab-navigator</code> </h1>
</p>
Please visit the Release release address of the third-party library to view the corresponding version information:

| Version                        | Package Name                             | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -----------
| <=0.3.4@deprecated | @react-native-oh-tpl/react-native-tab-navigator  | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-tab-navigator) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-tab-navigator/releases) | 0.72  |
| 0.3.4 | @react-native-ohos/react-native-tab-navigator  | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-tab-navigator) | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-tab-navigator/releases) | 0.72  |
| 0.4.0 | @react-native-ohos/react-native-tab-navigator  | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-tab-navigator) | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-tab-navigator/releases) | 0.77  |

## Installation and Usage

Go to the project directory and execute the following instruction:



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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

## Constraints

### Compatibility

This document is verified based on the following versions:
1. RNOH：0.72.26; SDK：HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio: 5.0.3.300SP2; ROM：3.0.0.25;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release; IDE: DevEco Studio 6.0.0.858; ROM：6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### TabNavigator props

| Name              | Description                     | Type           | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------- | -------------- | -------- | ----------- | ----------------- |
| sceneStyle        | define for rendered scene       | object (style) | No       | iOS/Android | Yes               |
| tabBarStyle       | define style for TabBar         | object (style) | No       | iOS/Android | Yes               |
| tabBarShadowStyle | define shadow style for tabBar  | object (style) | No       | iOS/Android | Yes               |
| hidesTabTouch     | disable onPress opacity for Tab | boolean        | No       | iOS/Android | Yes               |

### TabNavigator.Item props

| Name               | Description                                        | Type             | Required | Platform    | HarmonyOS Support |
| ------------------ | -------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| renderIcon         | returns Item icon                                  | function         | No       | iOS/Android | Yes               |
| renderSelectedIcon | returns selected Item icon                         | function         | No       | iOS/Android | Yes               |
| badgeText          | text for Item badge                                | string or number | No       | iOS/Android | Yes               |
| renderBadge        | returns Item badge                                 | function         | No       | iOS/Android | Yes               |
| title              | Item title                                         | string           | No       | iOS/Android | Yes               |
| titleStyle         | styling for Item title                             | style            | No       | iOS/Android | Yes               |
| selectedTitleStyle | styling for selected Item title                    | style            | No       | iOS/Android | Yes               |
| tabStyle           | styling for tab                                    | style            | No       | iOS/Android | Yes               |
| selected           | return whether the item is selected                | boolean          | No       | iOS/Android | Yes               |
| onPress            | onPress method for Item                            | function         | No       | iOS/Android | Yes               |
| allowFontScaling   | allow font scaling for title                       | boolean          | No       | iOS/Android | Yes               |
| accessible         | indicates if this item is an accessibility element | boolean          | No       | iOS/Android | Yes               |
| accessibilityLabel | override text for screen readers                   | string           | No       | iOS/Android | Yes               |
| testID             | used to locate this item in end-to-end-tests       | string           | No       | iOS/Android | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ptomasroos/react-native-tab-navigator/blob/master/LICENSE).
