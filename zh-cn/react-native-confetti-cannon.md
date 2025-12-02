> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-confetti-cannon</code> </h1>
</p>

> [!TIP] [ GitHub address](https://github.com/VincentCATILLON/react-native-confetti-cannon)

请到三方库的 Releases发布地址查看配套的版本信息：

| 三方库版本 | 支持RN版本 |
| ----------| ---------- |
| 1.5.2     |  0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-confetti-cannon@1.5.2
```

#### **yarn**

```bash
yarn add react-native-confetti-cannon@1.5.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

#### Using a Component

```js
import * as React from 'react';
import { StyleSheet, View, Text } from 'react-native';
import ConfettiCannon from 'react-native-confetti-cannon';

export default function ConfettiCannonExample() {

  return (
    <View style={{width: '100%', height: '100%'}}>
      <ConfettiCannon
        count={50}
        origin={{x: -10, y: -10}}
      />
    </View>
  )
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; OH SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio: 5.0.3.400; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| count  | 要显示的项目数量        | number  |    yes    |  iOS,Android,Web  |         yes        |
| origin  | 动画位置起始点       | {x: number, y: number}  |    yes    |  iOS,Android,Web  |         yes        |
| explosionSpeed  | 从起始点到顶部的爆炸持续时间（毫秒）        | number  |    no    |  iOS,Android,Web  |         yes        |
| fallSpeed  | 从顶部到底部的下降持续时间（毫秒）        | number  |    no    |  iOS,Android,Web  |         yes        |
| fadeOut  | 使彩纸在结束时消失        | boolean  |    no    |  iOS,Android,Web  |         yes        |
| colors  | 为彩纸提供自定义颜色        | string[]  |    no    |  iOS,Android,Web  |         yes        |
| autoStart  | 自动开始动画        | boolean  |    no    |  iOS,Android,Web  |         yes        |
| autoStartDelay  | 触发动画前等待的延迟时间        | number  |    no    |  iOS,Android,Web  |         yes        |


## 事件

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  onAnimationStart  |    动画开始时触发的回调函数	    | Function  |    no    |  iOS,Android,Web  |         yes        |
|  onAnimationResume  |    动画恢复时触发的回调函数	    | Function  |    no    |  iOS,Android,Web  |         yes        |
|  onAnimationStop  |    动画停止时触发的回调函数	    | Function  |    no    |  iOS,Android,Web  |         yes        |
|  onAnimationEnd  |    动画结束时触发的回调函数	    | Function  |    no    |  iOS,Android,Web  |         yes        |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  start  |    以编程方式启动动画	    | Function  |    no    |  iOS,Android,Web  |         yes        |
|  resume  |    以编程方式恢复动画	    | Function  |    no    |  iOS,Android,Web  |         yes        |
|  stop  |    以编程方式停止动画	    | Function  |    no    |  iOS,Android,Web  |         yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/VincentCATILLON/react-native-confetti-cannon/blob/master/LICENSE) ，请自由地享受和参与开源。
