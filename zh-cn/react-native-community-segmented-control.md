> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-segmented-control/segmented-control</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-segmented-control/segmented-control">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-segmented-control/segmented-control/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/segmented-control)

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.5.2      | [@react-native-oh-tpl/segmented-control Releases](https://github.com/react-native-oh-library/segmented-control/releases) | 0.72       |
| 2.6.0     | [@react-native-ohos/segmented-control Releases]()            | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/segmented-control

# 0.77
npm install @react-native-ohos/segmented-control
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/segmented-control

# 0.77
yarn add @react-native-ohos/segmented-control
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

- 0.72 示例

```js
import React, { useState, useEffect } from "react";
import SegmentedControl from "@react-native-segmented-control/segmented-control";

const CustomValues = ["One", "Two"];

export const MSegmentedControl: React.FC = (): JSX.Element => {

    const [selectedIndex, setSelectedIndex] = useState(0);

    return <SegmentedControl
        values={["One", "Two"]}
        selectedIndex={selectedIndex}
        onChange={(event) => {
            setSelectedIndex(event.nativeEvent.selectedSegmentIndex);
        }}
    />;
}
```

- 0.77 示例

```js
import React, { useState } from "react";
import { View, StyleSheet, Text } from "react-native";
import SegmentedControl from "@react-native-segmented-control/segmented-control";

export const MSegmentedControl: React.FC = (): JSX.Element => {
  const [selectedIndex, setSelectedIndex] = useState(0);
  const testIDS = ['btn-1', 'btn-2'];

  return (
    <View style={styles.container}>
      <SegmentedControl
        values={["One", "Two"]}
        selectedIndex={selectedIndex}
        onChange={(event) => {
          setSelectedIndex(event.nativeEvent.selectedSegmentIndex);
        }}
        testIDS={testIDS}
        style={styles.segmentedControl}
      />
      <Text style={{marginTop: 20}}>
        当前选中 testID: {testIDS[selectedIndex]}
      </Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  segmentedControl: {
    width: "60%", 
    height: 40,
  },
});
```



## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [react-native-community/segmented-control 源库地址](https://github.com/react-native-segmented-control/segmented-control)

| Name                      | Description                                                                                    | Type                                                                                                                                                             | Required | Platform | HarmonyOS Support |
| ------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| enabled         | 如果为false，用户将无法与控件交互。默认值为true。                                                                                                                                                             | boolean         | No       | All          | Yes               |
| momentary       | 如果为true，则选择一个Tab页不会在视觉上保持选中状态。onValueChange回调仍会正常工作。                                                                                                                                | boolean         | No       | iOS          | Yes               |
| onChange        | 当用户点击Tab时调用的回调函数；将事件作为参数传递                                                                                                                                                            | function        | No       | All          | Yes               |
| onValueChange   | 当用户点击Tab时调用的回调函数；将Tab的值作为参数传递                                                                                                                                                  | function        | No       | All          | Yes               |
| selectedIndex   | 要（预先）选择的Tab在props.values中的索引。                                                                                                                                                                                    | number          | No       | All          | Yes               |
| tintColor       | 控件的强调色。                                                                                                                                                                                                                     | string          | No       | All          | Yes               |
| backgroundColor | 控件的背景颜色。                                                                                                                                                                                                           | string          | No       | All          | Yes               |
| values          | 控件Tab按钮的标签，按顺序排列。                                                                                                                                                                                          | string          | Yes      | All          | Yes               |
| appearance      | 覆盖控件外观，不受操作系统主题影响                                                                                                                                                                                  | 'dark', 'light' | No       | All          | Yes               |
| fontStyle       | 对象容器，包含：color: Tab文本颜色；fontSize: Tab文本字体大小；fontFamily: Tab文本字体系列；fontWeight: Tab文本字重                                                                                  | object          | No       | All          | Yes               |
| activeFontStyle | 对象容器，包含：color: 覆盖选中Tab文本颜色；fontSize: 覆盖选中Tab文本字体大小；fontFamily: 覆盖选中Tab文本字体系列；fontWeight: 覆盖选中Tab文本字重 | object          | No       | All          | Yes               |   
| tabStyle        | 设置负责切换选项卡的可点击表面样式                                                                                                                                                                                 | object          | No       | Android, Web | Yes               |
| testIDS<sup>0.77+</sup> | 每个Tab按钮的testID数组 | $ReadOnlyArray<string> | Yes | All | Yes |
| sliderStyle<sup>0.77+</sup> | 滑块组件(Animated.View)的样式属性 | object | No | Android, Web | Yes |

## 遗留问题
- [X] @react-native-segmented-control/segmented-control 的fontFamily属性未实现 HarmonyOS 化: [issue#858](https://github.com/react-native-segmented-control/segmented-control/issues/858)
- [X] @react-native-segmented-control/segmented-control 的momentary属性未实现 HarmonyOS 化: [issue#868](https://github.com/react-native-segmented-control/segmented-control/issues/868)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-segmented-control/segmented-control/blob/master/LICENSE) ，请自由地享受和参与开源。
