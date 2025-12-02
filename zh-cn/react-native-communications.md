> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-communications</code> </h1>
</p>

> [!TIP] [GitHub address](https://github.com/davebeehively/react-native-communications)

请到三方库的 Releases发布地址查看配套的版本信息：

| 三方库版本 | 支持RN版本 |
| ----------| ---------- |
| 2.2.1    |  0.72/0.77 |


对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-communications@2.2.1
```

#### **yarn**

```bash
yarn add react-native-communications@2.2.1
```

<!-- tabs:end -->

>[!WARNING] 使用时 import 的库名不变。

```js
var React = require('react-native');
var {
  StyleSheet,
  View,
  TouchableOpacity,
  Text
} = React;

import { phonecall, text, textWithoutEncoding, email, web } from 'react-native-communications';

const RNCommunications = () => {
  const handleButton1Press = () => {
    phonecall('0123456789', false)
  }
  const handleButton2Press = () => {
    email(['email@xxx.com'], null, null, 'My Subject', 'My body text')
  }
  const handleButton3Press = () => {
    text('0123456789')
  }
  const handleButton4Press = () => {
    web('https://www.baidu.com')
  }
  const handleButton5Press = () => {
    textWithoutEncoding('0123456789', "9999999")
  }

  return (
    <View style={styles.container}>
      <TouchableOpacity style={styles.button} onPress={handleButton1Press}>
        <Text>Make phonecall</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={handleButton2Press}>
        <Text>Send an email</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={handleButton3Press}>
        <Text>Send a text only phonenumber</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={handleButton4Press}>
        <Text>web to baidu</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={handleButton5Press}>
        <Text>Send a text with body</Text>
      </TouchableOpacity>
    </View>
  );
};

var styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  button: {
    padding: 10,
    margin: 5,
    backgroundColor: 'white',
    borderRadius: 5,
  }
});

export default RNCommunications;
```
## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| phonecall  | 拨打电话         | function  | yes | All      | yes |
| email  | 发送电子邮件      | function  | yes | All      | no |
| text  | 发送文本消息          | function  | yes | All      | yes |
| textWithoutEncoding  | 发送文本消息，但是不进行编码处理       | function  | yes | All      | yes |
| web  | 打开指定的网页 URL         | function  | yes | All      | yes |

## 遗留问题

- [ ] HarmonyOS 侧没有邮箱应用，导致email方法无法打开发送邮件界面。
- [ ] text添加body之后，没法在短信界面拆分进短信输入栏，框架侧接口Linking.canOpenURL不支持。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/davebeehively/react-native-communications/blob/master/LICENSE) ，请自由地享受和参与开源。
