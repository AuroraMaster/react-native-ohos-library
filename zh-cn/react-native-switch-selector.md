> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-switch-selector</code> </h1>
</p>

> [!TIP] [GitHub address](https://github.com/App2Sales/react-native-switch-selector)

请到三方库的 Releases发布地址查看配套的版本信息：

| 三方库版本 | 支持RN版本 |
| ----------| ---------- |
| 2.3.0    |  0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-switch-selector@2.3.0
```

#### **yarn**

```bash
yarn add react-native-switch-selector@2.3.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import SwitchSelector from "react-native-switch-selector";
import React from 'react';
import { ScrollView } from 'react-native';

const SwitchSelectorDemo = () => {
    const options = [
        { label: "电影", value: "movie" },
        { label: "地图", value: "map" },
        { label: "地铁", value: "metro" }
    ];
    return (
        <ScrollView>
            <SwitchSelector
                options={options}
                initial={0}
            />
        </ScrollView>
    )
}

export default SwitchSelectorDemo;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                         | Description                                                  | Type                     | Required | Platform    | HarmonyOS Support |
| ---------------------------- | ------------------------------------------------------------ | ------------------------ | -------- | ----------- | ----------------- |
| options                      | 要渲染的项目数组。每个项目都有标签和值，以及可选的图标 | array                    | Yes      | Android/IOS | Yes               |
| options[].label              | 每个项目的标签                                        | string                   | Yes      | Android/IOS | Yes               |
| options[].value              | 每个项目的值                                        | string                   | Yes      | Android/IOS | Yes               |
| options[].customIcon         | 每个项目的可选自定义图标                         | Jsx  element ou Function | No       | Android/IOS | Yes               |
| options[].imageIcon          | 每个项目图像图标的来源。在渲染时与标签具有相同的颜色 | string                   | No       | Android/IOS | Yes               |
| options[].activeColor        | 选中时每个项目的颜色                       | string                   | No       | Android/IOS | Yes               |
| options[].testID             | 用于测试的每个项目的测试ID（例如与Appium一起使用）    | string                   | No       | Android/IOS | Yes               |
| options[].accessibilityLabel | 用于测试的每个项目的可访问性标签（例如与Appium一起使用） | string                   | No       | Android/IOS | Yes               |
| initial                      | 初始渲染时选中的项目                             | number                   | No       | Android/IOS | Yes               |
| value                        | 开关的值（将调用onPress）                        | number                   | No       | Android/IOS | Yes               |
| onPress                      | 更改值后调用的回调函数                | function                 | Yes      | Android/IOS | Yes               |
| disableValueChangeOnPress    | 当值手动更改时禁用onPress调用 | bool                     | No       | Android/IOS | Yes               |
| fontSize                     | 标签的字体大小。如果为null，则使用应用程序的默认字体大小 | number                   | No       | Android/IOS | Yes               |
| selectedColor                | 选中项目的文字颜色                             | string                   | No       | Android/IOS | Yes               |
| buttonMargin                 | 选中项目到组件的边距                    | number                   | No       | Android/IOS | Yes               |
| buttonColor                  | 选中项目的背景颜色                               | string                   | No       | Android/IOS | Yes               |
| textColor                    | 未选中项目的文字颜色                       | string                   | No       | Android/IOS | Yes               |
| backgroundColor              | 组件的背景颜色                                   | string                   | No       | Android/IOS | Yes               |
| borderColor                  | 组件的边框颜色                               | string                   | No       | Android/IOS | Yes               |
| borderRadius                 | 组件的边框半径                              | number                   | No       | Android/IOS | Yes               |
| hasPadding                   | 指示项目是否有内边距                                | bool                     | No       | Android/IOS | Yes               |
| animationDuration            | 动画的持续时间                                   | number                   | No       | Android/IOS | Yes               |
| valuePadding                 | 内边距的大小                                             | number                   | No       | Android/IOS | Yes               |
| height                       | 组件的高度                                         | number                   | No       | Android/IOS | Yes               |
| bold                         | 指示文本是否具有fontWeight bold                        | bool                     | No       | Android/IOS | Yes               |
| textStyle                    | 文本样式                                                  | object                   | No       | Android/IOS | Yes               |
| selectedTextStyle            | 选中文本样式                                         | object                   | No       | Android/IOS | Yes               |
| textContainerStyle           | 文本（和图标）容器的样式（TouchableOpacity）      | object                   | No       | Android/IOS | Yes               |
| selectedTextContainerStyle   | 选中文本（和图标）容器的样式（TouchableOpacity） | object                   | No       | Android/IOS | Yes               |
| imageStyle                   | 图像样式                                                 | object                   | No       | Android/IOS | Yes               |
| style                        | 容器样式                                             | object                   | No       | Android/IOS | Yes               |
| returnObject                 | 指示onPress函数是否返回选项而不是option.value | bool                     | No       | Android/IOS | Yes               |
| disabled                     | 禁用开关                                         | bool                     | No       | Android/IOS | Yes               |
| borderWidth                  | 定义边框宽度                                         | number                   | No       | Android/IOS | Yes               |
| testID                       | 用于测试的测试ID（例如与Appium一起使用）                  | string                   | No       | Android/IOS | Yes               |
| accessibilityLabel           | 用于测试的可访问性标签（例如与Appium一起使用）      | string                   | No       | Android/IOS | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/App2Sales/react-native-switch-selector/blob/master/LICENSE)，请自由地享受和参与开源。