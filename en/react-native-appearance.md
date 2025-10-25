> Template Version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-appearance</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/expo/react-native-appearance">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/expo/react-native-appearance/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [Github Address](https://github.com/react-native-oh-library/react-native-appearance)

## Installation and Usage

Navigate to your project directory and enter the following command:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-appearance
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-appearance
```

<!-- tabs:end -->

### Example

The following code demonstrates how to use this color picker component in a page:

> [!WARNING] The library name in the import statement remains unchanged.

```tsx
import React, { useState } from "react";
import { Button, View, Text, StyleSheet, useColorScheme } from 'react-native';
import { Tester, TestSuite, TestCase } from '@rnoh/testerino';
import { AppearanceHarmony } from 'react-native-appearance';

const AppearanceExample = () => {
  const scheme = useColorScheme();
  const currentScheme = scheme ?? scheme!.toString();

  const [listenedScheme, setListenedScheme] = useState('');
  AppearanceHarmony.addChangeListener(({ colorScheme }) => {
    setListenedScheme(colorScheme ?? colorScheme!.toString());
  });

  const [gotScheme, setGotScheme] = useState('');
  const getAppearance = ()=> {
    const result = AppearanceHarmony.getColorScheme();
    setGotScheme(result ?? result!.toString());
  }

  const changeAppearance = ()=> {
    const result = AppearanceHarmony.getColorScheme();
    if (result == 'dark') {
      AppearanceHarmony.setColorScheme('light');
    } else if (result == 'light') {
      AppearanceHarmony.setColorScheme('dark');
    }
  }

  const styles = StyleSheet.create({
    container: {
      padding: 50,
      width: '100%',
      height: '100%',
      backgroundColor: currentScheme == 'dark' ? 'lightgray': 'white'
    },
    row: {
      paddingTop: 30
    }
  });

  return (
    <Tester style={{ paddingBottom: 80 }}>
      <TestSuite name='Appearance'>
        <TestCase itShould='Display Mode'>
          <View style={styles.container}>
            <Text style={styles.row}>Current display mode:{currentScheme}</Text>
            <Text style={styles.row}>Listening display mode:{listenedScheme}</Text>
            <Text style={styles.row}>Acquired display mode:{gotScheme}</Text>
            <View style={styles.row}><Button title="Get display mode" onPress={()=>getAppearance()} /></View>
            <View style={styles.row}><Button title="Change display mode" onPress={()=>changeAppearance()} /></View>
          </View>
        </TestCase>
      </TestSuite>
    </Tester>
  );
}
```

## Constraints

### Compatibility

To use this library, you need to use the correct versions of React-Native and RNOH. Additionally, you need to use the corresponding versions of DevEco Studio and the phone's ROM.

The content of this document has been verified with the following versions:

react-native-harmony: 0.72.86; SDK: HarmonyOS 5.1.0.125; IDE: DevEco Studio 5.1.0.849; ROM: 5.0.0.150;

react-native-harmony: 0.77.18; SDK: HarmonyOS 5.1.0.125; IDE: DevEco Studio 5.1.0.849; ROM: 5.0.0.150;

## Properties

> [!TIP] The "Platform" column indicates the platforms supported by the original third-party library.

> [!TIP] In the "HarmonyOS Support" column, "yes" means the property is supported on the HarmonyOS platform; "no" means it is not supported; "partially" means it is partially supported. The usage is consistent across platforms, and the effect is aligned with that on iOS or Android.

### Functions

| Name | Description                                                                                             | Type | Required | Platform | HarmonyOS Support |
| :--- |:--------------------------------------------------------------------------------------------------------| :--- | :--- | :--- | :--- |
| `useColorScheme` | Gets the current display mode. Returns a ColorSchemeName object.                                        | `function` | No | All | yes |
| `getColorScheme` | Gets the current display mode. Returns a ColorSchemeName object.                                        | `function` | No | All | yes |
| `setColorScheme` | Set display mode.                                                                                       | `function` | No | All | yes |
| `addChangeListener`| Listen for system display mode changes. Returns a ColorSchemeName object.                               | `function` | No | All | yes |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/instea/react-native-color-picker/blob/master/LICENSE).


