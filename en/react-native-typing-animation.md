> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-typing-animation</code> </h1>
</p>

> [!TIP] [GitHub address](https://github.com/watadarkstar/react-native-typing-animation)

Please check the corresponding version information in the Releases section of the third-party library's repository:

| Third-Party Library Version | Supported RN Version |
| ----------------------------| -------------------- |
| 0.1.7                      |  0.72/0.77 |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

## Installation and Usage

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

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

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

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|     Name     |                         Description                          |  Type   | Required |  Platform   | HarmonyOS Support |
| :----------: | :----------------------------------------------------------: | :-----: | :------: | :---------: | :---------------: |
|    style     |              Container styles; default is `{}`               | Object  |    No    | Android/ios |        Yes        |
|   dotColor   |             Dot color; default is `#000` (black)             | String  |    No    | Android/ios |        Yes        |
|  dotStyles   |                 Dot styles; default is `{}`                  | Object  |    No    |   Android   |        No         |
|  dotRadius   |                 Dot radius; default is `2.5`                 | Integer |    No    | Android/ios |        Yes        |
|  dotMargin   |      Dot margin, the space between dots; default is `3`      | Integer |    No    | Android/ios |        Yes        |
| dotAmplitude |                Dot amplitude; default is `3`                 | Integer |    No    | Android/ios |        Yes        |
|   dotSpeed   | Dot speed, the speed of the whole animation view; default is `0.15` | Integer |    No    | Android/ios |        Yes        |
|     dotY     |        Dot y, the starting y coordinate; default is 6        | Integer |    No    | Android/ios |        Yes        |
|     dotX     |  Dot x, the x coordinate of the center dot; default is `12`  | Integer |    No    | Android/ios |        Yes        |

## Known Issues

## Others

## License

This project is licensed under  [The MIT License (MIT)](https://github.com/watadarkstar/react-native-typing-animation/blob/master/LICENSE).

