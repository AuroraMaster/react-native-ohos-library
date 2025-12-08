> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@openspacelabs/react-native-zoomable-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/openspacelabs/react-native-zoomable-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/openspacelabs/react-native-zoomable-view/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/openspacelabs/react-native-zoomable-view)

| Version                 | Support RN version                 |
| ------------------------- | -------------------------- |
| 2.4.2                 |  0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @openspacelabs/react-native-zoomable-view@2.4.2
```

#### **yarn**

```bash
yarn add @openspacelabs/react-native-zoomable-view@2.4.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { View, StyleSheet, Image, Animated } from "react-native";
import React from "react";
import { ReactNativeZoomableView } from "@openspacelabs/react-native-zoomable-view";

export function ReactNativeZoomableViewExample() {
  const zoomAnimatedValue = React.useRef(new Animated.Value(1)).current;
  const scale = Animated.divide(1, zoomAnimatedValue);
  return (
    <View style={styles.container}>
      <View style={styles.box}>
        <ReactNativeZoomableView
          maxZoom={30}
          initialZoom={1.5}
          contentWidth={300}
          contentHeight={150}
          panBoundaryPadding={500}
          style={{ padding: 10, backgroundColor: "red" }}
        >
          <View style={styles.contents}>
            <Image
              style={styles.img}
              source={require("../assets/placeholder2000x2000.jpg")}
            />

            {[20, 40, 60, 80].map((left) =>
              [20, 40, 60, 80].map((top) => (
                <Animated.View
                  key={`${left}x${top}`}
                  style={[
                    styles.marker,
                    { left: `${left}%`, top: `${top}%` },
                    { transform: [{ scale }] },
                  ]}
                />
              ))
            )}
          </View>
        </ReactNativeZoomableView>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
    padding: 20,
  },
  contents: {
    flex: 1,
    alignSelf: "stretch",
  },
  box: {
    borderWidth: 5,
    flexShrink: 1,
    height: 500,
    width: 310,
  },
  img: {
    width: "100%",
    height: "100%",
    resizeMode: "contain",
  },
  marker: {
    position: "absolute",
    top: "50%",
    left: "50%",
    width: 20,
    height: 20,
    marginLeft: -10,
    marginTop: -10,
    borderRadius: 10,
    backgroundColor: "white",
    borderWidth: 2,
  },
});
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.26; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.300; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                             | Type     | Description                                                                                                                                                                                                                                                                                                                          | Required | Platform | HarmonyOS Support |
| -------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | ----------------- |
| zoomEnabled                      | boolean  | 可用于动态启用或禁用缩放功能                                                                                                                                                                                                                                                                             | no       | All      | yes               |
| panEnabled                       | boolean  | 可用于动态启用或禁用平移功能                                                                                                                                                                                                                                                                             | no       | All      | yes               |
| initialZoom                      | number   | 启动时的初始缩放级别                                                                                                                                                                                                                                                                                                        | no       | All      | yes               |
| maxZoom                          | number   | 最大可能的缩放级别（放大）。可以设置为null以允许无限缩放                                                                                                                                                                                                                                                | no       | All      | yes               |
| minZoom                          | number   | 最小可能的缩放级别（缩小）                                                                                                                                                                                                                                                                                               | no       | All      | yes               |
| disablePanOnInitialZoom          | boolean  | 如果为true，则当缩放级别等于初始缩放级别时禁用平移                                                                                                                                                                                                                                                      | no       | All      | yes               |
| doubleTapDelay                   | number   | 多少延迟仍会被识别为双击（毫秒                                                                                                                                                                                                                                                                         | no       | All      | yes               |
| doubleTapZoomToCenter            | boolean  | 如果为true，双击将始终缩放到视图中心，而不是双击的方向                                                                                                                                                                                                                          | no       | All      | yes               |
| bindToBorders                    | boolean  | 如果为true，则确保对象保持在框边界内                                                                                                                                                                                                                                                                           | no       | All      | yes               |
| zoomStep                         | number   | 双击时应应用多少缩放                                                                                                                                                                                                                                                                                        | no       | All      | yes               |
| pinchToZoomInSensitivity         | number   | 缩放的阻力（灵敏度）级别（0 - 10）- 数值越高越不敏感                                                                                                                                                                                                                                                 | no       | All      | yes               |
| pinchToZoomOutSensitivity        | number   | 缩小的阻力（灵敏度）级别（0 - 10）- 数值越高越不敏感                                                                                                                                                                                                                                               | no       | All      | yes               |
| movementSensibility              | number   | 移动视图周围的阻力应该是多少？（0.5 - 5）- 数值越高越不敏感                                                                                                                                                                                                                                               | no       | All      | yes               |
| initialOffsetX                   | number   | 图像应该开始的水平偏移量                                                                                                                                                                                                                                                                                      | no       | All      | yes               |
| initialOffsetY                   | number   | 像应该开始的垂直偏移量                                                                                                                                                                                                                                                                                        | no       | All      | yes               |
| contentHeight                    | number   | 如果要将缩放主题内**居中**内容的高度视为缩放主题的高度，请指定                                                                                                                                                                                                             | no       | All      | yes               |
| contentWidth                     | number   | 如果要将缩放主题内**居中**内容的宽度视为缩放主题的宽度，请指定                                                                                                                                                                                                                | no       | All      | yes               |
| panBoundaryPadding               | number   | 在某些缩放比例下，内容边缘距离容器边缘太近，导致难以平移到内容边缘并与之交互。为了解决这个问题，我们希望允许内容在距离容器边缘稍远一点的地方进行平移。因此有了"平移边界填充"，以像素为单位测量 | no       | All      | yes               |
| longPressDuration                | number   | 按下多长时间（毫秒）被视为长按                                                                                                                                                                                                                                                                              | no       | All      | yes               |
| visualTouchFeedbackEnabled       | boolean  | 触摸时是否显示触觉反馈圆圈                                                                                                                                                                                                                                                                                     | no       | All      | yes               |
| onTransform                      | function | 当变换配置（缩放级别和偏移量）发生变化时将被调用                                                                                                                                                                                                                                                 | no       | All      | yes               |
| onDoubleTapBefore                | function | 在双击开始时将被调用                                                                                                                                                                                                                                                                                         | no       | All      | yes               |
| onDoubleTapAfter                 | function | 在双击结束时将被调用                                                                                                                                                                                                                                                                                            | no       | All      | yes               |
| onShiftingBefore                 | function | 当用户点击并移动视图时调用，但在我们的视图移动工作开始之前（所以如果您需要中断移动，这里是实现的地方）                                                                                                                                                                           | no       | All      | yes               |
| onShiftingAfter                  | function | 当用户点击并移动视图时调用，但在值已经改变之后                                                                                                                                                                                                                                         | no       | All      | yes               |
| onShiftingEnd                    | function | 当用户停止点击和移动手势时调用                                                                                                                                                                                                                                                                               | no       | All      | yes               |
| onZoomBefore                     | function | 将在用户捏合屏幕时调用，但在我们的缩放功能启动之前（如果您需要中断缩放，这里是可以实现的地方）                                                                                                                                                                                     | no       | All      | yes               |
| onZoomAfter                      | function | 将在用户捏合屏幕时调用，但在值已经改变之后                                                                                                                                                                                                                                         | no       | All      | yes               |
| onZoomEnd                        | function | 将在捏合缩放结束后调用                                                                                                                                                                                                                                                                                          | no       | All      | yes               |
| onLongPress                      | function | 将在用户按住图像一段时间后调用                                                                                                                                                                                                                                                                       | no       | All      | yes               |
| onStartShouldSetPanResponder     | function | 确定当手指按下时，视图组是否响应触摸事件                                                                                                                                                                                                                                                 | no       | All      | yes               |
| onPanResponderGrant              | function | 手势已开始                                                                                                                                                                                                                                                                                                              | no       | All      | yes               |
| onPanResponderEnd                | function | 将在手势结束时调用（更准确地说，是在pan responder"释放"时）                                                                                                                                                                                                                                                       | no       | All      | yes               |
| onPanResponderTerminate          | function | 将在手势被另一个处理器强制中断时调用                                                                                                                                                                                                                                                              | no       | All      | yes               |
| onPanResponderTerminationRequest | function | 回调函数，询问手势是否应被其他处理器中断                                                                                                                                                                                                                                                         | no       | IOS      | no               |
| onPanResponderMove               | function | 用户触摸移动时将被调用                                                                                                                                                                                                                                                                                        | no       | All      | yes               |
| onShouldBlockNativeResponder     | function | 返回此组件是否应阻止原生组件成为JS响应者                                                                                                                                                                                                                                         | no       | All      | yes               |
| zoomTo                           | function | 将缩放级别更改为特定数值                                                                                                                                                                                                                                                                                          | no       | All      | yes               |
| zoomBy                           | function | 相对于当前级别更改缩放级别（使用正数放大，负数缩小）                                                                                                                                                                                                                 | no       | All      | yes               |
| moveTo                           | function | 将缩放部分移动到特定点（相对于x: 0, y: 0的像素）                                                                                                                                                                                                                                                            | no       | All      | yes               |
| moveBy                           | function | 按特定像素数量移动缩放部分                                                                                                                                                                                                                                                                                    | no       | All      | yes               |
| disableMomentum             | boolean | 拖动结束后是否启用惯性滑动                                                                                                                                                                                                                                                                                     | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/openspacelabs/react-native-zoomable-view/blob/master/LICENSE) ，请自由地享受和参与开源。