> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-htmlview</code> </h1>
</p>

> [!TIP] [GitHub address](https://github.com/jsdf/react-native-htmlview)

请到三方库的 Releases发布地址查看配套的版本信息：

| 三方库版本 | 支持RN版本 |
| ----------| ---------- |
| 0.17.0    |  0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-htmlview@0.17.0
```

#### **yarn**

```bash
yarn add react-native-htmlview@0.17.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import {StyleSheet, View, Linking} from 'react-native';
import HTMLView from 'react-native-htmlview';

const HtmlViewExample = () => {
  const htmlContent = `
      <h1>Hello, World!</h1>
      <p>This is a <a href="https://www.vmall.com">link</a></p>
      <p>Here is an image: <img src="https://res.vmallres.com/pimages/uomcdn/CN/pms/202404/displayProduct/10086102004921/428_428_a_mobileFF345C8650FF6E88771386A6433556D0.jpg" alt="Example Image" /></p>
  `;

  return (
    <View style={{...styles.container,backgroundColor:'white'}} >
      <HTMLView 
        value={htmlContent} 
        stylesheet={styles} // Optional: Pass custom styles for HTML elements
        onLinkPress={(url) => Linking.openURL(url)} // Optional: Handle link presses
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 16,
  },
    // Define custom styles for HTML elements
    a: {
      fontWeight: 'bold',
      color: 'blue',
      fontSize: 20,
      borderColor:'#000000',
      borderWidth:2
    },
    img: {
      width: 200,
      height: 100,
    },
});

export default HtmlViewExample;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Preview2; IDE: DevEco Studio 4.1.3.700; ROM: 3.0.0.19;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

> [!TIP] 该库为UI组件库，可以在该库的标签下，使原本无法在RN框架生效的Html写法，可以实现对应的功能。

| Name            | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| value           | 要渲染的HTML内容字符串                           | string | yes      | All      | yes               |
| onLinkPress     | 当链接被点击时会调用此函数并传入URL。传递此属性将覆盖链接的处理方式 | string | no       | All      | yes               |
| onLinkLongPress | 当链接被长按时会调用此函数并传入URL。默认行为是 | string | no       | All      | yes               |
| stylesheet      | 通过标签名称键控的样式表对象，将覆盖应用于这些相应标签的样式。 | string | no       | All      | yes               |
| renderNode      | 自定义函数，用于按您认为合适的方式渲染HTML节点。  | string | no       | All      | yes               |
| bullet          | 在`ul`内每个`li`元素前渲染的文本        | string | no       | All      | yes               |
| paragraphBreak  | 在每个`p`元素后出现的文本                    | string | no       | All      | yes               |
| lineBreak       | 在创建新行的文本元素后出现的文本 | string | no       | All      | yes               |
| addLineBreaks   | 当明确设置时，有效设置为                           | boolean | no       | All      | yes               |

## 开源协议

本项目基于 [The ISC License (ISC)](https://github.com/jsdf/react-native-htmlview/blob/master/LICENSE) ，请自由地享受和参与开源。
