> Template Version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-color-picker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/instea/react-native-color-picker">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/instea/react-native-color-picker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [Github Address](https://github.com/instea/react-native-color-picker)

## Installation and Usage

Navigate to your project directory and enter the following command:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-color-picker@0.6.0
```

#### **yarn**

```bash
yarn add react-native-color-picker@0.6.0
```

<!-- tabs:end -->

### Example

The following code demonstrates how to use this color picker component in a page:

> [!WARNING] The library name in the import statement remains unchanged.

```javascript
import React from 'react'
import { View, Text, Alert } from 'react-native'
import { TriangleColorPicker, toHsv } from 'react-native-color-picker'

export default class App extends React.Component {

  constructor(...args) {
    super(...args)
    this.state = { color: toHsv('green') }
    this.onColorChange = this.onColorChange.bind(this)
  }

  onColorChange(color) {
    this.setState({ color })
  }

  render() {
    return (
      <View style={{flex: 1, padding: 45, backgroundColor: '#212021'}}>
        <Text style={{color: 'white'}}>React Native Color Picker - Controlled</Text>
        <TriangleColorPicker
          oldColor='purple'
          color={this.state.color}
          onColorChange={this.onColorChange}
          onColorSelected={color => Alert.alert(`Color selected: ${color}`)}
          onOldColorSelected={color => Alert.alert(`Old color selected: ${color}`)}
          style={{flex: 1}}
        />
      </View>
    )
  }

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

### ColorPicker Properties

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `color` | A controlled property used to set the current color of the picker. | `String` \| `HSV` | No | All | yes |
| `defaultColor` | An uncontrolled property used to set the initial color of the picker. | `String` \| `HSV` | No | All | yes |
| `oldColor` | An old color for visual comparison. If provided, the center of the picker will be split to show both the new and old colors. | `String` | No | All | yes |
| `style` | Styles applied to the root container of the picker. | `Style` | No | All | yes |
| `hideSliders` | **(ColorPicker only)** Whether to hide the saturation and value sliders. Default: false | `boolean` | No | All | yes |
| `sliderComponent`| **(ColorPicker only)** Pass in a custom slider component. | `React.Component` | No | All | yes |

### TriangleColorPicker Properties

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `color` | A controlled property used to set the current color of the picker. | `String` \| `HSV` | No | All | yes |
| `defaultColor` | An uncontrolled property used to set the initial color of the picker. | `String` \| `HSV` | No | All | yes |
| `oldColor` | An old color for visual comparison. If provided, the center of the picker will be split to show both the new and old colors. | `String` | No | All | yes |
| `style` | Styles applied to the root container of the picker. | `Style` | No | All | yes |
| `hideControls` | **(TrianglePicker only)** Whether to hide the color preview and confirmation button at the bottom. Default: false | `boolean` | No | All | yes |

### Callback Functions

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `onColorChange` | A callback triggered whenever the color changes. Returns the color as an HSV object. | `(color: HSV) => void` | No | All | yes |
| `onColorSelected`| A callback triggered when the user confirms a color selection (e.g., by tapping the center of the picker). Returns the color as a hex string. | `(color: string) => void` | No | All | yes |
| `onOldColorSelected` | A callback triggered when the user taps the old color preview area. Returns the old color as a hex string. | `(color: string) => void` | No | All | yes |

### Utility Functions

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `toHsv` | Converts a color string (e.g., `'blue'`, `'#ff0000'`) to an HSV object. | `(color: string) => HSV` | No | All | yes |
| `fromHsv`| Converts an HSV object to a hex color string. | `(hsv: HSV) => string` | No | All | yes |

## Known Issues

## Others

**HSV Object Format**:
```javascript
{
  h: number, // Hue: 0-360
  s: number, // Saturation: 0-1
  v: number, // Value: 0-1
}
```

## License

This project is licensed under [The MIT License (MIT)](https://github.com/instea/react-native-color-picker/blob/master/LICENSE).