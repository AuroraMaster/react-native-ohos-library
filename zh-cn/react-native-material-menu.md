模板版本：v0.2.2

<p align="center">
  <h1 align="center"> 
    <code>react-native-material-menu</code> 
  </h1>
</p>

<p align="center">
    <a href="https://github.com/mxck/react-native-material-menu">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mxck/react-native-material-menu/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/mxck/react-native-material-menu)

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本                 | 支持RN版本 |
| ------------------------- | -------------------------- |
| 0.2.2 | 0.72/0.77 |

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-material-menu@2.0.0
```

#### **yarn**

```bash
yarn add react-native-material-menu@2.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。


```js
import React, { useState } from 'react';

import { View, Text } from 'react-native';
import { Menu, MenuItem, MenuDivider } from 'react-native-material-menu';

export default function App() {
  const [visible, setVisible] = useState(false);

  const hideMenu = () => setVisible(false);

  const showMenu = () => setVisible(true);

  return (
    <View style={{ height: '100%', alignItems: 'center', justifyContent: 'center' }}>
      <Menu
        visible={visible}
        anchor={<Text onPress={showMenu}>Show menu</Text>}
        onRequestClose={hideMenu}
      >
        <MenuItem onPress={hideMenu}>Menu item 1</MenuItem>
        <MenuItem onPress={hideMenu}>Menu item 2</MenuItem>
        <MenuItem disabled>Disabled item</MenuItem>
        <MenuDivider />
        <MenuItem onPress={hideMenu}>Menu item 4</MenuItem>
      </Menu>
    </View>
  );
}


```


## 约束与限制
### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Menu

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| children | 菜单中渲染的组件（必填）   | ReactNode  | yes |     all  |       yes|
| anchor | 触发菜单的按钮组件（必填）   |  ReactNode  | yes |     all  |       yes|
| visible |  当前菜单是否显示   | Boolean  | no |     all  |       yes|
| style | 菜单容器样式   | [ViewStyle](https://reactnative.dev/docs/view-style-props)  | no |     all  |       yes|
| onRequestClose | 菜单隐藏时的回调函数	   | () => void  | no |     all  |       yes|
| animationDuration | 显示/隐藏动画时长，默认300毫秒   | Number  | no |     all  |       yes|


### MenuItem

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| children | 菜单项内渲染的内容（必填）   | ReactNode  | yes |     all  |       yes|
| disabled | 是否禁用，默认false   | Boolean  | no |     all  |       yes|
| disabledTextColor | 禁用状态下的文字颜色，默认#bdbdbd   | String  | no |     all  |       yes|
| onPress | 点击菜单项时触发的回调函数 | ()=>void  | no |     all  |       yes|
| style | 菜单项容器样式  | [ViewStyle](https://reactnative.dev/docs/view-style-props)  | no |     all  |       yes|
| textStyle | 文字样式  | [TextStyle](https://reactnative.dev/docs/text-style-props)  | no |     all  |       yes|
| pressColor | 按压状态的颜色，默认#e0e0e0   | String  | no |     all  |       yes|


### MenuDivider

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| color | 分隔线颜色，默认'rgba(0,0,0,0.12)'（半透明黑色）   | String  | no |     all  |       yes|


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mxck/react-native-material-menu/blob/master/LICENSE) ，请自由地享受和参与开源。
