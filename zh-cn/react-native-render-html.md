
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-render-html</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/meliorence/react-native-render-html">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/meliorence/react-native-render-html/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-BSD-blue.svg" alt="License" />
    </a>
</p>

> [!Tip] [Github 地址](https://github.com/meliorence/react-native-render-html)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本   | 发布信息                                                     | 支持RN版本 |
| ------------ | ------------------------------------------------------------ | ---------- |
| 6.3.4        | [react-native-render-html](https://github.com/meliorence/react-native-render-html/releases)   | 0.72/0.77       |

进入到工程目录并输入以下命令：



<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-render-html@6.3.4
```

#### **yarn**

```bash
yarn add react-native-render-html@6.3.4
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { useWindowDimensions } from "react-native";
import RenderHtml from "react-native-render-html";

const source = {
  html: `
<p style='text-align:center;'>
  Hello World!
</p>`,
};

export default function App() {
  const { width } = useWindowDimensions();
  return <RenderHtml contentWidth={width} source={source} />;
}
```


## 约束与限制

### 兼容性
本文档内容基于以下版本验证通过：

1. RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE：DevEco Studio 5.0.3.403; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH：0.77.18; SDK：HarmonyOS 5.1.1 Release; IDE: DevEco Studio 5.1.1.830; ROM：NEXT 5.1.0.150; 


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**组件 RenderHtml**

| Name                                   | Description                                                                                                                                                                                                       | Type                                               | Required | Platform      | HarmonyOS Support |
|----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------|----------|---------------|-------------------|
| allowedStyles                          | 将特定的内联CSS样式属性列入白名单，并忽略其他属性。                                                                                                                                             | CSSPropertyNameList                                | NO       | Android、iOS   | Yes               |
| baseStyle                              | 文档的默认样式（根）。可继承的样式将传递给子对象。这也适用于文本风格。                                                                               | MixedStyleDeclaration                              | NO       | Android、iOS   | Yes               |
| classesStyles                          | 为CSS类选择的目标元素提供混合样式。                                                                                                                                                 | Readonly<Record<string, MixedStyleDeclaration>>    | NO       | Android、iOS   | Yes               |
| computeEmbeddedMaxWidth                | 一个函数，它接受contentWidth和tagName作为参数，并返回一个新的宽度。可以返回Infinity来表示不受约束的宽度。                                                                         | (contentWidth: number, tagName: string) => number  | NO       | Android、iOS   | Yes               |
| contentWidth                           | 要显示的HTML内容的宽度。建议的做法是传递useWindowDimensions（）.width减去任何填充或边距。                                                                           | number                                             | NO       | Android、iOS   | Yes               |
| customHTMLElementModels                | 为目标标记自定义元素模型。                                                                                                                                                                         | HTMLElementModelRecord                             | NO       | Android、iOS   | Yes               |
| dangerouslyDisableHoisting             | 禁止起吊。特别适用于使用react native web进行渲染。请注意，您的布局可能会在本地中断！                                                                                             | boolean                                            | NO       | Android、iOS   | Yes               |
| dangerouslyDisableWhitespaceCollapsing | 禁用空白折叠。如果您的html正在使用minifier在服务器端进行预处理，则特别有用。                                                                                                 | boolean                                            | NO       | Android、iOS   | Yes               |
| debug                                  | 在每次瞬态渲染树失效后，将渲染的TDocument的快照记录到控制台。                                                                                                            | boolean                                            | NO       | Android、iOS   | Yes               |
| defaultTextProps                       | 渲染树中文本元素的默认道具。                                                                                                                                                               | TextProps                                          | NO       | Android、iOS   | Yes               |
| defaultViewProps                       | 渲染树中View元素的默认道具。                                                                                                                                                               | ViewProps                                          | NO       | Android、iOS   | Yes               |
| domVisitors                            | 当解析DOM元素或文本节点并附加其子节点时，将调用回调的对象。这对于篡改dom、删除子节点、插入节点、更改文本节点数据非常有用。……等等。 | DomVisitorCallbacks                                | NO       | Android、iOS   | Yes               |
| emSize                                 | 1em的默认像素值。                                                                                                                                                                              | number                                             | NO       | Android、iOS   | Yes               |
| enableCSSInlineProcessing              | 启用或禁用内联样式的内联CSS处理。                                                                                                                                                         | boolean                                            | NO       | Android、iOS   | Yes               |
| enableExperimentalBRCollapsing         | 建议值在非网络平台上为“true”。另请注意，这是一个实验性特征，因此会受到行为不稳定的影响。                                                                         | boolean                                            | NO       | Android、iOS   | Yes               |
| enableExperimentalMarginCollapsing     | 启用或禁用边距折叠CSS行为（实验！）。                                                                                                                                                 | boolean                                            | NO       | Android、iOS   | Yes               |
| idsStyles                              | 启用或禁用边距折叠CSS行为（实验！）。                                                                                                                                                 | boolean                                            | NO       | Android、iOS   | Yes               |
| ignoreDomNode                          | 忽略特定的DOM节点。                                                                                                                                                                                        | (node: Node, parent: NodeWithChildren) => unknown  | NO       | Android、iOS   | Yes               |
| ignoredDomTags                         | DOM中不应包含的小写标签列表。                                                                                                                                                 | Array<string>                                      | NO       | Android、iOS   | Yes               |
| ignoredStyles                          | 将特定的内联CSS样式属性列入黑名单，并允许其他属性。                                                                                                                                             | CSSPropertyNameList                                | NO       | Android、iOS   | Yes               |
| bypassAnonymousTPhrasingNodes          | 最简单的一个是它简化了渲染树                                                                                                                                                          | boolean                                            | NO       | Android、iOS   | Yes               |
| onDocumentMetadataLoaded               | 当文档元数据可用时调用处理程序。它将在HTML内容更改时重新触发。                                                                                                              | (documentMetadata: DocumentMetadata) => void       | NO       | Android、iOS   | Yes               |
| onHTMLLoaded                           | 当HTML可用于RenderHTML组件时触发。                                                                                                                                                     | (html: string) => void                             | NO       | Android、iOS   | Yes               |
| onTTreeChange                          | 当瞬态渲染树发生变化时触发。可用于调试。                                                                                                                                           | (ttree: TDocument) => void                         | NO       | Android、iOS   | Yes               |
| renderers                              | 您的自定义渲染器。                                                                                                                                                                                            | CustomTagRendererRecor                             | NO       | Android、iOS   | Yes               |
| selectDomRoot                          | 在生成TTree之前选择DOM根。例如，您可以迭代子元素，直到到达article元素并返回此元素。                                                             | TRenderEngineOptions                               | NO       | Android、iOS   | Yes               |
| setMarkersForTNode                     | 从TNode及其所有子体设置自定义标记。标记将在自定义渲染器中通过`tnode.markets`道具访问。                                                                                | SetMarkersForTNode                                 | NO       | Android、iOS   | Yes               |
| source                                 | 要呈现的对象源（｛uri｝、｛html｝或｛dom｝）。                                                                                                                                                | HTMLSource                                         | Yes      | Android、iOS   | Yes               |
| renderersProps                         | 使用useRenderProps在自定义渲染器中使用的道具。                                                                                                                                                           | Partial<RenderersProps>                            | NO       | Android、iOS   | Yes               |
| systemFonts                            | 当前平台中可用的字体列表。这些字体将用于选择CSS“fontFamily”属性中的第一个匹配项，该属性支持逗号分隔的字体列表。默认情况下，每个平台都会选择几种字体。 | Array<string>                                      | No       | Android、iOS   | Yes               |
| tagsStyles                             | 为目标HTML标记名提供混合样式。                                                                                                                                                                    | Readonly<Record<string, MixedStyleDeclaration>>    | NO       | Android、iOS   | Yes               |

## 遗留问题

## 其他
-  img 的宽度不会随着 contentWidth 的动态修改而更改,接口属性原库本身不支持（与iOS/Android表现一致）（由 RN 基座引起，RNImage 组件更新状态时 this.descriptorWrapper 没有重新赋值） [issue#638](https://github.com/meliorence/react-native-render-html/issues/638)
## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/meliorence/react-native-render-html/blob/master/LICENSE) ，请自由地享受和参与开源。
