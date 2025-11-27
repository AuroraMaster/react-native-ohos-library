<p align="center">
  <h1 align="center"> <code>react-countdown-circle-timer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/vydimitrov/react-countdown-circle-timer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vydimitrov/react-countdown-circle-timer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/vydimitrov/react-countdown-circle-timer)

## 安装与使用
请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本| 支持RN版本 |
| ---------- | ---------- |
| 3.2.1      | 0.72       |
| 3.2.1      | 0.77       |

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-countdown-circle-timer@3.2.1
```

#### **yarn**

```bash
yarn add react-native-countdown-circle-timer@3.2.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { View, StyleSheet, Button, Text, ScrollView } from "react-native";
import { CountdownCircleTimer } from "react-native-countdown-circle-timer";

export function SwitchDemo() {
  const [isPlaying, setIsPlaying] = useState(true);
  const [count, setCount] = useState(15);

  return (
    <View style={styles.container}>
      <CountdownCircleTimer
        isPlaying={isPlaying}
        duration={count}
        initialRemainingTime={6}
        isSmoothColorTransition={false}
        colors="#aabbcc"
        onUpdate={(remainingTime) => {
          console.log("Counter is ", count);
          console.log("Remaining time is ", remainingTime);
        }}
        onComplete={() => ({ shouldRepeat: true })}
      >
        {({ remainingTime }) => remainingTime}
      </CountdownCircleTimer>
      <Button
        onPress={() => setIsPlaying((prev) => !prev)}
        title={"Toggle Playing"}
      ></Button>
      <Button
        onPress={() => setCount((prev) => (prev += 5))}
        title={"Count"}
      ></Button>
    </View>
  );
}
const styles = StyleSheet.create({
  container: {
    alignItems: "center",
    justifyContent: "center",
    backgroundColor: "#fff",
  },
});
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg-capi.md#link)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.29;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 Yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|          名称           |                                                                                         描述                                                                                         |              类型               | 是否必需 |  支持的平台   | 是否支持HarmonyOS |
| :---------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------: | :------: | :---------: | :---------------: |
|        duration         |                                                                                倒计时持续时间（秒）                                                                                |             number              |   Yes    | Android/iOS |        Yes        |
|         colors          |                      colors 属性可以是：（任意格式的单一有效颜色或渐变的 URL；HEX 格式的颜色数组。至少应提供 2 种颜色）                      |       `string & string[]`       |    No    | Android/iOS |        Yes        |
|       colorsTime        | 表示颜色应切换到下一种颜色的时间。第一个数字是倒计时时长，最后一个数字是 0 或目标值。仅在 colors 是 HEX 颜色数组时有效 |            number[]             |    No    | Android/iOS |        Yes        |
|        isPlaying        |                                                                                   播放或暂停动画                                                                                   |             boolean             |    No    | Android/iOS |        Yes        |
|  initialRemainingTime   |                                                             如果与持续时间不同，请设置初始剩余时间                                                             |             number              |    No    | Android/iOS |        Yes        |
|     updateInterval      |                                  更新间隔（秒）。决定计时器更新的频率。设置为0时，数值将在每个关键帧上更新                                  |             number              |    No    | Android/iOS |        Yes        |
|          size           |                                                                             SVG 元素的宽度和高度                                                                             |             number              |    No    | Android/iOS |        Yes        |
|       strokeWidth       |                                                                                      路径笔画宽度                                                                                      |             number              |    No    | Android/iOS |        Yes        |
|    trailStrokeWidth     |                                                                                     轨迹笔触宽度                                                                                      |             number              |    No    | Android/iOS |        Yes        |
|      strokeLinecap      |                                                                                    路径描边线端点                                                                                     |    `round 、 square 、 butt`    |    No    | Android/iOS |        Yes        |
|        rotation         |                                                                              进度条旋转方向                                                                               | `clockwise 、 counterclockwise` |    No    | Android/iOS |        Yes        |
|        isGrowing        |                                                            指示进度条的路径应该是增长而不是缩小                                                            |             boolean             |    No    | Android/iOS |        Yes        |
|       trailColor        |                                                                      圆圈轨迹颜色 - 可以使用任何有效的颜色格式                                                                      |             string              |    No    | Android/iOS |        Yes        |
| isSmoothColorTransition |                                                            指示颜色是否应平滑过渡到下一个颜色                                                            |             boolean             |    No    | Android/iOS |        Yes        |
|        children         |                                                          渲染函数，用于自定义圆心的时间/内容                                                          |            function             |    No    | Android/iOS |        Yes        |
|       onComplete        |                                                                             在动画完成事件处理程序上                                                                             |            function             |    No    | Android/iOS |        Yes        |
|        onUpdate         |                                                                           在剩余时间更新事件处理程序                                                                            |            function             |    No    | Android/iOS |        Yes        |

## 遗留问题

## 其他

- 此库倒计时在完成时是会有重合效果显示，不贴边的效果是设置strokeWidth和strokeLinecap='square'属性的时候会出现，与ios保持一致。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/vydimitrov/react-countdown-circle-timer/blob/master/LICENSE) ，请自由地享受和参与开源。
