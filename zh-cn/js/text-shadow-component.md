> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>text-shadow-component</code> </h1>
</p>

请到三方库的 Releases 发布地址查看配套的版本信息：[text-shadow-component Releases](https://github.com/bswnth48/text-shadow-react-native/releases)。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

| 三方库版本 |  支持RN版本 | 
| ---------- |---------- |
| 1.0.7 | 0.72/0.77 |

> [!TIP] 从 RNOH 0.72.97 版本开始，RNOH 0.72 支持阴影效果渲染。

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

1. RNOH: 0.77.18; SDK: HarmonyOS 5.0.0 Release(API Version 12 Release); IDE: DevEco Studio 5.1.1.830; ROM: 5.0.0.150 SP8;
2. RNOH: 0.72.97; SDK: HarmonyOS 6.0.0.47 (API Version 20 Release); IDE: DevEco Studio 6.0.0 Release; ROM: 6.0.0.108 SP6;

## 属性
> [!TIP] "Platform" 列表示源库标注的平台；

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name         | Description                                   | Type   | Required | Platform    | HarmonyOS Support |
|--------------|-----------------------------------------------|--------|----------|-------------|-------------------|
| title        | 要显示的文本内容                               | string | yes      | Android/iOS | yes               |
| textShadow   | CSS 风格的 text-shadow 字符串（支持多层）     | string | yes      | Android/iOS | yes               |
| titleStyle   | 文本样式（如 fontSize、color 等）             | style  | no       | Android/iOS | yes               |


## 遗留问题

## 其他

从 RNOH 0.72.97 版本开始，RNOH 0.72 支持阴影效果渲染。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/bswnth48/text-shadow-react-native/blob/master/LICENSE) ，请自由地享受和参与开源。
