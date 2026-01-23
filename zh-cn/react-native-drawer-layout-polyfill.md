> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-drawer-layout-polyfill</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/rnc-archive/react-native-drawer-layout-polyfill">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/rnc-archive/react-native-drawer-layout-polyfill/tree/v2.0.0)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-drawer-layout-polyfill@2.0.0
```

#### **yarn**

```bash
yarn add react-native-drawer-layout-polyfill@2.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useState, useRef } from "react";
import { Button, Text, StyleSheet, View, TextInput } from "react-native";
import DrawerLayout from "react-native-drawer-layout-polyfill";

const App = () => {
  const drawerLayoutRef = useRef<{ openDrawer: () => void, closeDrawer: () => void }>(null);
  const [drawerPosition, setDrawerPosition] = useState("left");
  const [keyboardDismissMode, setKeyboardDismissMode] = useState("none");
  const [drawerLockMode, setDrawerLockMode] = useState("unlocked ");
  const [isOpen, setIsOpen] = useState("关闭 ");
  const [drawerSlideOutput, setDrawerSlideOutput] = useState("");
  const [drawerStateChangedOutput, setDrawerStateChangedOutput] = useState("");
  const [drawerWidth, setDrawerWidth] = useState(300);
  const [value, onChangeText] = useState("");

  const open = () => {
    drawerLayoutRef.current?.openDrawer();
  };

  const close = () => {
    drawerLayoutRef.current?.closeDrawer();
  };

  const changeDrawerPosition = () => {
    console.log("drawerPosition-修改弹框位置", drawerPosition);
    if (drawerPosition === "left") {
      setDrawerPosition("right");
    } else {
      setDrawerPosition("left");
    }
  };

  const changeDrawerHideKeyboard = () => {
    console.log("keyboardDismissMode-是否隐藏软键盘", keyboardDismissMode);
    if (keyboardDismissMode === "none") {
      setKeyboardDismissMode("on-drag");
    } else {
      setKeyboardDismissMode("none");
    }
  };

  const changeDrawerWidth = () => {
    console.log("drawerWidth-修改弹框宽度", drawerWidth);
    if (value && Number(value) >= 100) {
      setDrawerWidth(Number(value));
    }
  };

  const changeDrawerLockMode = (type: string) => {
    console.log("drawerLockMode-修改弹框锁定模式", type);
    setDrawerLockMode(type);
  };

  const handleDrawerOpen = (e: any) => {
    console.log("onDrawerOpen-打开弹框的回调");
    setIsOpen("打开");
  };

  const handleDrawerClose = (e: any) => {
    console.log("onDrawerClose-关闭弹框的回调");
    setIsOpen("关闭");
  };

  const handleDrawerSlide = (e: any) => {
    console.log("onDrawerSlide-导航视图发生交互时的回调函数");
    setDrawerSlideOutput(JSON.stringify(e.nativeEvent));
  };

  const handleDrawerStateChanged = (e: any) => {
    console.log("onDrawerStateChanged-导航视图的状态发生变化时的回调函数");
    setDrawerStateChangedOutput(JSON.stringify(e));
  };

  const navigationView = (
    <View style={styles.navigationContainer}>
      <Text style={styles.textCommon}>I'm in the Drawer!</Text>
      <Text style={styles.textCommon}>弹框状态:{isOpen}</Text>
      <Text style={styles.textCommon}>
        弹框打开关闭过程中触发:{drawerSlideOutput}
      </Text>
      <Text style={styles.textCommon}>
        弹框状态切换触发:{drawerStateChangedOutput}
      </Text>
      <Button
        style={styles.buttonMargin}
        title="关闭弹框"
        onPress={() => close()}
      />
    </View>
  );

  return (
    <DrawerLayout
      ref={drawerLayoutRef}
      drawerWidth={drawerWidth}
      drawerPosition={drawerPosition}
      renderNavigationView={() => navigationView}
      keyboardDismissMode={keyboardDismissMode}
      drawerLockMode={drawerLockMode}
      drawerBackgroundColor="red"
      statusBarBackgroundColor="blue"
      onDrawerOpen={handleDrawerOpen}
      onDrawerClose={handleDrawerClose}
      onDrawerSlide={handleDrawerSlide}
      onDrawerStateChanged={handleDrawerStateChanged}
    >
      <View style={styles.container}>
        <Text style={styles.textCommon}>
          设置导航视图的锁定模式:{drawerLockMode}
        </Text>
        <Text style={styles.textCommon}>
          是否隐藏软键盘:{keyboardDismissMode}
        </Text>
        <Text style={styles.textCommon}>弹框状态:{isOpen}</Text>
        <Text style={styles.textCommon}>
          弹框打开关闭过程中触发:{drawerSlideOutput}
        </Text>
        <Text style={styles.textCommon}>
          弹框状态切换触发:{drawerStateChangedOutput}
        </Text>
        <Button title="打开弹框" onPress={() => open()} />
        <View style={styles.buttonMargin}></View>
        <Button title="改变弹框位置" onPress={() => changeDrawerPosition()} />
        <View style={styles.buttonMargin}></View>
        <Button
          title="弹框动画过程中是否隐藏键盘"
          onPress={() => changeDrawerHideKeyboard()}
        />
        <View style={styles.buttonMargin}></View>
        <Button
          title="设置导航视图的锁定模式- unlocked "
          onPress={() => changeDrawerLockMode("unlocked")}
        />
        <View style={styles.buttonMargin}></View>
        <Button
          title="设置导航视图的锁定模式- locked-closed"
          onPress={() => changeDrawerLockMode("locked-closed")}
        />
        <View style={styles.buttonMargin}></View>
        <Button
          title="设置导航视图的锁定模式- locked-open"
          onPress={() => changeDrawerLockMode("locked-open")}
        />
        <View style={styles.buttonMargin}></View>
        <TextInput
          style={{
            height: 40,
            borderColor: "gray",
            borderWidth: 1,
            width: 300,
          }}
          onChangeText={(text) => onChangeText(text)}
          value={value}
        />
        <View style={styles.buttonMargin}></View>
        <Button title="修改弹框宽度" onPress={() => changeDrawerWidth()} />
      </View>
    </DrawerLayout>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
    paddingTop: 50,
    padding: 8,
  },
  navigationContainer: {
    flex: 1,
    paddingTop: 50,
    padding: 8,
  },
  textCommon: {
    marginBottom: 10,
    fontSize: 15,
  },
  buttonMargin: {
    marginBottom: 5,
  },
});

export default App;
```

## 约束与限制

### 兼容性

在以下版本验证通过

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-drawer-layout-polyfill](https://reactnative.dev/docs/drawerlayoutandroid)

| Name                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                        | Type     | Required | Platform    | HarmonyOS Support | note                                                   |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- | ------------------------------------------------------ |
| renderNavigationView     | 一种将渲染在屏幕侧边、可滑动唤出的导航视图。                                                                                                                                                                                                                                                                                                                                          | function | YES      | Android IOS | YES               |                                                        |
| drawerPosition           | 指定抽屉式导航栏滑入屏幕时对应的侧边方向。默认设置为左侧。枚举类型：('left', 'right')                                                                                                                                                                                                                                                                                                          | string   | NO       | Android IOS | YES               |                                                        |
| drawerWidth              | 指定抽屉的宽度，更准确地说，是从窗口边缘滑入的视图的宽度。                                                                                                                                                                                                                                                                                                             | number   | NO       | Android IOS | YES               |                                                        |
| keyboardDismissMode      | 决定拖动操作是否会收起软键盘。取值 none（默认值）时，拖动不会收起软键盘；取值 on-drag 时，拖动时软键盘即会收起。                                                                                                                                                                                                                                            | string   | NO       | Android IOS | YES               |                                                        |
| drawerLockMode           | 指定抽屉的锁定模式。抽屉可被锁定为三种状态：unlocked（默认）：抽屉会响应触摸手势，支持打开 / 关闭操作；locked-closed：抽屉保持关闭状态，不能使用手势打开；locked-open：抽屉保持打开状态，不能使用手势关闭。 | string   | NO       | Android IOS | YES               |                                                        |
| drawerBackgroundColor    | 指定抽屉的背景颜色，默认值为白色。若需设置抽屉的不透明度，请使用 rgba 颜色值。                                                                                                                                                                                                                                                                                                  | string   | NO       | Android IOS | YES               |                                                        |
| statusBarBackgroundColor | 使抽屉占据整个屏幕并绘制状态栏背景，以允许其在状态栏上方展开。此功能仅在 API 21 及以上版本生效，不支持 iOS 和鸿蒙系统。                                                                                                                                                                                                                       | string   | NO       | Android     | NO                | 该原生库仅支持安卓。|
| onDrawerOpen             | 导航视图被打开后的回调函数。                                                                                                                                                                                                                                                                                                                                                                      | function | NO       | Android IOS | YES               |                                                        |
| onDrawerClose            | 导航视图被关闭后的回调函数。                                                                                                                                                                                                                                                                                                                                                                      | function | NO       | Android IOS | YES               |                                                        |
| onDrawerSlide            | 导航视图发生交互时的回调函数。                                                                                                                                                                                                                                                                                                                                                         | function | NO       | Android IOS | YES               |                                                        |
| onDrawerStateChanged     | 导航视图的状态变化时的回调函数。有三种状态： idle，导航视图没有发生任何交互；dragging，导航视图正在进行交互； settling，导航视图正在发生交互，并且导航视图正在完成其关闭或打开动画。                                                                                                                                                                                                                                                            | function | NO       | Android IOS | YES               |                                                        |

## 方法

| Name        | Description        | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------ | -------- | ----------- | ----------------- |
| openDrawer  | 打开弹框。          | NO       | Android IOS | YES               |
| closeDrawer | 关闭弹框。          | NO       | Android IOS | YES               |

## 遗留问题

- [ ] 属性statusBarBackgroundColor 鸿蒙暂不支持。[issue#10](https://github.com/rnc-archive/react-native-drawer-layout-polyfill/issues/10)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://www.mit-license.org/) ，请自由地享受和参与开源。
