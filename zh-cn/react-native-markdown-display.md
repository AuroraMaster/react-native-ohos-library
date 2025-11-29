> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-markdown-display</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-markdown-display">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20macos%20|%20web%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/iamacup/react-native-markdown-display/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-markdown-display/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-markdown-display Releases](https://github.com/react-native-oh-library/react-native-markdown-display/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

| version | Package Name                                       |Repository | Release               |  RN version |
| ---------- | ------------------------------------------------------------ | -------|--------|---------- |
| 7.0.1     | @react-native-oh-tpl/react-native-markdown-display | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-markdown-display)  | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-markdown-display/releases)|0.72       |
| 7.1.0    | @react-native-ohos/react-native-markdown-display  |[Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-markdown-display)  | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-markdown-display/releases)| 0.77       |

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
#0.72
npm install @react-native-oh-tpl/react-native-markdown-display

#0.77
npm install @react-native-ohos/react-native-markdown-display
```

#### **yarn**

```bash
#0.72
yarn add @react-native-oh-tpl/react-native-markdown-display

#0.77
yarn add @react-native-ohos/react-native-markdown-display
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { SafeAreaView, ScrollView, StatusBar } from 'react-native';

import Markdown from 'react-native-markdown-display';

const copy = `# h1 Heading 8-)

**This is some bold text!**

This is normal text
`;

const App: () => React$Node = () => {
  return (
    <>
      <StatusBar barStyle="dark-content" />
      <SafeAreaView>
        <ScrollView
          contentInsetAdjustmentBehavior="automatic"
          style={{height: '100%'}}
        >
          <Markdown>
            {copy}
          </Markdown>
        </ScrollView>
      </SafeAreaView>
    </>
  );
};

export default App;
```

## 约束与限制

### 兼容性

在以下版本验证通过

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：204.1.0.59;
2. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请查看[react-native-markdown-display](https://github.com/iamacup/react-native-markdown-display/blob/master/README.md)

如下是已经 HarmonyOS 化的属性：

> [!TIP] " HarmonyOS 支持"列为 yes 的属性表示支持 HarmonyOS 平台，并且效果对标"原库平台"列中的 ios 或 android 的效果。

| Name                      | Description                                                                                                                                                                                           | Default                                                                                                                    | Required | Platform | HarmonyOS Support |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| `children`                | 要渲染的 Markdown 字符串，或 [pre-processed tree](https://github.com/react-native-oh-library/react-native-markdown-display/tree/sig#pre-processing)                                          | N/A                                                                                                                        | Yes      | All      | yes               |
| `style`                   | 用于覆盖各类规则样式的配置对象，如需更多信息，请点击 [see style section below](https://github.com/react-native-oh-library/react-native-markdown-display/tree/sig#rules-and-styles)   | [source](https://github.com/react-native-oh-library/react-native-markdown-display/blob/7.0.2-0.0.1/src/lib/styles.js)      | No       | All      | yes               |
| `mergeStyle`              | 若此项为 true，当传入样式参数时，各独立样式项将与默认样式进行合并而非完全覆盖 them                                                                                | `true`                                                                                                                     | No       | All      | yes               |
| `rules`                   | 用于定义各 Markdown 元素渲染规则的配置对象，如需更多信息，请看 [see rules section below](https://github.com/react-native-oh-library/react-native-markdown-display/tree/sig#rules)    | [source](https://github.com/react-native-oh-library/react-native-markdown-display/blob/7.0.2-0.0.1/src/lib/renderRules.js) | No       | All      | yes               |
| `onLinkPress`             |用于改变点击行为的处理函数，如需更多信息，请看 [see handling links section below](https://github.com/react-native-oh-library/react-native-markdown-display/tree/sig#handling-links)       | `import { Linking } from 'react-native';` and `Linking.openURL(url);`                                                      | No       | All      | yes               |
| `debugPrintTree`          | 该功能将在控制台输出 AST 语法树，帮助您查看 Markdown 文档的转换结果。to                                                                                                       | `false`                                                                                                                    | No       | All      | yes               |
| `renderer`                | 当使用自定义渲染器时，将无法同时启用 rules 或 styles 属性配置 。                                                                                                | `instanceOf(AstRenderer)`                                                                                                  | No       | All      | yes               |
| `markdownit`              | 可传入自定义配置的 markdownit 实例，默认值为 MarkdownIt({typographer: true})。`                                                                                                    | `instanceOf(MarkdownIt)`                                                                                                   | No       | All      | yes               |
| `maxTopLevelChildren`     | 若设置为数值，则仅渲染前 n 个顶层子元素，随后将尝试渲染 topLevelMaxExceededItem 组件。`topLevelMaxExceededItem`                                                                  | `null`                                                                                                                     | No       | All      | yes               |
| `topLevelMaxExceededItem` | 当达到 maxTopLevelChildren 限制时将渲染此组件，请务必为其设置 key 属性！                                                                                                                          | `<Text key="dotdotdot">...</Text>`                                                                                         | No       | All      | yes               |
| `allowedImageHandlers`    | 对于未以指定前缀开头的图片链接，系统将自动前置 defaultImageHandler 值（若该值为 null 则放弃渲染）。        | `['data:image/png;base64', 'data:image/gif;base64', 'data:image/jpeg;base64', 'https://', 'http://']`                      | No       | All      | yes               |
| `defaultImageHandler`     | 若图片 URL 未以 allowedImageHandlers 数组中的前缀开头，系统将自动前置此默认值；若该值设为 null，则不会尝试修复而直接放弃渲染。 | `http://`                                                                                                                  | No       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/iamacup/react-native-markdown-display/blob/master/LICENSE) ，请自由地享受和参与开源。
