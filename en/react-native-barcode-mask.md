> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-barcode-mask</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/shahnawaz/react-native-barcode-mask">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/shahnawaz/react-native-barcode-mask/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [GitHub address](https://github.com/shahnawaz/react-native-barcode-mask)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-barcode-mask
```

#### **yarn**

```bash
yarn add react-native-barcode-mask
```

<!-- tabs:end -->

### Example

The following code demonstrates a use case of this library in combination with a camera component:

> [!WARNING] The import name of the library remains the same when in use.

```javascript
import React, { useState, useEffect } from 'react';
import { StyleSheet, View, Text } from 'react-native';
import BarcodeMask from 'react-native-barcode-mask';
import { Camera, useCameraDevice, useCameraPermission } from 'react-native-vision-camera';

export default function SimplifiedScannerDemo() {
  const [layoutInfo, setLayoutInfo] = useState(null);

  // Vision Camera Hooks
  const device = useCameraDevice('back');
  const { hasPermission, requestPermission } = useCameraPermission();

  useEffect(() => {
    if (!hasPermission) {
      requestPermission();
    }
  }, [hasPermission, requestPermission]);

  // Callback function after BarcodeMask finishes measuring its layout
  const handleLayoutMeasured = ({ nativeEvent }) => {
    if (!layoutInfo) {
      setLayoutInfo(nativeEvent.layout);
    }
  };

  if (!device) {
    return <View style={styles.container}><Text style={styles.infoText}>No camera device found</Text></View>;
  }

  if (!hasPermission) {
    return null; 
  }

  return (
    <View style={styles.container}>
      {/* Dynamically positioned camera clipping window */}
      {layoutInfo && (
        <View
          style={[
            styles.cameraClip,
            {
              left: layoutInfo.x - 12,
              top: layoutInfo.y - 12,
              width: layoutInfo.width + 24,
              height: layoutInfo.height + 24,
            },
          ]}
        >
          <Camera
            style={StyleSheet.absoluteFill}
            device={device}
            isActive={true}
          />
        </View>
      )}

      {/* Barcode scanner mask overlay */}
      <BarcodeMask
        width={250}
        height={200}
        onLayoutMeasured={handleLayoutMeasured}
        showAnimatedLine={true}
        lineAnimationDuration={1000}
      />
    </View>
  );
}

// Stylesheet
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: 'black',
  },
  infoText: {
    color: 'white',
    fontSize: 16,
    textAlign: 'center',
  },
  cameraClip: {
    position: 'absolute',
    overflow: 'hidden',
  },
});
```

Hint: Platform camera permissions need to be configured; ensure the mask layer is on top; if you need to display the camera view only within the frame, you can use the coordinates returned by onLayoutMeasured to clip the Camera container.

## Constraints

## Compatibility

This document is verified based on the following versions:

react-native-harmony：0.72.86; SDK：HarmonyOS 5.1.0.125; IDE：DevEco Studio 5.1.0.849; ROM：5.0.0.150;

react-native-harmony：0.77.18; SDK：HarmonyOS 5.1.0.125; IDE：DevEco Studio 5.1.0.849; ROM：5.0.0.150;

## Props

> [!TIP] The "Platform" column indicates the platforms supported by the original third-party library.

> [!TIP] In the "HarmonyOS Support" column, `yes` means the prop is supported on the HarmonyOS platform, `no` means it is not supported, and `partially` means it is partially supported. The usage is consistent across platforms, with the effect aiming to match the iOS or Android implementation.

### Dimension Props

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `width` | Finder's width (the visible area). Default: 280 | number/string | No | All | yes |
| `height` | Finder's height (the visible area). Default: 230 | number/string | No | All | yes |
| `edgeWidth` | Edge/Corner's width. Default: 20 | number/string | No | All | yes |
| `edgeHeight` | Edge/Corner's height. Default: 20 | number/string | No | All | yes |

### Style Props

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `edgeColor` | Use this to give custom color to edges. Default: #FFF | string | No | All | yes |
| `edgeBorderWidth` | Use this to modify the border (thickness) of edges. Default: 4 | number/string | No | All | yes |
| `edgeRadius` | Use this to modify the border radius of edges. Default: 0 | number | No | All | yes |
| `backgroundColor` | Use this to modify the background color of area around finder. Default: rgb(0, 0, 0, 0.6) | string | No | All | yes |
| `outerMaskOpacity` | Use this to modify the transparency of outer mask. Default: 0.6 | number | No | All | yes |

### Animation Props

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `showAnimatedLine` | Whether to show animated scanning line. Default: true | boolean | No | All | yes |
| `animatedLineColor` | Color of the animated scanning line. Default: #FFF | string | No | All | yes |
| `animatedLineHeight` | Height of the animated scanning line. Default: 2 | number | No | All | yes |
| `animatedLineWidth` | Width of the animated scanning line. Default: 85% | number/string | No | All | yes |
| `lineAnimationDuration` | Duration of the scanning line animation in milliseconds. Default: 1500 | number | No | All | yes |
| `animatedLineOrientation` | Orientation of the scanning line animation (horizontal/vertical). Default: horizontal | string | No | All | yes |
| `useNativeDriver` | Whether to use native driver for animations. Default: true | boolean | No | All | yes |

### Callback Props

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `onLayoutMeasured` | Handler to receive onLayout event of finder. Useful if you want to only detect barcode inside the Finder area | function | No | All | yes |



## Known Issues

## Others

## License
This project is licensed under [The MIT License (MIT)](https://github.com/shahnawaz/react-native-barcode-mask/blob/master/LICENSE).