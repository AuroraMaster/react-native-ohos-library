> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-autolink</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/joshswan/react-native-autolink">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/joshswan/react-native-autolink/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/joshswan/react-native-autolink)

## 安装与使用

| 三方库版本  |  支持RN版本 |
| ---------- | ---------- |
| 4.2.0      | 0.72/0.77      |

#### **npm**

```bash
npm install react-native-autolink@4.2.0
```

#### **yarn**

```bash
yarn add react-native-autolink@4.2.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';
import Autolink from 'react-native-autolink';

const AutolinkDemo = () => {
    return (
        <View style={styles.container}>
            <Text style={styles.text}>
                Here is a demo of react-native-autolink:
            </Text>
            <Autolink
                text="This is the string to parse for urls (https://github.com/joshswan/react-native-autolink), phone numbers (415-555-5555), emails (josh@example.com), mentions/handles (@twitter), and hashtags (#exciting)"
                email
                hashtag="instagram"
                mention="twitter"
                phone="sms"
                url
            />
        </View>
    )
};

const styles = StyleSheet.create({
    container: {
        flex: 1,
        padding: 20,
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: '#f0f0f0',
    },
    text: {
        fontSize: 18,
        marginBottom: 10,
    },
    autolink: {
        fontSize: 16,
        lineHeight: 24,
    },
    link: {
        color: 'blue',
        textDecorationLine: 'underline',
    },
    customLink: {
        color: 'red',
        textDecorationLine: 'underline',
    },
    customText: {
        color: 'red',
    }
});

export default AutolinkDemo;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.29;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 Yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|        Name        |                         Description                          |        Type         | Required |  Platform   | HarmonyOS Support |
| :----------------: | :----------------------------------------------------------: | :-----------------: | :------: | :---------: | :---------------: |
|     component      |     覆盖用作输出容器的组件。     | React.ComponentType |    No    | Android/IOS |        Yes        |
|       email        |          是否链接电子邮件（mailto:{email}）。          |       boolean       |    No    | Android/IOS |        Yes        |
|      hashtag       | 是否将标签链接至提供的服务。可能值：false（禁用）、"facebook"、"instagram"、"twitter"。 |  boolean or string  |    No    | Android/IOS |        Yes        |
|     linkProps      |         应用于链接文本组件的属性。          |      TextProps      |    No    | Android/IOS |        Yes        |
|     linkStyle      | 应用于链接文本组件的样式。注：如果提供的样式为 [`linkProps`](https://github.com/joshswan/react-native-autolink#linkprops). |      TextStyle      |    No    | Android/IOS |        Yes        |
|      matchers      | 自定义匹配器对象数组，具有可选的新闻处理程序、样式和文本/url提取。 |   CustomMatcher[]   |    No    | Android/IOS |        Yes        |
|      mention       | 是否将提及/处理链接到提供的服务。可能的值：false（禁用）、“instagram”、“soundcloud”、“twitter”。 |  boolean or string  |    No    | Android/IOS |        Yes        |
|      onPress       | 覆盖默认链接按压行为。签名：（url:string，match:match）=>无效。 |      function       |    No    | Android/IOS |        Yes        |
|    onLongPress     | 处理链接长按事件。签名：（url:string，match:match）=>void。 |      function       |    No    | Android/IOS |        Yes        |
|       phone        | 是否链接电话号码。可能的值: `false` (disabled), `true` (`tel:{number}`), `"sms"` or `"text"` (`sms:{number}`). |  boolean or string  |    No    | Android/IOS |        Yes        |
|     renderLink     | 覆盖默认链接渲染行为。签名: `(text: string, match: Match, index: number) => React.ReactNode`. |      function       |    No    | Android/IOS |        Yes        |
|     renderText     | 覆盖默认文本呈现行为。签名: `(text: string, index: number) => React.ReactNode`. |      function       |    No    | Android/IOS |        Yes        |
|     showAlert      | 是否在离开应用程序之前显示警报（出于隐私或意外点击）。 |       boolean       |    No    | Android/IOS |        Yes        |
|    stripPrefix     | 是否从URL链接文本中删除协议 (e.g. `https://github.com` -> `github.com`). |       boolean       |    No    | Android/IOS |        Yes        |
| stripTrailingSlash | 是否从URL链接文本中删除尾随斜线 (e.g. `github.com/` -> `github.com`). |       boolean       |    No    | Android/IOS |        Yes        |
|        text        |                要解析链接的字符串。                |       string        |   Yes    | Android/IOS |        Yes        |
|     textProps      |      应用于非链接文本组件的属性。        |      TextProps      |    No    | Android/IOS |        Yes        |
|      truncate      | URL链接文本的最大长度。可能的值：0（禁用），1+（最大长度）。 |       number        |    No    | Android/IOS |        Yes        |
|   truncateChars    | 用字符替换截断的URL链接文本段 (e.g. `github.com/../repo`) |       string        |    No    | Android/IOS |        Yes        |
|  truncateLocation  | 覆盖截断位置。可能值： `"smart"`, `"end"`, `"middle"`. |       string        |    No    | Android/IOS |        Yes        |
|        url         | 是否链接URL。可能的值：false（禁用）、true、UrlConfig（见下文）。 |  boolean or object  |    No    | Android/IOS |        Yes        |
|  useNativeSchemes  | 在链接到标签和提及链接的服务时，是否使用本地应用程序方案（例如twitter://）而不是web URL。 |       boolean       |    No    | Android/IOS |        Yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License](https://github.com/joshswan/react-native-autolink/blob/master/LICENSE) ，请自由地享受和参与开源。
