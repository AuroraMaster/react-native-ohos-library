> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-swipe-gestures</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/glepur/react-native-swipe-gestures">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/glepur/react-native-swipe-gestures?tab=MIT-1-ov-file">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/glepur/react-native-swipe-gestures)

| 三方库版本                 | 支持RN版本                 |
| ------------------------- | -------------------------- |
| 1.0.5               |  0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

####  npm

```bash
npm install react-native-swipe-gestures@^1.0.5
```

#### yarn

```bash
yarn add react-native-swipe-gestures@^1.0.5
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
'use strict';

import React, {Component} from 'react';
import {View, Text} from 'react-native';
import GestureRecognizer, {swipeDirections} from 'react-native-swipe-gestures';

class SomeComponent extends Component {

  constructor(props) {
    super(props);
    this.state = {
      myText: 'I\'m ready to get swiped!',
      gestureName: 'none',
      backgroundColor: '#fff'
    };
  }

  onSwipeUp(gestureState) {
    this.setState({myText: 'You swiped up!'});
  }

  onSwipeDown(gestureState) {
    this.setState({myText: 'You swiped down!'});
  }

  onSwipeLeft(gestureState) {
    this.setState({myText: 'You swiped left!'});
  }

  onSwipeRight(gestureState) {
    this.setState({myText: 'You swiped right!'});
  }

  onSwipe(gestureName, gestureState) {
    const {SWIPE_UP, SWIPE_DOWN, SWIPE_LEFT, SWIPE_RIGHT} = swipeDirections;
    this.setState({gestureName: gestureName});
    switch (gestureName) {
      case SWIPE_UP:
        this.setState({backgroundColor: 'red'});
        break;
      case SWIPE_DOWN:
        this.setState({backgroundColor: 'green'});
        break;
      case SWIPE_LEFT:
        this.setState({backgroundColor: 'blue'});
        break;
      case SWIPE_RIGHT:
        this.setState({backgroundColor: 'yellow'});
        break;
    }
  }

  render() {

    const config = {
      velocityThreshold: 0.3,
      directionalOffsetThreshold: 80
    };

    return (
      <GestureRecognizer
        onSwipe={(direction, state) => this.onSwipe(direction, state)}
        onSwipeUp={(state) => this.onSwipeUp(state)}
        onSwipeDown={(state) => this.onSwipeDown(state)}
        onSwipeLeft={(state) => this.onSwipeLeft(state)}
        onSwipeRight={(state) => this.onSwipeRight(state)}
        config={config}
        style={{
          flex: 1,
          backgroundColor: this.state.backgroundColor
        }}
        >
        <Text>{this.state.myText}</Text>
        <Text>onSwipe callback received gesture: {this.state.gestureName}</Text>
      </GestureRecognizer>
    );
  }
}

export default SomeComponent;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
2. RNOH：0.77.17; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

Can be passed within optional `config` property.

| Params                     | Default | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| -------------------------- | ------- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| velocityThreshold          | 0.3     | 触发滑动手势必须达到的速度阈值（`gestureState` 的 `vx` 和 `vy` 属性） | Number | No       | IOS/Android | yes               |
| directionalOffsetThreshold | 80      | 触发滑动手势时不应超过的绝对偏移量（水平滑动为 `dy`，垂直滑动为 `dx`） | Number | No       | IOS/Android | yes               |
| gestureIsClickThreshold    | 5       | 手势不被视为点击操作必须达到的绝对距离（`gestureState` 的 `dx` 或 `dy` 属性） | Number | No       | IOS/Android | yes               |

## Methods

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| name         | Params       | Description                              | Type   | Required | Platform    | HarmonyOS Suppor |
| ------------ | ------------ | ---------------------------------------- | ------ | -------- | ----------- | ---------------- |
| onSwipe      | gestureState | 从 PanResponder 接收到的滑动手势状态   | Object | No       | IOS/Android | yes              |
| onSwipeUp    | gestureState | 从 PanResponder 接收到的向上滑动手势    | Object | No       | IOS/Android | yes              |
| onSwipeDown  | gestureState | 从 PanResponder 接收到的向下滑动手势  | Object | No       | IOS/Android | yes              |
| onSwipeLeft  | gestureState | 从 PanResponder 接收到的向左滑动手势  | Object | No       | IOS/Android | yes              |
| onSwipeRight | gestureState | 从 PanResponder 接收到的向右滑动手势 | Object | No       | IOS/Android | yes              |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/glepur/react-native-swipe-gestures?tab=MIT-1-ov-file) ，请自由地享受和参与开源。