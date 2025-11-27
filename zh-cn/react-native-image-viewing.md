> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-viewing</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jobtoday/react-native-image-viewing/blob/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jobtoday/react-native-image-viewing/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-image-viewing)

请到三方库的 Releases 发布地址查看配套的版本信息：

| Version                        | Package Name                                  | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 0.2.2 | @react-native-oh-tpl/react-native-image-viewing | [Github](https://github.com/react-native-oh-library/react-native-image-viewing) | [Github Releases](https://github.com/react-native-oh-library/react-native-image-viewing/releases) | 0.72 |
| 0.3.0                        | @react-native-ohos/react-native-image-viewing       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-image-viewing) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-viewing/releases) | 0.77 |

## 安装与使用

进入到工程目录并输入以下命令：



<!-- tabs:start -->

进入到工程目录并输入以下命令：

#### npm

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-image-viewing

# 0.77
npm install @react-native-ohos/react-native-image-viewing
```

#### yarn

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-image-viewing

# 0.77
yarn add @react-native-ohos/react-native-image-viewing
```

快速使用：

```js
import React, { useState } from "react";
import {
  Alert,
  Platform,
  SafeAreaView,
  StatusBar,
  StyleSheet,
  Text,
  View,
  Image, ScrollView, TouchableOpacity
} from "react-native";
import memoize from "lodash/memoize";
import get from "lodash/get";
import ImageViewing from "react-native-image-viewing";
import {ImageSource} from "react-native-image-viewing/dist/@types"

type Props = {
  images: string[];
  onPress: (index: number) => void;
  shift?: number;
};

const IMAGE_WIDTH = 120;
const IMAGE_HEIGH = 120;

const architecture = [
  {
    thumbnail: "https://img.zcool.cn/community/01d191576ccecb0000018c1b64e382.jpg@1280w_1l_2o_100sh.jpg",
    original: "https://img.zcool.cn/community/01d191576ccecb0000018c1b64e382.jpg@1280w_1l_2o_100sh.jpg",
  },
  {
    thumbnail: "https://p0.ssl.qhimgs1.com/sdr/400__/t0461b1cfd7e4ef2b66.jpg",
    original: "https://p0.ssl.qhimgs1.com/sdr/400__/t0461b1cfd7e4ef2b66.jpg",
  },
  {
    thumbnail: "https://p0.ssl.qhimgs1.com/sdr/400__/t017c44dc545b663cce.jpg",
    original: "https://p0.ssl.qhimgs1.com/sdr/400__/t017c44dc545b663cce.jpg",
  }
];


const ImageList = ({ images, shift = 0, onPress }: Props) => (
  <ScrollView
    horizontal
    style={styles1.root}
    contentOffset={{ x: shift * IMAGE_WIDTH, y: 0 }}
    contentContainerStyle={styles1.container}
  >
    {images.map((imageUrl, index) => (
      <TouchableOpacity
        style={styles1.button}
        key={`${imageUrl}_${index}`}
        activeOpacity={0.8}
        onPress={() => onPress(index)}
      >
        {
          typeof imageUrl === 'string' ? <Image source={{ uri: imageUrl }} key={`${index}`} style={styles1.image} /> : <Image source={ imageUrl } key={`${index}`} doubleTapToZoomEnabled={true} style={styles1.image} />
        }
      </TouchableOpacity>
    ))}
  </ScrollView>
);

const styles1 = StyleSheet.create({
  root: { flexGrow: 0 },
  container: {
    flex: 0,
    paddingLeft: 10,
    marginBottom: 10
  },
  button: {
    marginRight: 10
  },
  image: {
    width: IMAGE_WIDTH,
    height: IMAGE_HEIGH,
    borderRadius: 10
  }
});

function App() {
  const [currentImageIndex, setImageIndex] = useState(0);
  const [images, setImages] = useState(architecture);
  const [isVisible, setIsVisible] = useState(false);

  const onSelect = (images, index) => {
    setImageIndex(index);
    setImages(images);
    setIsVisible(true);
  };

  const onRequestClose = () => setIsVisible(false);


  const getImageSource = memoize((images): ImageSource[] =>
    images.map((image) =>
      typeof image.original === "number"
        ? image.original
        : { uri: image.original as string }
    )
  );

  return (
    <SafeAreaView style={styles.root}>
      <ImageList
        images={architecture.map((image) => image.thumbnail)}
        onPress={(index) => onSelect(architecture, index)}
        shift={0.75}
      />
      <ImageViewing
        images={getImageSource(images)}
        imageIndex={currentImageIndex}
        visible={isVisible}
        onRequestClose={onRequestClose}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  root: {
    flex: 1,
    backgroundColor: "#000",
    ...Platform.select({
      android: { paddingTop: StatusBar.currentHeight },
      default: null,
    }),
  },
  about: {
    flex: 1,
    marginTop: -12,
    alignItems: "center",
    justifyContent: "center",
  },
  name: {
    textAlign: "center",
    fontSize: 24,
    fontWeight: "200",
    color: "#FFFFFFEE",
  },
});

```

## 约束与限制

### 兼容性

在以下版本验证通过：

1. RNOH:0.72.28; SDK:HarmonyOS NEXT DB2; IDE:DevEco Studio 5.0.3.500; ROM:3.0.0.28;
2. RNOH: 0.77.1;SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;

## 属性

> [!TIP]  "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                   | Description                                                  | Type                                                        | Platform | Required | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | ----------------------------------------------------------- | -------- | -------- | ----------------- |
| images                 | 图片数组用于显示                                   | ImageSource[]                                               | All      | Yes      | Yes               |
| keyExtractor           | 唯一标识每张图片                               | (imageSrc: ImageSource, index: number) => string            | All      | No       | Yes               |
| imageIndex             | 当前显示图片的索引                            | number                                                      | All      | Yes      | Yes               |
| visible                | 控制模态框是否显示                                        | boolean                                                     | All      | No       | Yes               |
| onRequestClose         | 关闭模态框时调用的函数                           | function                                                    | All      | Yes      | Yes               |
| onImageIndexChange     | 图片索引改变时调用的函数            | function                                                    | All      | No       | Yes               |
| onLongPress            | 长按图片时调用的函数                      | function (event: GestureResponderEvent, image: ImageSource) | All      | No       | Yes               |
| delayLongPress         | 长按触发前的延迟时间(毫秒)           | number                                                      | All      | No       | Yes               |
| animationType          | 模态框显示动画类型                      | none, fade, slide                                           | All      | No       | Yes               |
| presentationStyle      | 模态框展示样式: 默认为全屏，Android可使用overFullScreen隐藏状态栏 | fullScreen, pageSheet, formSheet, overFullScreen            | All      | No       | Partially (Support "fullScreen", "overFullScreen") |
| backgroundColor        | 模态框背景颜色(HEX格式)                         | string                                                      | All      | No       | Yes               |
| swipeToCloseEnabled    | 是否允许上下滑动关闭模态框                   | boolean                                                     | All      | No       | Yes               |
| doubleTapToZoomEnabled | 是否允许双击放大图片                      | boolean                                                     | All      | No       | Yes               |
| HeaderComponent        | 头部组件，接收当前图片索引作为参数          | component, function                                         | All      | No       | Yes               |
| FooterComponent        | 底部组件，接收当前图片索引作为参数          | component, function                                         | All      | No       | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/jobtoday/react-native-image-viewing/blob/master/LICENSE) ，请自由地享受和参与开源。
