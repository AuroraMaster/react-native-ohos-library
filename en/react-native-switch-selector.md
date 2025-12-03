> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-switch-selector</code> </h1>
</p>

> [!TIP] [GitHub address](https://github.com/App2Sales/react-native-switch-selector)

Please check the corresponding version information in the Releases section of the third-party library's repository:

| Third-Party Library Version | Supported RN Version |
| ----------------------------| -------------------- |
| 2.3.0                     |  0.72/0.77 |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-switch-selector@2.3.0
```

#### **yarn**

```bash
yarn add react-native-switch-selector@2.3.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```jsx
import SwitchSelector from "react-native-switch-selector";
import React from 'react';
import { ScrollView } from 'react-native';

const SwitchSelectorDemo = () => {
    const options = [
        { label: "movie", value: "movie" },
        { label: "map", value: "map" },
        { label: "subway", value: "metro" }
    ];
    return (
        <ScrollView>
            <SwitchSelector
                options={options}
                initial={0}
            />
        </ScrollView>
    )
}

export default SwitchSelectorDemo;
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

| Name                         | Description                                                  | Type                     | Required | Platform    | HarmonyOS Support |
| ---------------------------- | ------------------------------------------------------------ | ------------------------ | -------- | ----------- | ----------------- |
| options                      | Items array to  render. Each item has a label and a value and optionals icons | array                    | Yes      | Android/IOS | Yes               |
| options[].label              | Label from  each item                                        | string                   | Yes      | Android/IOS | Yes               |
| options[].value              | Value  from each item                                        | string                   | Yes      | Android/IOS | Yes               |
| options[].customIcon         | Optional  custom icon from each item                         | Jsx  element ou Function | No       | Android/IOS | Yes               |
| options[].imageIcon          | Source  from a image icon form each item. Has the same color then label in render | string                   | No       | Android/IOS | Yes               |
| options[].activeColor        | Color  from each item when is selected                       | string                   | No       | Android/IOS | Yes               |
| options[].testID             | Test ID for each item used for testing (e.g. with Appium)    | string                   | No       | Android/IOS | Yes               |
| options[].accessibilityLabel | Accessibility Label for each item used for testing (e.g. with Appium) | string                   | No       | Android/IOS | Yes               |
| initial                      | Item  selected in initial render                             | number                   | No       | Android/IOS | Yes               |
| value                        | The  switch value (will call onPress)                        | number                   | No       | Android/IOS | Yes               |
| onPress                      | Callback  function called after change value.                | function                 | Yes      | Android/IOS | Yes               |
| disableValueChangeOnPress    | Disables  the onPress call when the value is manually changed | bool                     | No       | Android/IOS | Yes               |
| fontSize                     | Font  size from labels. If null default fontSize of the app is used. | number                   | No       | Android/IOS | Yes               |
| selectedColor                | Color  text of the item selected                             | string                   | No       | Android/IOS | Yes               |
| buttonMargin                 | Margin  of the item selected to component                    | number                   | No       | Android/IOS | Yes               |
| buttonColor                  | Color  bg of the item selected                               | string                   | No       | Android/IOS | Yes               |
| textColor                    | Color  text of the not selecteds items                       | string                   | No       | Android/IOS | Yes               |
| backgroundColor              | Color  bg of the component                                   | string                   | No       | Android/IOS | Yes               |
| borderColor                  | Border  Color of the component                               | string                   | No       | Android/IOS | Yes               |
| borderRadius                 | Border  Radius of the component                              | number                   | No       | Android/IOS | Yes               |
| hasPadding                   | Indicate  if item has padding                                | bool                     | No       | Android/IOS | Yes               |
| animationDuration            | Duration  of the animation                                   | number                   | No       | Android/IOS | Yes               |
| valuePadding                 | Size  of padding                                             | number                   | No       | Android/IOS | Yes               |
| height                       | Height  of component                                         | number                   | No       | Android/IOS | Yes               |
| bold                         | Indicate  if text has fontWeight bold                        | bool                     | No       | Android/IOS | Yes               |
| textStyle                    | Text  style                                                  | object                   | No       | Android/IOS | Yes               |
| selectedTextStyle            | Selected  text style                                         | object                   | No       | Android/IOS | Yes               |
| textContainerStyle           | Style  for text (and icon) container (TouchableOpacity)      | object                   | No       | Android/IOS | Yes               |
| selectedTextContainerStyle   | Style  for selected text (and icon) container (TouchableOpacity) | object                   | No       | Android/IOS | Yes               |
| imageStyle                   | Image  style                                                 | object                   | No       | Android/IOS | Yes               |
| style                        | Container  style                                             | object                   | No       | Android/IOS | Yes               |
| returnObject                 | Indicate  if onPress function return an option instead of option.value | bool                     | No       | Android/IOS | Yes               |
| disabled                     | Disables  the switch                                         | bool                     | No       | Android/IOS | Yes               |
| borderWidth                  | Define  border width                                         | number                   | No       | Android/IOS | Yes               |
| testID                       | Test ID used for testing (e.g. with Appium)                  | string                   | No       | Android/IOS | Yes               |
| accessibilityLabel           | Accessibility Label used for testing (e.g. with Appium)      | string                   | No       | Android/IOS | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/App2Sales/react-native-switch-selector/blob/master/LICENSE)，请自由地享受和参与开源。