> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-material-textfield</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/n4kz/react-native-material-textfield">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/n4kz/react-native-material-textfield/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-BSD-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-material-textfield/tree/sig)

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-material-textfield`，具体版本所属关系如下：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.16.1     | [@react-native-oh-tpl/react-native-material-textfield Releases](https://github.com/react-native-oh-library/react-native-material-textfield/releases) | 0.72       |
| 0.17.0     | [@react-native-ohos/react-native-material-textfield Releases]() | 0.77       |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

0.72

```bash
npm install @react-native-oh-tpl/react-native-material-textfield
npm install deprecated-react-native-prop-types
```

0.77

```
npm install @react-native-ohos/react-native-material-textfield
npm install deprecated-react-native-prop-types
```

#### **yarn**

0.72

```bash
yarn add @react-native-oh-tpl/react-native-material-textfield
yarn add deprecated-react-native-prop-types
```

0.77

```
yarn add @react-native-ohos/react-native-material-textfield
yarn add deprecated-react-native-prop-types
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx

import React, {useState} from 'react';
import {  StyleSheet,SafeAreaView,Platform,ScrollView,View,Button} from 'react-native';
import {
  TextField,
} from 'react-native-material-textfield';


let defaults = {
  firstname: 'Eddard',
  lastname: 'Stark'
};


// 导出组件
export default function TextfieldDemo() {
  const [errors, setErrors] = useState({});  
  const [combinedState, setCombinedState] = useState({  
    ...defaults,  
    secureTextEntry:true, // 从上面的 useState 中取得值  
  }); 
  const firstnameRef  = React.createRef();;
  const lastnameRef  = React.createRef();
  const aboutRef  = React.createRef();
  const emailRef = React.createRef();
  const passwordRef = React.createRef();

  const onSubmit = () => {
    let errors = {};
    ['firstname', 'lastname', 'email', 'password']
    .forEach((name) => {
        const ref = name === 'firstname' ? firstnameRef :  
                    name === 'lastname' ? lastnameRef :
                    name === 'email' ? emailRef : 
                    passwordRef;       
        let value = ref.current ? ref.current.value() : ''; // 从 ref 中获取值 
        if(!value) {
          errors[name] = 'Should not be empty';
        } else {
          if('password' === name && value.length < 6) {
            errors[name] = 'Too short';
          }
        }
    });
    setErrors(errors)
  }

  const onChangeText= () => {
    ['firstname', 'lastname', 'email', 'password']
    .forEach((name) => {
      const ref = name === 'firstname' ? firstnameRef :  
      name === 'lastname' ? lastnameRef :
      name === 'email' ? emailRef : 
      passwordRef;      
      let value = ref.current ? ref.current.value() : ''; // 从 ref 中获取值  
      setCombinedState({  
        ...combinedState,  
        // 例如，更新 firstname 属性  
        [name]: value
      });  
    })
  }
 
  return (
    <SafeAreaView style={styles.safeContainer}>
        <ScrollView
            style={styles.scroll}
            contentContainerStyle={styles.contentContainer}
            keyboardShouldPersistTaps='handled'
          >
          <View style={styles.container}>
              <TextField
                ref={firstnameRef}
                value={defaults.firstname}
                autoCorrect={false}
                enablesReturnKeyAutomatically={true}
                returnKeyType='next'
                label='First Name'
                onChangeText={onChangeText}
                error={errors.firstname}
              />

             <TextField
                ref={lastnameRef}
                value={defaults.lastname}
                autoCorrect={false}
                enablesReturnKeyAutomatically={true}      
                returnKeyType='next'
                label='Last Name'
                onChangeText={onChangeText}
                error={errors.lastname}
              />  

              <TextField
                ref={emailRef}
                keyboardType='email-address'
                autoCapitalize='none'
                autoCorrect={false}
                enablesReturnKeyAutomatically={true}
                returnKeyType='next'
                label='Email Address'
                onChangeText={onChangeText}
                error={errors.email}
              />

              <TextField 
                ref={passwordRef}
                autoCapitalize='none'
                autoCorrect={false}
                enablesReturnKeyAutomatically={true}
                returnKeyType='done'
                label='Password'
                title='Choose wisely'
                maxLength={30}
                onChangeText={onChangeText}
                characterRestriction={20}
                error={errors.password}
              />

             <Button title='运行' color='#841584' onPress={onSubmit}></Button>
              
          </View>
        </ScrollView>

    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeContainer: {
    flex: 1,
    backgroundColor: '#FFFFFF',
  },
  scroll: {
    backgroundColor: 'transparent',
  },

  container: {
    margin: 8,
    marginTop: Platform.select({ harmony:8,ios: 8,android: 32 }),
    flex: 1,
  },

  contentContainer: {
    padding: 8,
  },

  buttonContainer: {
    paddingTop: 8,
    margin: 8,
  }
});

```

## 约束与限制

### 兼容性

在下述版本验证通过：

RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release SDK；IDE：DevEco Studio  6.0.0.868; ROM：6.0.0.112; 

## 属性

### 此组件有以下属性:
>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|           Name           |                       Description                        |   Type   | Required |  Platform   | HarmonyOS Support |
| :----------------------: | :------------------------------------------------------: | :------: | :------: | :---------: | :---------------: |
|      **textColor**       |                       文本输入颜色                       |  String  |    No    | iOS/Android |        Yes        |
|       **fontSize**       |                     文本输入字体大小                     |  Number  |   YES    | iOS/Android |        Yes        |
|    **labelFontSize**     |                    文本框标签字体大小                    |  Number  |    No    | iOS/Android |        Yes        |
|      **lineWidth**       |                     文本框下划线宽度                     |  Number  |    No    | iOS/Android |        Yes        |
|   **activeLineWidth**    |                  文本框激活时下划线宽度                  |  Number  |    No    | iOS/Android |        Yes        |
|  **disabledLineWidth**   |                  文本框禁用时下划线宽度                  |  Number  |    No    | iOS/Android |        Yes        |
|      **tintColor**       |           文本框强调色（如光标、激活状态颜色）           |  String  |    No    | iOS/Android |        Yes        |
|      **baseColor**       |            文本框基础颜色（如下划线默认颜色）            |  String  |    No    | iOS/Android |        Yes        |
|        **label**         |                      文本框标签文本                      |  String  |    No    | iOS/Android |        Yes        |
|        **title**         |                    文本框辅助说明文本                    |  String  |    No    | iOS/Android |        Yes        |
|        **prefix**        |          文本框前缀文本（如输入框前的固定内容）          |  String  |    No    | iOS/Android |        Yes        |
|        **suffix**        |       文本框后缀文本（如输入框后的单位、固定内容）       |  String  |    No    | iOS/Android |        Yes        |
|        **error**         |                    文本框错误提示文本                    |  String  |    No    | iOS/Android |        Yes        |
|      **errorColor**      |     文本框错误状态颜色（如错误提示文本、下划线颜色）     |  String  |    No    | iOS/Android |        Yes        |
|       **lineType**       |            文本框下划线样式（如实线、虚线等）            |  String  |    No    | iOS/Android |        Yes        |
|   **disabledLineType**   |                  文本框禁用时下划线样式                  |  String  |    No    | iOS/Android |        Yes        |
|  **animationDuration**   |               文本框动画时长（单位：毫秒）               |  Number  |    No    | iOS/Android |        Yes        |
| **characterRestriction** |  文本框字符计数器软限制（提示最大输入长度，不强制拦截）  |  Number  |    No    | iOS/Android |        Yes        |
|       **disabled**       |          文本框是否禁用（禁用后无法输入和交互）          | Boolean  |    No    | iOS/Android |        Yes        |
|       **editable**       |                   文本框内容是否可编辑                   | Boolean  |    No    | iOS/Android |        Yes        |
|      **multiline**       |                  文本框是否支持多行输入                  | Boolean  |    No    | iOS/Android |        Yes        |
|     **contentInset**     |     文本框内容内边距配置对象（控制文本与边框的间距）     |  Object  |    No    | iOS/Android |        Yes        |
|     **labelOffset**      |       文本框标签位置偏移量（调整标签的 x/y 坐标）        |  Object  |    No    | iOS/Android |        Yes        |
| **inputContainerStyle**  |    文本框输入容器视图样式（如输入区域的背景、边框等）    |  Object  |    No    | iOS/Android |        Yes        |
|    **containerStyle**    |    文本框整体容器视图样式（如整个组件的背景、边距等）    |  Object  |    No    | iOS/Android |        Yes        |
|    **labelTextStyle**    |    文本框标签内部文本组件样式（如标签的字体、颜色等）    |  Object  |    No    | iOS/Android |        Yes        |
|    **titleTextStyle**    |                文本框辅助说明文本组件样式                |  Object  |    No    | iOS/Android |        Yes        |
|    **affixTextStyle**    |              文本框前缀 / 后缀文本组件样式               |  Object  |    No    | iOS/Android |        Yes        |
|      **formatText**      |   输入内容格式化回调函数（如实时格式化手机号、日期等）   | Function |    No    | iOS/Android |        Yes        |
| **renderLeftAccessory**  |       渲染文本框左侧辅助视图（如左侧图标、按钮等）       | Function |    No    | iOS/Android |        Yes        |
| **renderRightAccessory** | 渲染文本框右侧辅助视图（如右侧清除按钮、密码切换图标等） | Function |    No    | iOS/Android |        Yes        |
|     **onChangeText**     |       文本内容变化时的回调函数（返回最新输入文本）       | Function |    No    | iOS/Android |        Yes        |
|       **onFocus**        |                文本框获取焦点时的回调函数                | Function |    No    | iOS/Android |        Yes        |
|        **onBlur**        |                文本框失去焦点时的回调函数                | Function |    No    | iOS/Android |        Yes        |

## **API（TextField）**
>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|            Name            |             Description              |  Type   | Required |  Platform   | HarmonyOS Support |
| :------------------------: | :----------------------------------: | :-----: | :------: | :---------: | :---------------: |
|        **focus()**         |               获取焦点               |         |    No    | iOS/Android |        Yes        |
|         **blur()**         |               释放焦点               |         |    No    | iOS/Android |        Yes        |
|        **clear()**         |            清空文本框内容            |         |    No    | iOS/Android |        Yes        |
|        **value()**         |            获取当前输入值            | String  |    No    | iOS/Android |        Yes        |
|      **isFocused()**       |     获取当前焦点状态（是否聚焦）     | Boolean |    No    | iOS/Android |        Yes        |
|      **isErrored()**       |   获取当前错误状态（是否存在错误）   | Boolean |    No    | iOS/Android |        Yes        |
|     **isRestricted()**     |  获取当前限制状态（是否处于限制中）  | Boolean |    No    | iOS/Android |        Yes        |
|   **isDefaultVisible()**   | 获取默认值可见状态（默认值是否显示） | Boolean |    No    | iOS/Android |        Yes        |
| **isPlaceholderVisible()** | 获取占位符可见状态（占位符是否显示） | Boolean |    No    | iOS/Android |        Yes        |
|       **setValue()**       |            设置当前输入值            |         |    No    | iOS/Android |        Yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [BSD License](https://github.com/n4kz/react-native-material-textfield/blob/master/license.txt) ，请自由地享受和参与开源。