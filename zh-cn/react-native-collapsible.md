> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-collapsible</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/oblador/react-native-collapsible">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/oblador/react-native-collapsible/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/oblador/react-native-collapsible/tree/v1.6.1)

## 安装与使用

| 三方库版本 | 支持RN版本 |
| ---------- | ---------- |
| 1.6.1      | 0.72       |
| 1.6.2      | 0.77       |

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install react-native-collapsible@1.6.1

# 0.77
npm install react-native-collapsible@1.6.2
```

#### **yarn**

```bash
# 0.72
yarn add react-native-collapsible@1.6.1

# 0.77
yarn add react-native-collapsible@1.6.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, { useState } from 'react';
import { ScrollView, StyleSheet, Text, View, TouchableOpacity,Button } from 'react-native';
import Collapsible from 'react-native-collapsible';
import Accordion from 'react-native-collapsible/Accordion';
export function CollapsibleExample() {
    const [activeSections, setActiveSections] = useState([0]);
    const [isCollapsed, setIsCollapsed] = useState(true);
    function renderHeader(section: any, _: any, isActive: any) {
        return (<Text>{section.title}</Text>);
    };
    function renderContent(section: any, _: any, isActive: any) {
        return (<Text>{section.content}</Text> );
    }
    return(
        <ScrollView>
         <Accordion
            activeSections={activeSections}
            sections={CONTENT}
            touchableComponent={TouchableOpacity}
            renderHeader={renderHeader}
            renderContent={renderContent}
            duration={400}
            onChange={setActiveSections}
            renderAsFlatList={false}
        />
        <Button title = "open" onPress = {() =>{ setIsCollapsed(!isCollapsed) } } />
            <Collapsible 
                collapsed={isCollapsed}
                onAnimationEnd = { ()=>{ console.log("log:动画结束") } }
                duration = { 100 }
                collapsedHeight = { 0 } >
                <Button title = "aaaaa" />
                <Button title = "bbbbb" />
            </Collapsible>
        </ScrollView>
    );
}
const CONTENT = [
    { title: 'First', feet: '1', content: "a", },
    { title: 'Second', feet: '2', content: "b", },
    { title: 'Third', feet: '3', content: "c", },
];
```


## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
#### Collapsible
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`align`** | 过渡时内容的对齐方式，可以是 `top`、`center` 或 `bottom`。 | enum | no | All | yes |
| **`collapsed`** | 是否显示子组件。 | boolean | no | All | yes |
| **`collapsedHeight`** | 组件折叠后的高度。 | number | no | All | yes |
| **`enablePointerEvents`** | 在折叠视图上启用指针事件。 | boolean | no | All | yes |
| **`duration`** | 过渡持续时间（以毫秒为单位）。 | number | no | All | yes |
| **`easing`** | 来自 [`Easing`](https://github.com/facebook/react-native/blob/master/Libraries/Animated/src/Easing.js) 的函数或函数名（如果 RN < 0.8，则是 [`tween-functions`](https://github.com/chenglou/tween-functions)）。如果你使用类似 `tween-functions` 的命名方式，Collapsible 会尝试为你组合 `Easing` 函数。 | string \| function | no | All | yes |
| **`renderChildrenCollapsed`** | 即使不可见，也在折叠组件中渲染子元素。 | boolean | no | All | yes |
| **`style`** | 容器的可选样式。 | object | no | All | yes |
| **`onAnimationEnd`** | 切换动画结束时的回调。用于避免在动画期间进行繁重的布局工作。 | function | no | All | yes |

#### Accordion 
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`sections`** | 传递给渲染方法的 sections 数组。 | array | no | All | yes |
| **`renderHeader(content, index, isActive, sections)`** | 一个函数，应返回表示标题的可渲染内容。 | function | no | All | yes |
| **`renderContent(content, index, isActive, sections)`** | 一个函数，应返回表示内容的可渲染内容。 | function | no | All | yes |
| **`renderFooter(content, index, isActive, sections)`** | 一个函数，应返回表示页脚的可渲染内容。 | function | no | All | yes |
| **`renderSectionTitle(content, index, isActive)`** | 一个函数，应返回表示可触摸元素外部 section 标题的可渲染内容。 | function | no | All | yes |
| **`onChange(indexes)`** | 当当前激活的 section 更新时调用的函数。 | function | no | All | yes |
| **`keyExtractor(item, index)`** | 用于提取指定索引处给定项的唯一键。 | function | no | All | yes |
| **`activeSections`** | 控制 `sections` 数组中哪些索引当前处于展开状态。如果为空，则关闭所有 section。 | array | no | All | yes |
| **`underlayColor`** | 点击标题时显示的底层颜色。默认为黑色。 | string | no | All | yes |
| **`touchableComponent`** | Accordion 中使用的可触摸组件。默认为 `TouchableHighlight`。 | object | no | All | yes |
| **`touchableProps`** | `touchableComponent` 的属性。 | object | no | All | yes |
| **`disabled`** | 设置用户是否可以与 Accordion 交互。 | boolean | no | All | yes |
| **`align`** | 见 `Collapsible`。 | enum | no | All | yes |
| **`duration`** | 见 `Collapsible`。 | number | no | All | yes |
| **`easing`** | 见 `Collapsible`。 | string \| function | no | All | yes |
| **`onAnimationEnd(key, index)`** | 见 `Collapsible`。 | function | no | All | yes |
| **`expandFromBottom`** | 从底部而不是顶部展开内容。 | boolean | no | All | yes |
| **`expandMultiple`** | 允许展开多个 section。默认为 false。 | boolean | no | All | yes |
| **`sectionContainerStyle`** | section 容器的可选样式。 | object | no | All | yes |
| **`containerStyle`** | Accordion 容器的可选样式。 | object | no | All | yes |
| **`renderAsFlatList`** | 可选作为 FlatList 渲染（默认为 false）。 | boolean | no | All | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/oblador/react-native-collapsible/blob/master/LICENSE) ，请自由地享受和参与开源。