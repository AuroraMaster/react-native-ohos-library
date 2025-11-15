> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-status-bar-height</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ovr/react-native-status-bar-height">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ovr/react-native-status-bar-height/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-status-bar-height)

## 安装与使用
请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息 | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.6.1      | [@react-native-ohos/react-native-status-bar-height Releases](https://github.com/react-native-oh-library/react-native-status-bar-height/releases) | 0.72，0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# V2.6.1
npm install @react-native-ohos/react-native-status-bar-height
```

#### **yarn**

```bash
# V2.6.1
yarn add @react-native-ohos/react-native-status-bar-height
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```ts

import React, { useState } from "react";
import { View, Text, Button, PixelRatio } from "react-native";
import {TestCase, Tester} from "@rnoh/testerino"
import { getStatusBarHeight } from 'react-native-status-bar-height';

const App = (props) => {
    let [statusBarHeight,setData] = useState<number>(0);
    const getstatusbarHeight = () => {
    statusBarHeight = getStatusBarHeight(false);
    setData(statusBarHeight) 
    console.debug(statusBarHeight);
  };
  
  return (
    <Tester style={{flex: 1 , marginTop: 30}}>
      <TestCase itShould={"getstatusbarHeight"}>
        <View style={{ margin: 50, flexDirection: "column", justifyContent: "center" }}>
          <View>
            <Button
              title="getStatusBarHeight"
              onPress={() => getstatusbarHeight()}
            />
            <Text>{"statusBarHeight: "+JSON.stringify(statusBarHeight)+" dp"}</Text>
            <Text>{"statusBarHeight: "+JSON.stringify(PixelRatio.getPixelSizeForLayoutSize(statusBarHeight))+" px"}</Text>
          </View>
        </View>
      </TestCase>
    </Tester>
  );
};

export default App
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.6.1      | [@react-native-ohos/react-native-status-bar-height Releases](https://github.com/react-native-oh-library/react-native-status-bar-height/releases) | 0.72，0.77       |


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- |
| getStatusBarHeight | Called on each swipe event | `function` | yes | iOS,Android | yes |
| isIPhoneX | Whether it is an iPhoneX. | `function` |  yes | iOS | no |
| isIPhoneXMax | Whether it is an iPhoneX Max. | `function` |  yes | iOS | no |
| isIPhone12 | Whether it is an iPhone12. | `function` |  yes | IOS | no |
| isIPhone12Max | Whether it is an iPhone12 Max. | `function` |  yes | iOS | no |
| isIPhoneWithMonobrow | Whether it is an iPhone with Monobrow. | `function` |  yes | IOS | no |
| isExpo | whether to use Expo. | `function` |  yes | iOS,Android | no |


## 遗留问题

## 其他
isIPhoneX，isIPhoneXMax，isIPhone12，isIPhone12Max，isIPhoneWithMonobrow这些接口用于判断IPhone机型，Harmony不支持，未实现。

isExpo是判断是否使用Expo框架，Harmony不支持使用Expo框架，未实现。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ovr/react-native-status-bar-height/blob/master/LICENSE) ，请自由地享受和参与开源。

