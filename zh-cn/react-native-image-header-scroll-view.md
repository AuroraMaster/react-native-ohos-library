> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-header-scroll-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/bamlab/react-native-image-header-scroll-view">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bamlab/react-native-image-header-scroll-view/blob/master/LICENCE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/bamlab/react-native-image-header-scroll-view)

请到三方库的 Releases 发布地址查看配套的版本信息：

| Version                        | Package Name                                  | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 0.10.3 | @react-native-oh-tpl/react-native-image-header-scroll-view | [Github](https://github.com/react-native-oh-library/react-native-image-header-scroll-view) | [Github Releases](https://github.com/react-native-oh-library/react-native-image-header-scroll-view/releases) | 0.72 |
| 1.1.0                        | @react-native-ohos/react-native-image-header-scroll-view     | [Github](https://github.com/bamlab/react-native-image-header-scroll-view) | [Github Releases](https://github.com/bamlab/react-native-image-header-scroll-view/releases) | 0.77 |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-image-header-scroll-view

# 0.77
npm install @react-native-ohos/react-native-image-header-scroll-view
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-image-header-scroll-view

# 0.77
yarn add @react-native-ohos/react-native-image-header-scroll-view
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useEffect, useState } from 'react';
import { StyleSheet, Text, View, Image,Animated,StatusBar, Dimensions ,Easing} from 'react-native';
import ImageHeaderScrollView ,{TriggeringView}  from 'react-native-image-header-scroll-view';
const MIN_HEIGHT = 80;
const MAX_HEIGHT = 250;
const tvShowContent = {
  title: 'Doctor Who',
  overview: `
    The Doctor looks and seems human. He's handsome, witty, and could be mistaken for just another man in the street.

    But he is a Time Lord: a 900 year old alien with 2 hearts, part of a gifted civilization who mastered time travel.

    The Doctor saves planets for a living – more of a hobby actually, and he's very, very good at it.

    He's saved us from alien menaces and evil from before time began – but just who is he?`,
  year: 2005,
  genres: ['Action & Adventure', 'Drama', 'Sci-Fi & Fantasy'],
  keywords: [
    'time travel',
    'time machine',
    'phone booth',
    'alien',
    'time traveler',
    'police box',
    'space and aliens',
  ],
};

const styles = StyleSheet.create({
  image: {
    height: MAX_HEIGHT,
    width: Dimensions.get('window').width,
    alignSelf: 'stretch',
    resizeMode: 'cover',
  },
  title: {
    fontSize: 20,
  },
  name: {
    fontWeight: 'bold',
  },
  section: {
    padding: 20,
    borderBottomWidth: 1,
    borderBottomColor: '#cccccc',
    backgroundColor: 'white',
  },
  sectionTitle: {
    fontSize: 18,
    fontWeight: 'bold',
  },
  sectionContent: {
    fontSize: 16,
    textAlign: 'justify',
  },
  keywords: {
    flexDirection: 'row',
    justifyContent: 'flex-start',
    alignItems: 'flex-start',
    flexWrap: 'wrap',
  },
  keywordContainer: {
    backgroundColor: '#999999',
    borderRadius: 10,
    margin: 10,
    padding: 10,
  },
  keyword: {
    fontSize: 16,
    color: 'white',
  },
  titleContainer: {
    flex: 1,
    alignSelf: 'stretch',
    justifyContent: 'center',
    alignItems: 'center',
  },
  imageTitle: {
    color: 'white',
    backgroundColor: 'transparent',
    fontSize: 24,
  },
  navTitleView: {
    height: MIN_HEIGHT,
    justifyContent: 'center',
    alignItems: 'center',
    paddingTop: 16,
    opacity: 0,
  },
  navTitle: {
    color: 'white',
    fontSize: 18,
    backgroundColor: 'transparent',
  },
  sectionLarge: {
    height: 600,
  },
});

function HeaderImageExample () {
    const [visible, setVisible] = useState(false);
    const fadeAnim = new Animated.Value(0);
    useEffect(() => {
        if (visible) {
          Animated.timing(fadeAnim, {
            toValue: 1,
            duration: 100,
            easing: Easing.bounce,
            useNativeDriver: true,
          }).start();
        } else {
          // 如果当前是不可见的，则执行淡出动画
          Animated.timing(fadeAnim, {
            toValue: 0,
            duration: 100,
            easing: Easing.bounce,
            useNativeDriver: true,
          }).start();
        }
      }, [visible, fadeAnim]);  
 
    return (
      <View style={{ flex: 1 }}>
        <StatusBar barStyle="light-content" />
        <ImageHeaderScrollView
          maxHeight={MAX_HEIGHT} 
          minHeight={MIN_HEIGHT}  
          maxOverlayOpacity={0.8} 
          minOverlayOpacity={0.2}   
          fadeOutForeground={true} 
          foregroundParallaxRatio={1}
          overlayColor={'blue'} 
          renderHeader={() => <Image source={'请输入本地图片路径'} style={styles.image} />} 
          renderFixedForeground={() => (
            <Animated.View
                    style={[styles.navTitleView,{ opacity: fadeAnim}]}  >
                    <Text style={styles.navTitle}>
                        {tvShowContent.title}, ({tvShowContent.year})
                    </Text>
            </Animated.View>
          )} 
          renderForeground={() => (
            <View style={styles.titleContainer}>
              <Text style={styles.imageTitle}>{tvShowContent.title}</Text>
            </View> as any
          )}  
          useNativeDriver={true}
          disableHeaderGrow={false}>
         <>
          <TriggeringView
            onHide={() => setVisible(true)}
            onDisplay={() => setVisible(false)}
          >
            <Text style={styles.title}>
              <Text style={styles.name}>{tvShowContent.title}</Text>, ({tvShowContent.year})
            </Text>
          </TriggeringView>
          <View style={styles.section}>
            <Text style={styles.sectionTitle}>Overview</Text>
            <Text style={styles.sectionContent}>{tvShowContent.overview}</Text>
          </View>
          <View style={[styles.section, styles.sectionLarge]}>
            <Text style={styles.sectionTitle}>Keywords</Text>
            <View style={styles.keywords}>
              {tvShowContent.keywords.map(keyword => (
                <View style={styles.keywordContainer} key={keyword}>
                  <Text style={styles.keyword}>{keyword}</Text>
                </View>
              ))}
            </View>
          </View>
          </>
        </ImageHeaderScrollView>
      </View>
    );
  
}

export default HeaderImageExample;
```

## 约束与限制

### 兼容性

在以下版本验证通过：

1. RNOH:0.72.28; SDK:HarmonyOS NEXT DB2; IDE:DevEco Studio 5.0.3.500; ROM:3.0.0.28;
2. RNOH: 0.77.1;SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;

## 属性

> [!Tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!Tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### **Header**

| Name                          | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `renderHeader` | 返回用作头部的组件的函数。例如，它可以返回背景图片。           | function | No       | All      | Yes               |
| `headerImage`               | renderHeader={() => <Image source={this.props.headerImage} style={{ height: this.props.maxHeight, width: Dimensions.get('window').width }} 的快捷方式                         | Image source Props (object or number) | No       | All      | Yes               |
| `maxHeight`                | 头部的最大高度     | number | No       | All      | Yes               |
| `minHeight`                | 头部的最小高度（导航栏模式下）                           | number | No       | All      | Yes               |
| `minOverlayOpacity`           | 滚动前头部黑色覆盖层的不透明度 | number | No       | All      | Yes               |
| `maxOverlayOpacity`           | 导航栏模式下头部黑色覆盖层的不透明度 | number | No       | All      | Yes               |
| `overlayColor`           | 头部覆盖层的颜色 | string | No       | All      | Yes               |
| `useNativeDriver`           | 使用原生驱动程序来提高动画性能。如果 useNativeDriver=true，目前有几个属性不受支持（onScroll、ScrollComponent、renderTouchableFixedForeground） | boolean | No       | All      | Yes               |
| `headerContainerStyle`           | 可选样式，传递给头部组件容器 | Object | No       | All      | Yes               |
| `disableHeaderGrow`           | 禁用头部增长效果 | boolean | No       | All      | Yes              |


#### **Foreground**

| Name                          | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `renderForeground` | 返回用作前景的组件的函数。该组件在头部前面渲染，并随ScrollView一起滚动。例如，它可以返回一个标题。           | function | No       | All      | Yes               |
| `renderFixedForeground`               | 返回用作固定前景的组件的函数。该组件与头部一起显示，但不受覆盖层影响。                           | Image source Props (object or number) | No       | All      | Yes               |
| `foregroundExtrapolate`                | 可选属性，允许覆盖前景的外推模式。使用null允许外推，这对于将前景用作底部标题很有用   | string | No       | All      | Yes               |
| `foregroundParallaxRatio`                | 滚动时前景视差效果的比例。如果为2，头部上升的速度是滚动速度的两倍                          | number | No       | All      | Yes               |
| `fadeOutForeground`           | 如果设置，则在向上滚动时对前景添加淡出效果 | boolean | No       | All      | Yes               |
| `renderTouchableFixedForeground`           | 与renderFixedForeground相同，但允许在其中使用可触摸组件。[在Android上可能会导致性能问题](https://github.com/bamlab/react-native-image-header-scroll-view/issues/6)   | function | No       | All      | Yes               |
| `fixedForegroundContainerStyles`           | 	可选样式，传递给固定前景组件的容器 | Object | No       | All      | Yes               |


#### **Mixed**

| Name                          | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `ScrollViewComponent` | 用于滚动的组件。可以是任何具有onScroll属性的组件（即ListView、FlatList、SectionList或ScrollView）         | Component | No       | All      | Yes               |
| `scrollViewBackgroundColor`               | scrollView内容的背景颜色                        | string | No       | All      | Yes               |



#### **TriggeringView**

| Name                          | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `onBeginHidden` | 当组件开始在滚动视图顶部隐藏时调用。          | function | No       | All      | Yes               |
| `onHide`               | 当组件在向上滚动后不再显示时调用             | function | No       | All      | Yes               |
| `onBeginDisplayed`                | 当组件在向下滚动后开始再次显示时调用 | function | No       | All      | Yes               |
| `onDisplay`                | 当组件完成再次显示时调用。            | function | No       | All      | Yes               |
| `onTouchTop`           | 	当组件完成再次显示时调用。(onDisplay + onBeginHidden) | function | No       | All      | Yes               |
| `onTouchBottom`           | 当组件在向上滚动后不再显示时调用(onHide + onBeginDisplayed)  | function | No       | All      | Yes               |
| `style`<sup>1.0.1+</sup> | TriggeringView的样式 | ViewStyle | No | All | Yes |

## 遗留问题

## 其他
-  foregroundExtrapolate属性无法生效，与Android、iOS一致：[issue#2](https://github.com/bamlab/react-native-image-header-scroll-view/issues/132 )。
-  ScrollViewComponent属性无法滚动，与Android、iOS一致：[issue#3](https://github.com/bamlab/react-native-image-header-scroll-view/issues/133 )。


## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/bamlab/react-native-image-header-scroll-view/blob/master/LICENCE) ，请自由地享受和参与开源。