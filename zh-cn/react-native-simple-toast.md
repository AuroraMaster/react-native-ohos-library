> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-simple-toast</code></h1>
</p>
<p align="center">
    <a href="https://github.com/vonovak/react-native-simple-toast">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vonovak/react-native-simple-toast/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-simple-toast)

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-simple-toast`，具体版本所属关系如下：

| Version                        | Package Name       | Repository          |  Release            |Supported RN Version  |
| ------------------------------ | ----------------   | ------------------- | ------------------- | -------------------- |
| 3.3.1  | @react-native-oh-tpl/react-native-simple-toast | [Github](https://github.com/react-native-oh-library/react-native-simple-toast) | [Github Releases](https://github.com/react-native-oh-library/react-native-simple-toast/releases) | 0.72 |
| 3.4.0 | @react-native-ohos/react-native-simple-toast   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-simple-toast) | [GitCode Releases]() | 0.77 |

## 安装与使用

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# V3.3.1
npm install @react-native-oh-tpl/react-native-simple-toast

# V3.4.0
npm install @react-native-ohos/react-native-simple-toast
```

#### **yarn**

```bash
# V3.3.1
yarn add @react-native-oh-tpl/react-native-simple-toast

# V3.4.0
yarn add @react-native-ohos/react-native-simple-toast
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';

import {
  StyleSheet,
  View,
  Button,
  Alert,
  TextInput,
  ScrollView,
  Pressable,
  Modal,
  Text,
} from 'react-native';
import Toast from 'react-native-simple-toast';
import { useState } from 'react';



const ToastTest = () => {
  const [modalVisible, setModalVisible] = useState(false);
  return (
    <>
      <Modal
        animationType="slide"
        transparent={true}
        visible={modalVisible}
        onRequestClose={() => {
          Alert.alert('Modal has been closed.');
          setModalVisible(!modalVisible);
        }}
      >
        <View style={styles.centeredView}>
          <View style={styles.modalView}>
            <Text style={styles.modalText}>Hello World!</Text>
            <Pressable
              style={[styles.button, styles.buttonClose]}
              onPress={() => setModalVisible(!modalVisible)}
            >
              <Text style={styles.textStyle}>Hide Modal</Text>
            </Pressable>
          </View>
        </View>
      </Modal>

      <ScrollView
        contentContainerStyle={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}
        keyboardDismissMode={'on-drag'}
        keyboardShouldPersistTaps={'always'}
        automaticallyAdjustKeyboardInsets
        style={{ backgroundColor: 'white' }}
      >
        <View style={styles.container}>
          <Button
            title={'simple toast'}
            color={'#2196F3'}
            onPress={() => {
              Toast.show('This is a toast.', Toast.SHORT);
            }}
          />
          <View style={{ height: 20 }} />
          <Button
            title={'tap to dismiss toast'}
            color={'#f44336'}
            onPress={() => {
              Toast.show('Tap to dismiss toast.', Toast.LONG, {
                tapToDismissEnabled: true,
              });
            }}
          />
        </View>
      </ScrollView>
    </>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
    padding: 16,
    backgroundColor: '#fff',
  },
  centeredView: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: 'rgba(0,0,0,0.3)',
  },
  modalView: {
    margin: 20,
    backgroundColor: 'white',
    borderRadius: 8,
    padding: 32,
    alignItems: 'center',
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.25,
    shadowRadius: 4,
    elevation: 5,
  },
  modalText: {
    marginBottom: 16,
    textAlign: 'center',
    fontSize: 18,
    color: '#333',
  },
  button: {
    borderRadius: 8,
    paddingVertical: 10,
    paddingHorizontal: 20,
    elevation: 2,
    backgroundColor: '#2196F3',
  },
  buttonClose: {
    backgroundColor: '#f44336',
    marginTop: 12,
  },
  textStyle: {
    color: 'white',
    fontWeight: 'bold',
    textAlign: 'center',
  },
});

export default ToastTest;
```
## 约束与限制

### 兼容性
要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机ROM。

1. RNOH：0.72.23; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.19
2. RNOH：0.72.96; SDK：HarmonyOS 5.1.1 Release SDK; IDE：DevEco Studio 5.1.1.840; ROM：6.0.0;
3. RNOH：0.77.18; SDK：HarmonyOS 5.1.1 Release SDK; IDE：DevEco Studio 5.1.1.840; ROM：6.0.0;


## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name                   | Description               | Required | Platform | HarmonyOS Support |
| ---------------------- |---------------------------| -------- |----------|-------------------|
| show(message, duration, options)        | 展示轻提示                        | No       | All      | partially         |
| showWithGravity(message, duration, gravity, options)   | 可设置为顶部、底部和居中位置的轻提示 | No       | All      | No                |
| showWithGravityAndOffset(message,duration,gravity,xOffset,yOffset,options,); | 可设置x轴和y轴偏移的轻提示           | No       | All      | No                |


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description          | Type   | Required | HarmonyOS Support |
| ------ | -------------------- | ------ | -------- | ----------------- |
| LONG   | toast显示时间:LONG   | number | /        | yes               |
| SHORT  | toast显示时间：SHORT | number | /        | yes               |
| TOP    | toast显示位置:TOP    | number | /        | no                |
| BOTTOM | toast显示位置:BOTTOM | number | /        | no                |
| CENTER | toast显示位置:CENTER | number | /        | no                |

## 遗留问题

- [ ]  HarmonyOS toast不支持修改字体，背景色等样式[issue#3](https://github.com/react-native-oh-library/react-native-simple-toast/issues/3)
- [ ]  HarmonyOS rn框架toast组件不支持设置位置及偏移[issue#2](https://github.com/react-native-oh-library/react-native-simple-toast/issues/2)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/vonovak/react-native-simple-toast/blob/master/LICENSE) ，请自由地享受和参与开源。