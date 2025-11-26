> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-url-polyfill</code> </h1>
</p>

| 三方库版本                 | 支持RN版本                 |
| ------------------------- | -------------------------- |
| 2.0.0               |  0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install --save react-native-url-polyfill@2.0.0
```

#### **yarn**

```bash
yarn add react-native-url-polyfill@2.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { ScrollView, Text, Button, View, StyleSheet } from 'react-native';
import { URL, URLSearchParams } from 'react-native-url-polyfill';

const URLPolyfillDemo = () => {
  const url = new URL('https://github.com');
  const searchParams = new URLSearchParams('abc=456&rn=ReactNative&abc=javascript');

  const [appendResult, setAppendResult] = useState('');
  const [setResult, setSetResult] = useState('');
  const [deleteResult, setDeleteResult] = useState('');
    
  // searchParams.append()
  const appendExample = () => {
    searchParams.append('q', 'CodeHub');
    let result = searchParams.toString();
    setAppendResult(result);
  }

  // searchParams.set()
  const setExample = () => {
    searchParams.set('abc', 'Gitee');
    let result = searchParams.toString();
    setSetResult(result);
  }

  // searchParams.delete()
  const deleteExample = () => {
    searchParams.delete('abc', 'javascript');
    let result = searchParams.toString();
    setDeleteResult(result);
  }

  return (
    <ScrollView>
      <View>
      	<View>
          <Text style={styles.text}>property: href</Text>
          <Text style={styles.result} allowFontScaling>{url.href}</Text>
        </View>

        <View>
          <Text style={styles.text}>Method：append（q,CodeHub）</Text>
          <Button
            title="append"
            color="#9a73ef"
            onPress={appendExample}
          />
          <Text style={styles.result} allowFontScaling>{appendResult}</Text>
        </View>

        <View>
          <Text style={styles.text}>Method：set（abc,Gitee））</Text>
          <Button
            title="set"
            color="#9a73ef"
            onPress={setExample}
          />
          <Text style={styles.result} allowFontScaling>{setResult}</Text>
        </View>

        <View>
          <Text style={styles.text}>Method：delete（abc,javascript）</Text>
          <Button
            title="delete"
            color="#9a73ef"
            onPress={deleteExample}
          />
          <Text style={styles.result} allowFontScaling>{deleteResult}</Text>
        </View>
      </View>
    </ScrollView>
 )
};

const styles = StyleSheet.create({
  text: {
    fontSize: 18,
    marginBottom: 10,
    color: 'red',
  },
  result: {
    marginTop: 10,
    fontSize: 18,
    marginBottom: 10,
    color: 'black',
  }
});

export default URLPolyfillDemo;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name         | Description                                                  | Type            | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------------------------------------ | --------------- | -------- | ----------- | :---------------- |
| hash         | 获取或设置 URL 的片段标识部分               | string          | no       | Android/iOS | yes               |
| host         | 获取或设置 URL 的主机部分                   | string          | no       | Android/iOS | yes               |
| hostname     | 获取或设置 URL 的主机名部分              | string          | no       | Android/iOS | yes               |
| href         | 获取或设置序列化的 URL                            | string          | no       | Android/iOS | yes               |
| origin       | 获取 URL 源的只读序列化        | string          | no       | Android/iOS | yes               |
| password     | 获取或设置 URL 的密码部分               | string          | no       | Android/iOS | yes               |
| pathname     | 获取或设置 URL 的路径部分                   | string          | no       | Android/iOS | yes               |
| port         | 获取或设置 URL 的端口部分                   | string          | no       | Android/iOS | yes               |
| protocol     | 获取或设置 URL 的协议部分               | string          | no       | Android/iOS | yes               |
| search       | 获取或设置序列化的查询部分       | string          | no       | Android/iOS | yes               |
| searchParams | 获取表示 URL 查询参数的 `URLSearchParams` 对象 | URLSearchParams | no       | Android/iOS | yes               |
| username     | 获取或设置 URL 的用户名部分               | string          | no       | Android/iOS | yes               |
| size         | `URLSearchParams` 对象上的参数条目总数 | number          | no       | Android/iOS | yes               |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name     | Description                                                  | Type                               | Required | Platform    | HarmonyOS Support |
| -------- | ------------------------------------------------------------ | ---------------------------------- | -------- | ----------- | ----------------- |
| toString | 返回 URL 的序列化字符串 | string                             | no       | Android/iOS | yes               |
| toJSON   | 返回 URL 的序列化字符串 | string                             | no       | Android/iOS | yes               |
| append   | 向查询字符串添加新的参数键值对            | void                               | no       | Android/iOS | yes               |
| delete   | 删除指定参数名的所有键值对 | void                               | no       | Android/iOS | yes               |
| entries  | 返回包含所有参数键值对的 ES6 `Iterator` | IterableIterator<[string, string]> | no       | Android/iOS | yes               |
| forEach  | 遍历所有参数键值对并执行回调函数 | void                               | no       | Android/iOS | yes               |
| get      | 获取指定参数名的第一个值，不存在时返回 null	 | string \| null                     | no       | Android/iOS | yes               |
| getAll   | 获取指定参数名的所有值，不存在时返回空数组 | string[]                           | no       | Android/iOS | yes               |
| has      | 检查是否存在指定参数名的键值对 | boolean                            | no       | Android/iOS | yes               |
| keys     | 返回所有参数名的 ES6 `Iterator` | IterableIterator<string>           | no       | Android/iOS | yes               |
| set      | 设置指定参数名的值 | void                               | no       | Android/iOS | yes               |
| sort     | 按参数名对所有键值对进行排序  | void                               | no       | Android/iOS | yes               |
| toString | 返回经过百分比编码的查询参数字符串 | string                             | no       | Android/iOS | yes               |
| values   | 返回所有参数值的 ES6 `Iterator` | IterableIterator<string>           | no       | Android/iOS | yes               |

## 遗留问题

## 其他

- [ ] 本库在Harmony、iOS、Android都存在的问题，URLSearchParams对象上size属性无法获取对应参数条目的总数，问题: [issue#472](https://github.com/charpeni/react-native-url-polyfill/issues/472)
- [ ] 本库在Harmony、iOS、Android都存在的问题，URLSearchParams对象上sort方法按名称对现有的key-value进行排序，排序无效果， 问题: [issue#471](https://github.com/charpeni/react-native-url-polyfill/issues/471)

## 开源协议

本项目基于[The MIT License](https://github.com/charpeni/react-native-url-polyfill/blob/main/LICENSE) ，请自由地享受和参与开源。
