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

> [!Tip] [Github 地址](https://github.com/shahnawaz/react-native-barcode-mask)

## 安装与使用

进入到工程目录并输入以下命令：

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

### 示例

下面的代码展示了这个库与相机组件结合的使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

  // BarcodeMask 测量完成后的回调函数
  const handleLayoutMeasured = ({ nativeEvent }) => {
    if (!layoutInfo) {
      setLayoutInfo(nativeEvent.layout);
    }
  };

  if (!device) {
    return <View style={styles.container}><Text style={styles.infoText}>未找到相机设备</Text></View>;
  }

  if (!hasPermission) {
    return null; 
  }

  return (
    <View style={styles.container}>
      {/* 动态定位的相机裁剪窗口 */}
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

      {/* 扫码框遮罩 */}
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

// 样式表
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

提示：需配置平台相机权限；确保遮罩层在上方；如需仅显示框内相机画面，可用 onLayoutMeasured 返回坐标裁剪 Camera 容器。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

本文档内容基于以下版本验证通过：

react-native-harmony：0.72.86; SDK：HarmonyOS 5.1.0.125; IDE：DevEco Studio 5.1.0.849; ROM：5.0.0.150;

react-native-harmony：0.77.18; SDK：HarmonyOS 5.1.0.125; IDE：DevEco Studio 5.1.0.849; ROM：5.0.0.150;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 尺寸属性

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `width` | 取景器的宽度（可见区域）。默认值：280 | number/string | No | All | yes |
| `height` | 取景器的高度（可见区域）。默认值：230 | number/string | No | All | yes |
| `edgeWidth` | 边/角的宽度。默认值：20 | number/string | No | All | yes |
| `edgeHeight` | 边/角的高度。默认值：20 | number/string | No | All | yes |

### 样式属性

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `edgeColor` | 用于为边缘设置自定义颜色。默认值：#FFF | string | No | All | yes |
| `edgeBorderWidth` | 用于修改边缘的边框（厚度）。默认值：4 | number/string | No | All | yes |
| `edgeRadius` | 用于修改边缘的边框圆角。默认值：0 | number | No | All | yes |
| `backgroundColor` | 用于修改取景器周围区域的背景颜色。默认值：rgb(0, 0, 0, 0.6) | string | No | All | yes |
| `outerMaskOpacity` | 用于修改外部遮罩的透明度。默认值：0.6 | number | No | All | yes |

### 动画属性

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `showAnimatedLine` | 是否显示动画扫描线。默认值：true | boolean | No | All | yes |
| `animatedLineColor` | 动画扫描线的颜色。默认值：#FFF | string | No | All | yes |
| `animatedLineHeight` | 动画扫描线的高度。默认值：2 | number | No | All | yes |
| `animatedLineWidth` | 动画扫描线的宽度。默认值：85% | number/string | No | All | yes |
| `lineAnimationDuration` | 扫描线动画的持续时间（毫秒）。默认值：1500 | number | No | All | yes |
| `animatedLineOrientation` | 扫描线动画的方向（水平/垂直）。默认值：horizontal | string | No | All | yes |
| `useNativeDriver` | 是否为动画使用原生驱动。默认值：true | boolean | No | All | yes |

### 回调函数

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `onLayoutMeasured` | 用于接收取景器 onLayout 事件的处理程序。 | function | No | All | yes |



## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/shahnawaz/react-native-barcode-mask/blob/master/LICENSE) ，请自由地享受和参与开源。