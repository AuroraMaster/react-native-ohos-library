> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-recaptcha-that-works</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/douglasjunior/react-native-recaptcha-that-works">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/douglasjunior/react-native-recaptcha-that-works/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/douglasjunior/react-native-recaptcha-that-works)

| 三方库版本 | 支持RN版本 |
|-------|---------- |
| 2.0.0 | 0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-recaptcha-that-works@2.0.0
```

#### **yarn**

```bash
yarn add react-native-recaptcha-that-works@2.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, {useRef, useCallback, useState} from 'react';
import {
  SafeAreaView,
  StyleSheet,
  View,
  Text,
  StatusBar,
  Button,
  Alert,
} from 'react-native';

import Recaptcha, { RecaptchaRef } from 'react-native-recaptcha-that-works';

const styles = StyleSheet.create({
  safeArea: {
    flex: 1,
  },
  container: {
    backgroundColor: '#00ff00',
    justifyContent: 'center',
    alignItems: 'center',
    flex: 1,
  },
});

const App = () => {
  const size = 'invisible';
  const [token, setToken] = useState('<none>');

  const $recaptcha = useRef<RecaptchaRef | null>(null);

  const handleOpenPress = useCallback(() => {
    $recaptcha.current?.open();
  }, []);

  const handleClosePress = useCallback(() => {
    $recaptcha.current?.close();
  }, []);

  return (
    <SafeAreaView style={styles.safeArea}>
      <StatusBar barStyle="dark-content" />
      <View style={styles.container}>
        <Button onPress={handleOpenPress} title="Open" />
        <Text>Token: {token}</Text>
        <Text>Size: {size}</Text>
      </View>

      <Recaptcha
        ref={$recaptcha}
        lang="pt"
        headerComponent={
          <Button title="Close modal" onPress={handleClosePress} />
        }
        footerComponent={<Text>Footer here</Text>}
        siteKey="6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ_MXjiZKhI"
        baseUrl="http://127.0.0.1"
        size={size}
        theme="dark"
        onLoad={() => Alert.alert('onLoad event')}
        onClose={() => Alert.alert('onClose event')}
        onError={(err) => {
          Alert.alert('onError event');
          console.warn(err);
        }}
        onExpire={() => Alert.alert('onExpire event')}
        onVerify={(token) => {
          Alert.alert('onVerify event');
          setToken(token);
        }}
        enterprise={false}
        hideBadge={false}
      />
    </SafeAreaView>
  );
};
```
## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-webview 的原生端代码，如已在鸿蒙工程中引入过这个库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-webview 文档](/zh-cn/react-native-webview.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.28; OH SDK: HarmonyOS-Next-DB2 5.0.0.31 (API Version 12 Beta2); IDE: DevEco Studio: 5.0.3.500; ROM: 3.0.0.31;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name             | Description                                                                                                                                                                                                                                                                                        | Type                                                                                                       | Required | Platform    | HarmonyOS Support |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| headerComponent  | 在模态框顶部渲染的组件                                                                                                                                                                                                                                                             | `React Element`                                                                                            | no       | iOS,Android | yes               |
| footerComponent  | 	在模态框底部渲染的组件                                                                                                                                                                                                                                                          | `React Element`                                                                                            | no       | iOS,Android | yes               |
| loadingComponent | 自定义加载组件                                                                                                                                                                                                                                                                      | `React Element`                                                                                            | no       | iOS,Android | yes               |
| style            | 自定义默认样式，如背景色                                                                                                                                                                                                                                                 | [`ViewStyle`](https://reactnative.dev/docs/view-style-props)                                               | no       | iOS,Android | yes               |
| modalProps       | 覆盖模态框属性                                                                                                                                                                                                                                                                          | [ModalProps](https://reactnative.dev/docs/modal)                                                           | no       | iOS,Android | yes               |
| webViewProps     | 覆盖WebView属性                                                                                                                                                                                                                                                                        | [WebViewProps](https://github.com/react-native-webview/react-native-webview/blob/master/docs/Reference.md) | no       | iOS,Android | yes               |
| lang             | [语言代码](https://developers.google.com/recaptcha/docs/language).                                                                                                                                                                                                                            | `string`                                                                                                   | no       | iOS,Android | yes               |
| siteKey          | (必需) 您的Web reCAPTCHA站点密钥。(必须使用Web密钥，而不是Android密钥)                                                                                                                                                                                                                | `string`                                                                                                   | yes      | iOS,Android | yes               |
| baseUrl          | (必需) 在reCAPTCHA控制台设置中配置的URL(域名)。(例如http://my.domain.com) (另请参见https://github.com/douglasjunior/react-native-recaptcha-that-works/issues/34)                                                                                                          | `string`                                                                                                   | yes      | iOS,Android | yes               |
| size             | 小部件的大小                                                                                                                                                                                                                                                                            | `'invisible'`, `'normal'` or `'compact'`                                                                   | no       | iOS,Android | yes               |
| theme            | 小部件的颜色主题                                                                                                                                                                                                                                                                     | `'dark'` or `'light'`                                                                                      | no       | iOS,Android | yes               |
| onLoad           | 回调函数，在reCAPTCHA准备使用时执行                                                                                                                                                                                                                                  | `function()`                                                                                               | no       | iOS,Android | yes               |
| onVerify         | (必需) 回调函数，在用户提交成功响应时执行。reCAPTCHA响应令牌将传递给您的回调函数                                                                                                                                                     | `function(token)`                                                                                          | yes      | iOS,Android | yes               |
| onExpire         | 回调函数，在reCAPTCHA响应过期且用户需要重新验证时执行。仅在onVerify调用后长时间保持webview打开时有效                                                                                                        | `function()`                                                                                               | no       | iOS,Android | yes               |
| onError          | 回调函数，在reCAPTCHA遇到错误(通常是网络连接)且无法继续直到连接恢复时执行。如果您在此处指定函数，您需要负责通知用户应该重试                                             | `function(error)`                                                                                          | no       | iOS,Android | yes               |
| onClose          | 回调函数，在模态框关闭时执行                                                                                                                                                                                                                                            | `function()`                                                                                               | no       | iOS,Android | yes               |
| recaptchaDomain  | 	reCAPTCHA有效API的主机名。[查看详情](https://developers.google.com/recaptcha/docs/faq#can-i-use-recaptcha-globally).                                                                                                                                                             | `string`                                                                                                   | no       | iOS,Android | yes               |
| hideBadge        | 当size = 'invisible'时，只要您在用户流程中明显包含reCAPTCHA品牌，就可以隐藏徽章。[查看详情](https://developers.google.com/recaptcha/docs/faq#id-like-to-hide-the-recaptcha-badge.-what-is-allowed).                                          | `boolean`                                                                                                  | no       | iOS,Android | yes               |
| enterprise       | 使用新的[reCAPTCHA企业版API](https://cloud.google.com/recaptcha-enterprise/docs/using-features)。注意：对于企业版，您需要在创建siteKey时选择size。[查看详情](https://github.com/douglasjunior/react-native-recaptcha-that-works/issues/55#issuecomment-2107089307). | `boolean` (enterprise)                                                                                     | no       | iOS,Android | yes               |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name  | Description                | Type       | Required | Platform    | HarmonyOS Support |
| ----- | -------------------------- | ---------- | -------- | ----------- | ----------------- |
| open  | 打开 reCAPTCHA 模态框  | `function` | no       | iOS,Android | yes               |
| close | 关闭 reCAPTCHA 模态框 | `function` | no       | iOS,Android | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/douglasjunior/react-native-recaptcha-that-works/blob/master/LICENSE) ，请自由地享受和参与开源。