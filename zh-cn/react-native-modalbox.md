> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-modalbox</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/maxs15/react-native-modalbox">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/maxs15/react-native-modalbox/blob/master/License.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-modalbox)

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                     | 支持RN版本 |
| ----------- | ------------------------------------------------------------ | ---------- |
| 2.0.2 | [@react-native-oh-tpl/react-native-modalbox Releases](https://github.com/react-native-oh-library/react-native-modalbox/releases) | 0.72       |
| 2.1.0   | [@react-native-ohos/react-native-modalbox Releases]()        | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-modalbox

# 0.77
npm install @react-native-ohos/react-native-modalbox
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-modalbox

# 0.77
yarn add @react-native-ohos/react-native-modalbox
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import {
  ScrollView,
  Easing,
  View,
  Button,
  Text,
  StyleSheet,
  TextInput,
} from 'react-native';

import React, {useState, useRef} from 'react';

import ModalBox from 'react-native-modalbox';

export const ModalBoxDemo = () => {
  const [isOpenVal, setIsOpenVal] = useState(false);
  const [isOpenVal1, setIsOpenVal1] = useState(false);
  const [isOpenVal2, setIsOpenVal2] = useState(false);
  const [isOpenVal3, setIsOpenVal3] = useState(false);
  const [isOpenVal4, setIsOpenVal4] = useState(false);
  const [isOpenVal5, setIsOpenVal5] = useState(false);
  const [isOpenVal6, setIsOpenVal6] = useState(false);
  const [isOpenVal7, setIsOpenVal7] = useState(false);
  const [isOpenVal8, setIsOpenVal8] = useState(false);
  const [isOpenVal9, setIsOpenVal9] = useState(false);
  const [isOpenVal10, setIsOpenVal10] = useState(false);
  const [isOpenVal11, setIsOpenVal11] = useState(false);
  const [isOpenVal12, setIsOpenVal12] = useState(false);
  const [isOpenVal13, setIsOpenVal13] = useState(false);
  const [isOpenVal14, setIsOpenVal14] = useState(false);
  const [isOpenVal15, setIsOpenVal15] = useState(false);
  const [isOpenVal16, setIsOpenVal16] = useState(false);
  const [isOpenVal17, setIsOpenVal17] = useState(false);
  const [isOpenVal18, setIsOpenVal18] = useState(false);
  const [isOpenVal19, setIsOpenVal19] = useState(false);
  const [isOpenVal20, setIsOpenVal20] = useState(false);
  const [isOpenVal21, setIsOpenVal21] = useState(false);
  const [isOpenVal22, setIsOpenVal22] = useState(false);
  const [isOpenVal23, setIsOpenVal23] = useState(false);
  const [isOpenVal24, setIsOpenVal24] = useState(false);

  const btnRef1 = useRef(null);

  const openModalBox = () => {
    btnRef1.current?.open();
  };
  const closeModalBox = () => {
    btnRef1.current?.close();
  };
  return (
    <ScrollView>
      <View style={styles.body}>
        <Button title="isOpen" onPress={() => setIsOpenVal(!isOpenVal)} />
        <ModalBox style={[styles.modal]} isOpen={isOpenVal} coverScreen={true}>
          <Text style={[styles.modalText]}>Modal is open</Text>
          <Button
            title={'close ModalBox'}
            onPress={() => setIsOpenVal(!isOpenVal)}
          />
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button title="isDisabled" onPress={() => setIsOpenVal1(!isOpenVal1)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal1}
          isDisabled={true}
          coverScreen={true}>
          <Text style={[styles.modalText]}>Modal is isDisabled</Text>
          <Button title={'close ModalBox'} />
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="backdropPressToClose"
          onPress={() => setIsOpenVal2(!isOpenVal2)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal2}
          coverScreen={true}
          backdropPressToClose={true}>
          <Text style={[styles.modalText]}>
            Close the the modal by pressing on the backdrop
          </Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="swipeToClose"
          onPress={() => setIsOpenVal3(!isOpenVal3)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal3}
          coverScreen={true}
          swipeToClose={true}>
          <Text style={[styles.modalText]}>
            Close the the modal by swipe down
          </Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="swipeThreshold"
          onPress={() => setIsOpenVal4(!isOpenVal4)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal4}
          coverScreen={true}
          swipeToClose={true}
          swipeThreshold={10}>
          <Text style={[styles.modalText]}>
            Close the the modal by swipe down 10px
          </Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button title="swipeArea" onPress={() => setIsOpenVal5(!isOpenVal5)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal5}
          coverScreen={true}
          swipeToClose={true}
          swipeArea={20}>
          <Text style={[styles.modalText]}>
            Close the the modal by swipe down swipeArea:20
          </Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="position:center"
          onPress={() => setIsOpenVal6(!isOpenVal6)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal6}
          coverScreen={true}
          backdropPressToClose={true}
          position={'center'}>
          <Text style={[styles.modalText]}>position is center</Text>
        </ModalBox>
        <Button
          title="position:bottom"
          onPress={() => setIsOpenVal7(!isOpenVal7)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal7}
          coverScreen={true}
          backdropPressToClose={true}
          position={'bottom'}>
          <Text style={[styles.modalText]}>position is bottom</Text>
        </ModalBox>
      </View>

      <View style={styles.body}>
        <Button title="entry:top" onPress={() => setIsOpenVal8(!isOpenVal8)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal8}
          coverScreen={true}
          backdropPressToClose={true}
          entry={'top'}>
          <Text style={[styles.modalText]}>entry is top</Text>
        </ModalBox>
        <Button
          title="entry:bottom"
          onPress={() => setIsOpenVal9(!isOpenVal9)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal9}
          coverScreen={true}
          backdropPressToClose={true}
          entry={'bottom'}>
          <Text style={[styles.modalText]}>entry is bottom</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button title="backdrop" onPress={() => setIsOpenVal10(!isOpenVal10)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal10}
          coverScreen={true}
          backdropPressToClose={true}
          backdrop={false}>
          <Text style={[styles.modalText]}>backdrop is false</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="backdropOpacity"
          onPress={() => setIsOpenVal11(!isOpenVal11)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal11}
          coverScreen={true}
          backdropPressToClose={true}
          backdropOpacity={0.5}>
          <Text style={[styles.modalText]}>backdropOpacity: 0.5</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="backdropColor"
          onPress={() => setIsOpenVal12(!isOpenVal12)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal12}
          coverScreen={true}
          backdropPressToClose={true}
          backdropColor={'green'}>
          <Text style={[styles.modalText]}>backdropColor: 'green'</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="backdropContent"
          onPress={() => setIsOpenVal13(!isOpenVal13)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal13}
          coverScreen={true}
          backdropPressToClose={true}
          backdropOpacity={0.5}
          backdropContent={
            <View style={{flex: 1, backgroundColor: 'rgba(0, 0, 0, 0.5)'}}>
              <Text style={{color: 'red', fontSize: 20}}>这是背景内容</Text>
            </View>
          }>
          <Text style={[styles.modalText]}>ModalBoxContent</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="animationDuration"
          onPress={() => setIsOpenVal14(!isOpenVal14)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal14}
          coverScreen={true}
          backdropPressToClose={true}
          animationDuration={1000}>
          <Text style={[styles.modalText]}>animationDuration:1000ms</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button title="easing" onPress={() => setIsOpenVal15(!isOpenVal15)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal15}
          coverScreen={true}
          backdropPressToClose={true}
          easing={ModalBox.easing}>
          <Text style={[styles.modalText]}>easing: 使用预定义的easing函数</Text>
        </ModalBox>
        <Button
          title="easing:custom"
          onPress={() => setIsOpenVal16(!isOpenVal16)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal16}
          coverScreen={true}
          backdropPressToClose={true}
          easing={Easing.elastic(8)}>
          <Text style={[styles.modalText]}>easing: 自定义easing函数</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="startOpen"
          onPress={() => setIsOpenVal18(!isOpenVal18)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal18}
          coverScreen={true}
          backdropPressToClose={true}
          startOpen={true}
          onClosed={() => console.log('Modal closed')}
          onOpened={() => console.log('Modal opened')}
          onClosingState={() => console.log('Modal closing state changed')}>
          <Text style={[styles.modalText]}>startOpen is true</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="coverScreen"
          onPress={() => setIsOpenVal19(!isOpenVal19)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal19}
          coverScreen={true}
          backdropPressToClose={true}>
          <Text style={[styles.modalText]}>coverScreen is true</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="keyboardTopOffset"
          onPress={() => setIsOpenVal20(!isOpenVal20)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal20}
          coverScreen={true}
          keyboardTopOffset={10}
          position={'bottom'}
          backdropPressToClose={true}>
          <Text style={[styles.modalText]}>keyboardTopOffset: 50</Text>
          <TextInput
            placeholder="text"
            placeholderTextColor="#9a73ef"
            autoCapitalize="none"
          />
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="useNativeDriver"
          onPress={() => setIsOpenVal21(!isOpenVal21)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal21}
          coverScreen={true}
          easing={Easing.elastic(8)}
          useNativeDriver={true}
          backdropPressToClose={true}>
          <Text style={[styles.modalText]}>useNativeDriver is true</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button title="onOpened" onPress={() => setIsOpenVal22(!isOpenVal22)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal22}
          coverScreen={true}
          onOpened={()=>console.log('...onOpened')}>
          <Text style={[styles.modalText]}>onOpened</Text>
        </ModalBox>
      </View>

      <View style={styles.body}>
        <Button title="onClosed" onPress={() => setIsOpenVal23(!isOpenVal23)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal23}
          coverScreen={true}
          onClosed={()=>console.log('...onClosed')}>
          <Text style={[styles.modalText]}>onClosed</Text>
        </ModalBox>
      </View>

      <View style={styles.body}>
        <Button
          title="onClosingState"
          onPress={() => setIsOpenVal24(!isOpenVal24)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal24}
          coverScreen={true}
          onClosingState={()=>console.log('...onClosingState')}>
          <Text style={[styles.modalText]}>onClosingState</Text>
        </ModalBox>
      </View>

      <View style={styles.body}>
        <Button title="open" onPress={openModalBox} />
        <Button title="close" onPress={closeModalBox} />
        <ModalBox ref={btnRef1} style={[styles.modal]} coverScreen={true}>
          <Text style={[styles.modalText]}>ModalBox open</Text>
        </ModalBox>
      </View>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  input: {},
  modal: {
    height: 300,
    width: 300,
    justifyContent: 'center',
    alignItems: 'center',
  },
  modalText: {
    fontSize: 20,
    margin: 10,
    color: 'black',
  },
  module: {
    margin: 15,
  },
  moduleName: {
    fontSize: 25,
    fontWeight: '700',
    marginBottom: 4,
    color: '#fff',
  },
  moduleContent: {
    fontSize: 16,
    fontWeight: '500',
    marginBottom: 4,
    color: '#fff',
  },
  moduleButton: {
    backgroundColor: 'deepskyblue',
    height: 34,
  },
  buttonText: {
    fontSize: 18,
    fontWeight: '400',
    color: '#fff',
    textAlign: 'center',
    lineHeight: 32,
    verticalAlign: 'middle',
  },
  body: {},
});
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                 |                         Description                          |      Type      | Required |  Platform   | HarmonyOS Support |
| :------------------- | :----------------------------------------------------------: | :------------: | :------: | :---------: | :---------------: |
| isOpen               | 打开/关闭模态框，可选，您可以使用 open/close 方法代替 |     `bool`     |    no    | iOS/Android |        yes        |
| isDisabled           |     禁用模态框的所有操作（打开、关闭、滑动）     |     `bool`     |    no    | iOS/Android |        yes        |
| backdropPressToClose |       点击背景关闭模态框       |     `bool`     |    no    | iOS/Android |        yes        |
| swipeToClose         |    设置为 true 时启用向下滑动关闭功能    |     `bool`     |    no    | iOS/Android |        yes        |
| swipeThreshold       |     关闭模态框需要达到的像素阈值      |    `number`    |    no    | iOS/Android |        yes        |
| swipeArea            | 可滑动区域的高度，默认为窗口高度 |    `number`    |    no    | iOS/Android |        yes        |
| position             |   控制模态框位置：top、center 或 bottom   |    `string`    |    no    | iOS/Android |        yes        |
| entry                |       	控制模态框进入位置：top 或 bottom       |    `string`    |    no    | iOS/Android |        yes        |
| backdrop             |             在模态框后显示背景              |     `bool`     |    no    | iOS/Android |        yes        |
| backdropOpacity      |                   设置模态框背景的透明度                    |    `number`    |    no    | iOS/Android |        yes        |
| backdropColor        |               设置模态框背景的颜色                |    `string`    |    no    | iOS/Android |        yes        |
| backdropContent      | 在背景中添加元素（例如关闭按钮）  | `ReactElement` |    no    | iOS/Android |        yes        |
| animationDuration    |                  动画持续时间                   |    `number`    |    no    | iOS/Android |        yes        |
| easing               |      应用于打开模态框动画的缓动函数      |   `function`   |    no    | iOS/Android |        yes        |
| backButtonClose      | （仅 Android）接收返回按钮事件时关闭模态框  |     `bool`     |    no    |   Android   |        no         |
| startOpen            | 	组件挂载时自动打开模态框 |     `bool`     |    no    | iOS/Android |        yes        |
| coverScreen          | 使用 RN Modal 组件覆盖整个屏幕 |     `bool`     |    no    | iOS/Android |        yes        |
| keyboardTopOffset    | 	防止键盘打开时模态框覆盖 iOS 状态栏 |    `number`    |    no    | iOS/Android |        yes        |
| useNativeDriver      | 	启用硬件加速来驱动模态框动画，注意启用可能导致动画闪烁 |     `bool`     |    no    | iOS/Android |        yes        |
| onClosed       |                                          模态框关闭且动画完成时触发                                           | `function` |    no    | iOS/Android |        yes        |
| onOpened       |                                          模态框打开且动画完成时触发                                           | `function` |    no    | iOS/Android |        yes        |
| onClosingState | 滑动关闭功能状态改变时触发（可用于更改模态框内容或显示消息） | `function` |    no    | iOS/Android |        yes        |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name  |   Description   |    Type    | Required |  Platform   | HarmonyOS Support |
| :---- | :-------------: | :--------: | :------: | :---------: | :---------------: |
| open  | 打开模态框  | `function` |    no    | iOS/Android |        yes        |
| close | 关闭模态框 | `function` |    no    | iOS/Android |        yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/maxs15/react-native-modalbox/blob/master/License.txt) ，请自由地享受和参与开源。

