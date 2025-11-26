> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-oh-tpl/react-native-popover-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/SteffeyDev/react-native-popover-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/SteffeyDev/react-native-popover-view/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-popover-view)

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-popover-view`，具体版本所属关系如下：
| Version                        | Package Name       | Repository          |  Release            |Supported RN Version  |
| ------------------------------ | ----------------   | ------------------- | ------------------- | -------------------- |
| 5.1.7  | @react-native-oh-tpl/react-native-popover-view | [Github](https://github.com/react-native-oh-library/react-native-popover-view) | [Github Releases](https://github.com/react-native-oh-library/react-native-popover-view/releases) | 0.72 |
| 6.1.1 | @react-native-ohos/react-native-popover-view   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-popover-view) | [GitCode Releases]() | 0.77 |

## 安装与使用

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### npm

```bash
# V5.1.7
npm install @react-native-oh-tpl/react-native-popover-view

# V6.1.1
npm install @react-native-ohos/react-native-popover-view
```

#### yarn

```bash
# V5.1.7
yarn add @react-native-oh-tpl/react-native-popover-view

# V6.1.1
yarn add @react-native-ohos/react-native-popover-view
```

<!-- tabs:end -->

快速使用：

```typescript
import React, { useState } from 'react';
import {View, TouchableOpacity, Text, Button, Easing } from 'react-native';
import Popover, {PopoverMode, PopoverPlacement, Rect } from 'react-native-popover-view';

const PopoverDemo = () => {
    const [showPopoverA, setShowPopoverA] = useState(false);
    const [showPopoverB, setShowPopoverB] = useState(false);
    const [showPopoverC, setShowPopoverC] = useState(false);
    const [onOpenStart, setOnOpenStart] = useState(111);
    const [onOpenComplete, setOnOpenComplete] = useState(111);
    const [onCloseStart, setOnCloseStart] = useState(111);
    const [onCloseComplete, setOnCloseComplete] = useState(111);
    const [offsetValue, setOffsetValue] = useState(10);
    return (
        <View>
            <TouchableOpacity>
                <Text>test:from、isVisible</Text>
                <Button
                title= 'testA'
                onPress= {() => setShowPopoverA(true)}
                color= '#841584'
                />
            </TouchableOpacity>
            <Popover
              from= {new Rect(5,100,20,40)}
              isVisible= {showPopoverA}
              onRequestClose={() => {setShowPopoverA(false)}}
              >
              <Text>This is the contents of the popoverA</Text>
            </Popover>
            <TouchableOpacity>
                <Text>test:mode、offset、placement、popoverShift、popoverStyle、backgroundStyle、arrowSize、arrowShift、animationConfig</Text>
                <Button
                onPress = {() => setShowPopoverB(true)}
                title = 'testB'
                color = '#cc15cc'
                />
            </TouchableOpacity>
            <Popover
              from = {new Rect(5,100,20,40)}
              isVisible = {showPopoverB}
              mode = {PopoverMode.RN_MODAL}
              offset = {10}
              placement= {PopoverPlacement.Top}
              popoverShift= {{x:1}}
              popoverStyle= {{backgroundColor: '#f00'}}
              backgroundStyle= {{backgroundColor: '#00f'}}
              arrowSize= {{width:30,height:8}}
              arrowShift= {2}
              animationConfig= {{duration: 600,easing:Easing.inOut(Easing.quad)}}
              onRequestClose= {() => {setShowPopoverB(false)}}
              >
              <Text>This is the contents of the popoverB</Text>
            </Popover>

            <TouchableOpacity>
                <Text>test:displayArea、displayAreaInsets、onOpenStart、onOpenComplete、onRequestClose、onCloseStart、onCloseComplete、onPositionChange、debug</Text>
                <Button
                onPress = {() => setShowPopoverC(true)}
                title = 'testC'
                color = '#87cc94'
                />
            </TouchableOpacity>
            <Popover
              from = {new Rect(5,100,20,40)}
              isVisible = {showPopoverC}
              offset = {offsetValue}
              debug = {true}
              displayArea = {new Rect(50,50,50,50)}
              displayAreaInsets = {{top:20}}
              onOpenStart = {() => {setOnOpenStart(222)}}
              onOpenComplete= {() => {setOnOpenComplete(222)}}
              onRequestClose= {() => {setShowPopoverC(false)}}
              onCloseStart= {() => {setOnCloseStart(222)}}
              onCloseComplete= {() => {setOnCloseComplete(222)}}
              onPositionChange= {() => {setOnCloseStart(222)}}
            >
              <Text>This is the contents of the popoverC</Text>
            </Popover>
            <Text>onOpenStart {onOpenStart}</Text>
            <Text>onOpenComplete {onOpenComplete}</Text>
            <Text>onCloseStart {onCloseStart}</Text>
            <Text>onCloseComplete {onCloseComplete}</Text>
            <Text>onPositionChange {offsetValue}</Text>
            <Button
            onPress = {() => setOffsetValue(offsetValue === 10 ? 20 : 10)}
            title = 'change position'
            color = '#876664'
            />
        </View>
      );
}

export default PopoverDemo;
```

## 约束与限制

### 兼容性
要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在下述版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;
2. RNOH：0.72.96; SDK：HarmonyOS 5.1.1 Release SDK; IDE：DevEco Studio 5.1.1.840; ROM：6.0.0;
3. RNOH：0.77.18; SDK：HarmonyOS 5.1.1 Release SDK; IDE：DevEco Studio 5.1.1.840; ROM：6.0.0;

### 属性&方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                 | Description                                                                                                                                                                                                                                                                                                                                                                    | Type                  | Required | Platform | HarmonyOS Support | remark         |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------- | -------- | -------- | ----------------- | -------------- |
| from                 | 弹出层锚点源。详见下方 From 章节。                                                                                                                                                                                                                                                                                                                                                | multiple              | no       | All      | yes               |
| isVisible            | 显示/隐藏弹出层。如果 `from` 不是可触摸组件或使用 `showPopover` 调用的函数，则必需。如果提供了此参数，无论 `from` 如何设置，都将优先使用此参数。                                                                                                                                                                                                                              | bool                  | no       | All      | yes               |
| placement            | 弹出层定位方式，可选值为 'top'、'bottom'、'left'、'right'、'floating' 或 'auto'。指定为 'auto' 时，会自动尝试确定最佳位置以确保弹出层在 `displayArea` 内完全可见。如果传入选项数组，则会选择第一个能容纳内容的选项。                                                                                                                                                          | string OR string list | no       | All      | yes               |
| mode                 | 模式，可选值为：'rn-modal'、'js-modal'、'tooltip'。详见下方 Mode 章节。                                                                                                                                                                                                                                                                                                      | string                | no       | All      | yes               |
| offset               | 弹出层偏离锚点源的距离。如果弹出层是居中的则不适用。                                                                                                                                                                                                                                                                                                                           | number                | no       | All      | yes               |
| popoverStyle         | 弹出层自身的样式。可以覆盖圆角、背景色或任何 View 支持的样式属性。                                                                                                                                                                                                                                                                                                             | object                | no       | All      | yes               |
| popoverShift         | 在各个方向上平移弹出层的量，作为乘数。格式为 { x: -1 到 1, y: -1 到 1 } 的对象，x 和 y 均为可选。值为 -1 将弹出层完全向左/上平移，值为 1 则向右/下平移。当前仅当 `placement` 为 'floating' 时适用，但在未来版本中将适用于所有定位方式。                                                                                                                                    | object                | no       | All      | yes               |
| backgroundStyle      | 背景视图的样式。默认为黑色背景，透明度 0.5。                                                                                                                                                                                                                                                                                                                                   | object                | no       | All      | yes               |
| arrowSize            | 箭头尺寸，是一个包含 width 和 height 属性的对象。箭头的 width 是指箭头接触弹出层边缘的尺寸（等腰三角形的底边），而 height 则覆盖从弹出层到锚点源视图的距离，与弹出层的位置无关。可以使用 { width: 0, height: 0 } 来完全隐藏箭头。                                                                                                                                           | object                | no       | All      | yes               |
| arrowShift           | 箭头向一侧平移的量，作为乘数。值为 -1 将箭头完全平移至锚点源视图的左（或上）角，值为 1 则完全平移至右（或下）角。值为 0.5 或 -0.8 会使其部分偏向一侧。                                                                                                                                                                                                                         | object                | no       | All      | yes               |
| onOpenStart          | 打开动画开始时触发的回调函数（动画开始前）                                                                                                                                                                                                                                                                                                                                     | function              | no       | All      | yes               |
| onOpenComplete       | 打开动画结束时触发的回调函数（动画结束后）                                                                                                                                                                                                                                                                                                                                     | function              | no       | All      | yes               |
| onRequestClose       | 当用户点击弹出层外部（背景）或点击 Android 系统返回按钮时触发的回调函数                                                                                                                                                                                                                                                                                                       | function              | no       | All      | yes               |
| onCloseStart         | 弹出层开始关闭时触发的回调函数（动画开始前）                                                                                                                                                                                                                                                                                                                                   | function              | no       | All      | yes               |
| onCloseComplete      | 弹出层完全关闭后触发的回调函数（动画结束后）                                                                                                                                                                                                                                                                                                                                   | function              | no       | All      | yes               |
| onPositionChange     | 弹出层位置移动完成后触发的回调函数（动画结束后）                                                                                                                                                                                                                                                                                                                               | function              | no       | All      | yes               |
| animationConfig      | 包含可传递给 Animated.timing 的任何配置选项的对象（例如 { duration: 600, easing: Easing.inOut(Easing.quad) }）。传入的配置选项将覆盖所有动画的默认值。                                                                                                                                                                                                                      | object                | no       | All      | yes               |
| displayArea          | 允许显示弹出层的区域。默认情况下，会自动计算为显示区域的大小，如果模式不是 'rn-modal'，则为父组件的大小。                                                                                                                                                                                                                                                                     | rect                  | no       | All      | yes               |
| displayAreaInsets    | 应用于显示区域的内边距。弹出层不允许超出显示区域减去内边距的范围。                                                                                                                                                                                                                                                                                                             | object                | no       | All      | yes               |
| statusBarTranslucent | 仅适用于 Android 上的 'rn-modal' 模式。决定背景是否应延伸到状态栏下方。此属性会传递给 RN Modal 组件，具体可参考其文档。                                                                                                                                                                                                                                                       | bool                  | no       | Android  | no                | 原库仅支持安卓 |
| verticalOffset<sup>deprecated from 6.1.1</sup> | 在屏幕上垂直移动弹出层的量，用于修正 Android 上偶尔出现的问题。在某些 Android 配置中，可能需要设置 verticalOffset 为 -StatusBar.currentHeight 以使弹出层从正确的位置开始显示。对于其他情况下的弹出层移动，应使用 offset 属性。                                                                                                                                              | number                | no       | Android  | no                | 原库仅支持安卓 |
| debug                | 设置为 true 可在控制台开启调试日志输出。这对于排查弹出层不显示的原因非常有用。                                                                                                                                                                                                                                                                                                 | bool                  | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/SteffeyDev/react-native-popover-view/blob/master/LICENSE) ，请自由地享受和参与开源。
