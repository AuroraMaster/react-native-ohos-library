> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>text-shadow-component</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/bswnth48/text-shadow-react-native">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bswnth48/text-shadow-react-native/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/bswnth48/text-shadow-react-native)

> [!TIP] Renders text shadow only on RNOH 0.77+; RNOH 0.72 is not supported.

## Installation and Usage

<!-- tabs:start -->

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install --save text-shadow-component@1.0.7
```

#### **yarn**

```bash
yarn add text-shadow-component@1.0.7
```

<!-- tabs:end -->

The following code shows the basic usage of this library:

```js
import React from 'react';
import { View, ScrollView } from 'react-native';
import { TextShadow } from 'text-shadow-component';

export default function App() {
  const cases = [
    {
      bg: '#232323',
      color: '#FFFFFF',
      textShadow: '0 0 5px #FFF, 0 0 12px #49FF18',
    },
    {
      bg: '#FFFFFF',
      color: '#202c2d',
      textShadow:
        '0 1px #808d93, -1px 0 #cdd2d5, -1px 2px #808d93, -2px 1px #cdd2d5',
    },
  ];

  return (
    <ScrollView>
      {cases.map((it, idx) => (
        <View
          key={idx}
          style={{
            height: 200,
            alignItems: 'center',
            justifyContent: 'center',
            backgroundColor: it.bg,
          }}
        >
          <TextShadow
            title="Preview"
            textShadow={it.textShadow}
            titleStyle={{ fontSize: 48, color: it.color }}
          />
        </View>
      ))}
    </ScrollView>
  );
}
```

## Constraints

### Compatibility

This document is verified with the following environment:

1. RNOH: 0.77.18; SDK: HarmonyOS 5.0.0 Release (API Version 12 Release); IDE: DevEco Studio 5.1.1.830; ROM: 5.0.0.150 SP8

> Note: On RNOH 0.77+, native text shadow drawing is implemented. Earlier versions (e.g., RNOH 0.72) will not render text shadow.

## Properties

> [!TIP] The Platform column indicates the platform where the properties are supported in the original third-party library.
>
> [!TIP] If the value of HarmonyOS Support is yes, it means the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage is the same across platforms and the effect targets iOS/Android parity.
>
> [!TIP] This document provides support conclusions for HarmonyOS (RNOH 0.77+) only.

| Name        | Description                                             | Type   | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| title       | The text content to display                             | string | yes      | Android/iOS | yes               |
| textShadow  | CSS-style text-shadow string (supports multiple layers) | string | yes      | Android/iOS | yes               |
| titleStyle  | Text style (such as fontSize, color, etc.)              | style  | no       | Android/iOS | yes               |

## Known Issues

Text shadow is not displayed on RNOH 0.72. [issue#ID0FUU](https://gitee.com/react-native-oh-library/usage-docs/issues/ID0FUU)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/bswnth48/text-shadow-react-native/blob/master/LICENSE).