> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-typing-animation</code> </h1>
</p>

> [!TIP] [GitHub address](https://github.com/watadarkstar/react-native-typing-animation)

请到三方库的 Releases发布地址查看配套的版本信息：

| 三方库版本 | 支持RN版本 |
| ----------| ---------- |
| 0.1.7    |  0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-typing-animation@0.1.7
```

#### **yarn**

```bash
yarn add react-native-typing-animation@0.1.7
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import React, { useEffect, useRef, useState } from 'react';
import {
  Animated,
  View,
  Text,
  PanResponder,
  Button,
  StyleSheet,
  TouchableHighlight,
  Alert,
  TouchableOpacity,
  ScrollView,
} from 'react-native';
import { TestSuite, Tester, TestCase } from '@rnoh/testerino';
import { TypingAnimation } from 'react-native-typing-animation';

const TypingAnimationDemos = () => {
  const typingAnimationProps = [
    {
      key: 'dotColor',
      value: {
        dotColor: 'green'
      }
    },
    {
      key: 'dotColor',
      value: {
        dotColor: 'red'
      }
    },
    {
      key: 'dotRadius',
      value: {
        dotRadius: 5
      }
    },
    {
      key: 'dotRadius',
      value: {
        dotRadius: 10
      }
    },
    {
      key: 'dotMargin',
      value: {
        dotMargin: 10
      }
    },
    {
      key: 'dotMargin',
      value: {
        dotMargin: 15
      }
    },
    {
      key: 'dotAmplitude',
      value: {
        dotAmplitude: 1
      }
    },
    {
      key: 'dotAmplitude',
      value: {
        dotAmplitude: 1
      }
    },
    {
      key: 'dotSpeed',
      value: {
        dotSpeed: 10
      }
    },
    {
      key: 'dotSpeed',
      value: {
        dotSpeed: 0.5
      }
    },
    {
      key: 'dotY',
      value: {
        dotY: 30
      }
    },
    {
      key: 'dotY',
      value: {
        dotY: 20
      }
    },
    {
      key: 'dotX',
      value: {
        dotX: 12
      }
    },
    {
      key: 'dotX',
      value: {
        dotX: 15
      },
    },
  ];
  return (
    <ScrollView>
      <Tester>
        {typingAnimationProps.map((item) => {
          return (

            <TestCase itShould={item.key} tags={['C_API']}>
              <View
                style={{
                  height: 30,
                  display: 'flex',
                  flexDirection: 'row',
                  justifyContent: 'center',
                }}>
                <TypingAnimation
                  {...item.value}
                ></TypingAnimation>
              </View>
            </TestCase>
          );
        })}
      </Tester>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: 'white',
  },
  button: {
    backgroundColor: 'blue',
    paddingHorizontal: 20,
    paddingVertical: 10,
    borderRadius: 5,
    marginBottom: 20,
  },
  buttonText: {
    color: 'white',
    fontSize: 16,
  },
  animationContainer: {
    alignItems: 'center',
  },
  text: {
    fontSize: 20,
    marginBottom: 20,
  },
  typingAnimation: {
    flexDirection: 'row',
  },
});

export default TypingAnimationDemos;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|     Name     |                         Description                          |  Type   | Required |  Platform   | HarmonyOS Support |
| :----------: | :----------------------------------------------------------: | :-----: | :------: | :---------: | :---------------: |
|    style     |              容器样式；默认值为`{}`               | Object  |    No    | Android/ios |        Yes        |
|   dotColor   |             点颜色；默认值为`#000`（黑色）             | String  |    No    | Android/ios |        Yes        |
|  dotStyles   |                 点样式；默认值为`{}`                  | Object  |    No    |   Android   |        No         |
|  dotRadius   |                 点半径；默认值为`2.5`                 | Integer |    No    | Android/ios |        Yes        |
|  dotMargin   |      点边距，点之间的间距；默认值为`3`      | Integer |    No    | Android/ios |        Yes        |
| dotAmplitude |                点振幅；默认值为`3`                 | Integer |    No    | Android/ios |        Yes        |
|   dotSpeed   | 点速度，整个动画视图的速度；默认值为`0.15` | Integer |    No    | Android/ios |        Yes        |
|     dotY     |        点y坐标，起始y坐标；默认值为6        | Integer |    No    | Android/ios |        Yes        |
|     dotX     |  点x坐标，中心点的x坐标；默认值为`12`  | Integer |    No    | Android/ios |        Yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于  [The MIT License (MIT)](https://github.com/watadarkstar/react-native-typing-animation/blob/master/LICENSE) ，请自由地享受和参与开源。

