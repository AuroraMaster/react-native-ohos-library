> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>text-shadow-component</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/bswnth48/text-shadow-react-native">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bswnth48/text-shadow-react-native/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/bswnth48/text-shadow-react-native)

> [!TIP] 仅在 RNOH 0.77+ 呈现阴影效果，不支持 RNOH 0.72。

## 安装与使用
<!-- tabs:start -->
进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install --save text-shadow-component@1.0.7
```

#### **yarn**

```bash
yarn add text-shadow-component@1.0.7
```

<!-- tabs:end -->

下面的代码展示了该库的基本使用场景：

```js
import React from 'react';
import { View, ScrollView } from 'react-native';
import { TextShadow } from 'text-shadow-component';

export default function App() {
  const cases = [
    {
      bg: '#232323',
      color: '#FFFFFF',
      textShadow: '0 0 5px #FFF, 0 0 12px #49FF18',
    },
    {
      bg: '#FFFFFF',
      color: '#202c2d',
      textShadow:
        '0 1px #808d93, -1px 0 #cdd2d5, -1px 2px #808d93, -2px 1px #cdd2d5',
    },
  ];

  return (
    <ScrollView>
      {cases.map((it, idx) => (
        <View
          key={idx}
          style={{
            height: 200,
            alignItems: 'center',
            justifyContent: 'center',
            backgroundColor: it.bg,
          }}
        >
          <TextShadow
            title="Preview"
            textShadow={it.textShadow}
            titleStyle={{ fontSize: 48, color: it.color }}
          />
        </View>
      ))}
    </ScrollView>
  );
}
```

## 约束与限制

### 兼容性

本文档内容基于以下环境验证通过：

1. RNOH: 0.77.18; SDK：HarmonyOS 5.0.0 Release(API Version 12 Release); IDE：DevEco Studio 5.1.1.830; ROM：5.0.0.150 SP8

> 说明：在 RNOH 0.77+ 上，原生已实现文本阴影绘制。早期版本（如：RNHO 0.72版本）不会呈现阴影效果。

## 属性
> [!TIP] "Platform" 列表示源库标注的平台；

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

> [!TIP] 本文档仅就 HarmonyOS（RNOH 0.77）给出支持结论。

| Name         | Description                                   | Type   | Required | Platform    | HarmonyOS Support |
|--------------|-----------------------------------------------|--------|----------|-------------|-------------------|
| title        | 要显示的文本内容                               | string | yes      | Android/iOS | yes               |
| textShadow   | CSS 风格的 text-shadow 字符串（支持多层）     | string | yes      | Android/iOS | yes               |
| titleStyle   | 文本样式（如 fontSize、color 等）             | style  | no       | Android/iOS | yes               |


## 遗留问题
在 RNOH 0.72 上不显示阴影效果。[issue#ID0FUU](https://gitee.com/react-native-oh-library/usage-docs/issues/ID0FUU)
## 其他


## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/bswnth48/text-shadow-react-native/blob/master/LICENSE) ，请自由地享受和参与开源。
