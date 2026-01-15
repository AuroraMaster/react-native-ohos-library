> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"><code><a href="https://github.com/oblador/react-native-vector-icons">react-native-vector-icons</a></code> </h1>
</p>
<p align="center">
    <a href="https://github.com/oblador/react-native-vector-icons">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/oblador/react-native-vector-icons/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/oblador/react-native-vector-icons)

## 安装与使用

| 三方库版本 | 支持RN版本 |
| ---------- | ---------- |
| 10.0.3     | 0.72       |
| 10.2.0     | 0.77       |
| - | 0.82     |
> [!TIP] 该库适配0.82的版本已拆分为多个子包，请按需引入，具体版本号见安装命令。


进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install react-native-vector-icons@10.0.3

# 0.77
npm install react-native-vector-icons@10.2.0

# 0.82
//使用自带字体
npm install @react-native-vector-icons/fontawesome5@12.3.0
npm install @react-native-vector-icons/fontawesome6@12.3.0
npm install @react-native-vector-icons/fontisto@12.4.0
npm install @react-native-vector-icons/foundation@12.4.0
npm install @react-native-vector-icons/ionicons@12.3.0
npm install @react-native-vector-icons/material-icons@12.4.0
npm install @react-native-vector-icons/simple-line-icons@12.4.0
npm install @react-native-vector-icons/octicons@20.4.0
npm install @react-native-vector-icons/zocial@12.4.0
npm install @react-native-vector-icons/ant-design@12.4.0
npm install @react-native-vector-icons/entypo@12.4.0
npm install @react-native-vector-icons/evil-icons@12.4.0
npm install @react-native-vector-icons/feather@12.4.0
npm install @react-native-vector-icons/fontawesome@12.4.0
npm install @react-native-vector-icons/material-design-icons@12.4.0
//使用外部字体
npm install @react-native-vector-icons/common@12.4.0
```

#### **yarn**

```bash
# 0.72
yarn add react-native-vector-icons@10.0.3

# 0.77
yarn add react-native-vector-icons@10.2.0

# 0.82
//使用自带字体
yarn add @react-native-vector-icons/fontawesome5@12.3.0
yarn add @react-native-vector-icons/fontawesome6@12.3.0
yarn add @react-native-vector-icons/fontisto@12.4.0
yarn add @react-native-vector-icons/foundation@12.4.0
yarn add @react-native-vector-icons/ionicons@12.3.0
yarn add @react-native-vector-icons/material-icons@12.4.0
yarn add @react-native-vector-icons/simple-line-icons@12.4.0
yarn add @react-native-vector-icons/octicons@20.4.0
yarn add @react-native-vector-icons/zocial@12.4.0
yarn add @react-native-vector-icons/ant-design@12.4.0
yarn add @react-native-vector-icons/entypo@12.4.0
yarn add @react-native-vector-icons/evil-icons@12.4.0
yarn add @react-native-vector-icons/feather@12.4.0
yarn add @react-native-vector-icons/fontawesome@12.4.0
yarn add @react-native-vector-icons/material-design-icons@12.4.0
//使用外部字体
yarn add @react-native-vector-icons/common@12.4.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

#### 自带字体图标对照网页

[Explore all icons](https://oblador.github.io/react-native-vector-icons/).

- [`AntDesign`](https://ant.design/) from AntFinance (_298_ icons)
- [`Entypo`](http://entypo.com) by Daniel Bruce (v1.0.1 with _411_ icons)
- [`EvilIcons`](http://evil-icons.io) designed by Alexander Madyankin & Roman Shamin (v1.10.1 with _70_ icons)
- [`Feather`](http://feathericons.com) created by Cole Bemis & Contributors (v4.28.0 featuring _286_ icons)
- [`FontAwesome`](http://fortawesome.github.io/Font-Awesome/icons/) by Dave Gandy (v4.7.0 containing _675_ icons)
- [`FontAwesome 5`](https://fontawesome.com/v5/icons/) from Fonticons, Inc. (v5.15.3 offering _1598_ free and _7848_ pro icons)
- [`FontAwesome 6`](https://fontawesome.com) designed by Fonticons, Inc. (v6.1.2 featuring _2016_ free and _16150_ pro icons)
- [`Fontisto`](https://github.com/kenangundogan/fontisto) created by Kenan Gündoğan (v3.0.4 featuring _615_ icons)
- [`Foundation`](http://zurb.com/playground/foundation-icon-fonts-3) by ZURB, Inc. (v3.0 with _283_ icons)
- [`Ionicons`](https://ionicons.com/) crafted by Ionic (v7.1.0 containing _1338_ icons)
- [`MaterialIcons`](https://fonts.google.com/icons/) by Google, Inc. (v4.0.0 featuring _2189_ icons)
- [`MaterialDesignIcons`](https://materialdesignicons.com/) from MaterialDesignIcons.com (v6.5.95 including _6596_ icons)
- [`Octicons`](http://octicons.github.com) designed by Github, Inc. (v16.3.1 with _250_ icons)
- [`Zocial`](http://zocial.smcllns.com/) by Sam Collins (v1.4.0 with _100_ icons)
- [`SimpleLineIcons`](https://simplelineicons.github.io/) crafted by Sabbir & Contributors (v2.5.5 with _189_ icons)

### 本库自带字体的使用

> [!ATTENTION] 使用字体时，请确保 entry/src/main/ets/assets/fonts 和 entry/src/main/resource/rawfile/assets/assets/fonts 下同时拥有要使用的 ttf 文件，否则图标不能正常显示

```js
// 0.72/0.77
import FontAwesome from "react-native-vector-icons/FontAwesome";

<FontAwesome.Button
  name="glass"
  backgroundColor="#3b5998"
  size={20}
></FontAwesome.Button>;

// 0.82
import FontAwesome from '@react-native-vector-icons/fontawesome';

<FontAwesome
  name="glass"
  color="#3b5998"
  size={20}
></FontAwesome>;
```

### 外部字体使用(0.72/0.77)

> [!ATTENTION] 使用外部字体时，请确保 entry/src/main/ets/assets/fonts 和 entry/src/main/resource/rawfile/assets/assets/fonts 下同时拥有要使用的 ttf 文件，否则图标不能正常显示
> 使用外部字体时，不管是用户自己制作的字体文件还是从网站下载的字体文件，都需要有 _.ttf 和 _.json 文件(文件目录不固定，能引用到就可以了)

#### 用户自制字体文件

用户自己制作的字体文件导入使用，以下字体文件名和字体家族名仅供参考，以用户实际输出字体文件信息为准

```js
import { createIconSet } from "react-native-vector-icons";

const CustomTest = createIconSet(
  require("../assets/fonts/test.json"), // 引入本地assets下的字体资源
  "poppy-icon",
  "../assets/fonts/test.ttf" // 引入本地assets下的字体资源
);

<CustomFont.Button
  name="to-do"
  backgroundColor="#3b5998"
  size={20}
></CustomFont.Button>;
```

#### [fontello](http://fontello.com)网站中的字体使用

从[fontello](http://fontello.com)网站选择合适的字体之后下载对应的字体文件和配置文件导入使用

```js
import { createIconSetFromFontello } from "react-native-vector-icons";
import fontelloConfig from "../assets/fonts/config.json";

const CustomFontello = createIconSetFromFontello(
  fontelloConfig,
  "fontello",
  "../assets/fonts/fontello.ttf" // 引入本地assets下的字体资源
);

<CustomFontello.Button
  name="emo-happy"
  backgroundColor="#3b5998"
  size={20}
></CustomFontello.Button>;
```

#### [IcoMoon](https://icomoon.io/app)网站中的字体使用

从[IcoMoon](https://icomoon.io/app)网站选择合适的字体之后下载对应的字体文件和配置文件导入使用

```js
import { createIconSetFromIcoMoon } from "react-native-vector-icons";
import icoMoonConfig from "../assets/fonts/selection.json"; // 引入本地assets下的字体资源

const CustomFontIcoMoon = createIconSetFromIcoMoon(
  icoMoonConfig,
  "icomoon",
  "../assets/fonts/icomoon.ttf" // 引入本地assets下的字体资源
);

<CustomFontIcoMoon.Button
  name="home2"
  backgroundColor="#3b5998"
  size={20}
></CustomFontIcoMoon.Button>;
```
### 外部字体使用(0.82)

```js
import { createIconSet } from "@react-native-vector-icons/common";

const CustomFontIcoMoon = createIconSet({ 
  "home": 59648 
  }, 
  "home", 
  "home.ttf"
);

<CustomFontIcoMoon
  name="home"
  color="#3b5998"
  size={20}
><Text>home</Text></CustomFontIcoMoon>
```

### 以下展示了本库的基本用法

> [!WARNING] 使用时 import 的库名不变。

```js
//0.72/0.77
import React from "react";
import { ScrollView } from "react-native";

//导入原库自带字体
import FontAwesome5 from "react-native-vector-icons/FontAwesome5";
import FontAwesome6 from "react-native-vector-icons/FontAwesome6";
import Fontisto from "react-native-vector-icons/Fontisto";
import Foundation from "react-native-vector-icons/Foundation";
import Ionicons from "react-native-vector-icons/Ionicons";
import MaterialCommunityIcons from "react-native-vector-icons/MaterialCommunityIcons";
import MaterialIcons from "react-native-vector-icons/MaterialIcons";
import SimpleLineIcons from "react-native-vector-icons/SimpleLineIcons";
import Octicons from "react-native-vector-icons/Octicons";
import Zocial from "react-native-vector-icons/Zocial";
import AntDesign from "react-native-vector-icons/AntDesign";
import Entypo from "react-native-vector-icons/Entypo";
import EvilIcons from "react-native-vector-icons/EvilIcons";
import Feather from "react-native-vector-icons/Feather";
import FontAwesome from "react-native-vector-icons/FontAwesome";

import {
  createIconSetFromIcoMoon,
  createIconSetFromFontello,
  createIconSet,
} from "react-native-vector-icons";
import icoMoonConfig from "../assets/fonts/icomoon-selection.json";
import fontelloConfig from "../assets/fonts/fontello-config.json";

export function VectorIconsDemo() {
  //引入用户自制字体
  const CustomTest = createIconSet(
    require("../assets/fonts/test.json"), // 引入本地assets下的字体资源
    "poppy-icon",
    "../assets/fonts/test.ttf" // 引入本地assets下的字体资源
  );

  //引入 IcoMoon 自定义字体
  const CustomIconMoon = createIconSetFromIcoMoon(
    icoMoonConfig,
    "icomoon",
    "../assets/fonts/icomoon.ttf" // 引入本地assets下的字体资源
  );

  //引入 fontello 自定义字体
  const CustomFontello = createIconSetFromFontello(
    fontelloConfig,
    "fontello",
    "../assets/fonts/fontello.ttf" // 引入本地assets下的字体资源
  );

  return (
    <ScrollView style={{ padding: 20 }}>
      <CustomTest.Button
        name="application-record"
        backgroundColor="#3b5998"
        size={20}
      >
        CustomTest application-record
      </CustomTest.Button>

      <CustomTest.Button name="to-do" backgroundColor="#3b5998" size={20}>
        CustomTest to-do
      </CustomTest.Button>

      <CustomIconMoon.Button name="home2" backgroundColor="#3b5998">
        CustomIconMoon home2
      </CustomIconMoon.Button>

      <CustomFontello.Button name="emo-happy" backgroundColor="#3b5998">
        CustomFontello emo-happy
      </CustomFontello.Button>

      <AntDesign.Button name="forward" backgroundColor="#3b5998" size={20}>
        AntDesign forward
      </AntDesign.Button>

      <Entypo.Button name="app-store" backgroundColor="#3b5998" size={20}>
        Entypo app-store
      </Entypo.Button>

      <EvilIcons.Button name="bell" backgroundColor="#3b5998" size={20}>
        EvilIcons bell
      </EvilIcons.Button>

      <Feather.Button name="sunrise" backgroundColor="#3b5998" size={20}>
        Feather sunrise
      </Feather.Button>
      <FontAwesome.Button name="glass" backgroundColor="#3b5998" size={20}>
        FontAwesome glass
      </FontAwesome.Button>

      <FontAwesome5.Button name="angry" backgroundColor="#3b5998" size={20}>
        FontAwesome5_regular angry
      </FontAwesome5.Button>
      <FontAwesome5.Button name="adn" backgroundColor="#3b5998" size={20}>
        FontAwesome5_brands adn
      </FontAwesome5.Button>
      <FontAwesome5.Button name="ad" backgroundColor="#3b5998" size={20}>
        FontAwesome5_solid ad
      </FontAwesome5.Button>

      <FontAwesome6.Button name="adn" backgroundColor="#3b5998" size={20}>
        FontAwesome6_brands adn
      </FontAwesome6.Button>
      <FontAwesome6.Button
        name="bookmark"
        backgroundColor="#3b5998"
        size={20}
        solid
      >
        FontAwesome6_regular bookmark
      </FontAwesome6.Button>
      <FontAwesome6.Button
        name="apple-whole"
        backgroundColor="#3b5998"
        size={20}
      >
        FontAwesome6_solid apple-whole
      </FontAwesome6.Button>
      <Fontisto.Button name="aws" backgroundColor="#3b5998" size={20}>
        Fontisto aws
      </Fontisto.Button>
      <Foundation.Button name="archive" backgroundColor="#3b5998" size={20}>
        Foundation archive
      </Foundation.Button>
      <Ionicons.Button name="aperture" backgroundColor="#3b5998" size={20}>
        Ionicons aperture
      </Ionicons.Button>
      <MaterialCommunityIcons.Button
        name="zip-box"
        backgroundColor="#3b5998"
        size={20}
      >
        MaterialCommunityIcons zip-box
      </MaterialCommunityIcons.Button>
      <MaterialIcons.Button name="airplay" backgroundColor="#3b5998" size={20}>
        MaterialIcons airplay
      </MaterialIcons.Button>
      <Octicons.Button name="share" backgroundColor="#3b5998" size={20}>
        Octicons share
      </Octicons.Button>
      <SimpleLineIcons.Button name="mouse" backgroundColor="#3b5998" size={20}>
        SimpleLineIcons mouse
      </SimpleLineIcons.Button>
      <Zocial.Button name="rss" backgroundColor="#3b5998" size={20}>
        Zocial rss
      </Zocial.Button>
    </ScrollView>
  );
}
```

```js
//0.82
import React from "react";
import { ScrollView, Text } from "react-native";

//导入原库自带字体
import FontAwesome5 from '@react-native-vector-icons/fontawesome5';
import FontAwesome6 from '@react-native-vector-icons/fontawesome6';
import Fontisto from '@react-native-vector-icons/fontisto';
import Foundation from '@react-native-vector-icons/foundation';
import Ionicons from '@react-native-vector-icons/ionicons';
import MaterialDesignIcons from '@react-native-vector-icons/material-design-icons';
import MaterialIcons from '@react-native-vector-icons/material-icons';
import SimpleLineIcons from '@react-native-vector-icons/simple-line-icons';
import Octicons from '@react-native-vector-icons/octicons';
import Zocial from '@react-native-vector-icons/zocial';
import AntDesign from '@react-native-vector-icons/ant-design';
import Entypo from '@react-native-vector-icons/entypo';
import EvilIcons from '@react-native-vector-icons/evil-icons';
import Feather from '@react-native-vector-icons/feather';
import FontAwesome from '@react-native-vector-icons/fontawesome';

import { createIconSet } from "@react-native-vector-icons/common";

export function VectorIconsDemo() {
    //引入用户自制字体
    const CustomFontIcoMoon = createIconSet(
        { "home": 59648 }, "home", "home.ttf"
    );

    const CustomFontello = createIconSet(
        { "child": 61870 }, "fontello", "fontello.ttf"
    );

    const Pencil = createIconSet(
        { "pencil": 59653 }, "pencil", "pencil.ttf"
    );

    return (
        <ScrollView style={{ padding: 20 }}>
            <CustomFontello
                name="child"
                color="#3b5998"
                size={20}
            ><Text>child</Text></CustomFontello>

            <Pencil
                name="pencil"
                color="#3b5998"
                size={20}
            ><Text>pencil</Text></Pencil>

            <CustomFontIcoMoon
                name="home"
                color="#3b5998"
                size={20}
            ><Text>home</Text></CustomFontIcoMoon>

            <AntDesign
                name="forward"
                color="#3b5998"
                size={20}
            >
                <Text>AntDesign forward</Text>
            </AntDesign>

            <Entypo
                name="app-store"
                color="#3b5998"
                size={20}
            >
                <Text>Entypo app-store</Text>
            </Entypo>

            <EvilIcons
                name="bell"
                color="#3b5998"
                size={20}
            >
                <Text>EvilIcons bell</Text>
            </EvilIcons>

            <Feather
                name="sunrise"
                color="#3b5998"
                size={20}
            >
                <Text>Feather sunrise</Text>
            </Feather>

            <FontAwesome
                name="glass"
                color="#3b5998"
                size={20}
            >
                <Text>FontAwesome glass</Text>
            </FontAwesome>

            <FontAwesome5
                name="angry"
                color="#3b5998"
                size={20}
            >
                <Text>FontAwesome5_regular angry</Text>
            </FontAwesome5>

            <FontAwesome5
                name="adn"
                color="#3b5998"
                size={20}
                iconStyle='brand'
            >
                <Text>FontAwesome5_brands adn</Text>
            </FontAwesome5>

            <FontAwesome5
                name="ad"
                color="#3b5998"
                size={20}
                iconStyle='solid'
            >
                <Text>FontAwesome5_solid ad</Text>
            </FontAwesome5>

            <FontAwesome6
                name="adn"
                color="#3b5998"
                size={20}
                iconStyle='brand'
            >
                <Text>FontAwesome6_brands adn</Text>
            </FontAwesome6>

            <FontAwesome6
                name="bookmark"
                color="#3b5998"
                size={20}
            >
                <Text>FontAwesome6_regular bookmark</Text>
            </FontAwesome6>

            <FontAwesome6
                name="apple-whole"
                color="#3b5998"
                size={20}
                iconStyle="solid"
            >
                <Text>FontAwesome6_solid apple-whole</Text>
            </FontAwesome6>

            <Fontisto
                name="aws"
                color="#3b5998"
                size={20}
            >
                <Text>Fontisto aws</Text>
            </Fontisto>

            <Foundation
                name="archive"
                color="#3b5998"
                size={20}
            >
                <Text>Foundation archive</Text>
            </Foundation>

            <Ionicons
                name="aperture"
                color="#3b5998"
                size={20}
            >
                <Text>Ionicons aperture</Text>
            </Ionicons>

            <MaterialDesignIcons
                name="zip-box"
                color="#3b5998"
                size={20}
            >
                <Text>MaterialCommunityIcons zip-box</Text>
            </MaterialDesignIcons>

            <MaterialIcons
                name="airplay"
                color="#3b5998"
                size={20}
            >
                <Text>MaterialIcons airplay</Text>
            </MaterialIcons>

            <Octicons
                name="share"
                color="#3b5998"
                size={20}
            >
                <Text>Octicons share</Text>
            </Octicons>

            <SimpleLineIcons
                name="mouse"
                color="#3b5998"
                size={20}
            >
                <Text>SimpleLineIcons mouse</Text>
            </SimpleLineIcons>

            <Zocial
                name="rss"
                color="#3b5998"
                size={20}
            >
                <Text>Zocial rss</Text>
            </Zocial>
        </ScrollView>
    );
}
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在 ArkTs 侧引入和注册字体文件

步骤一：
0.72/0.77：
复制 `node_modules/react-native-vector-icons/Fonts` 目录下的字体文件到 `entry/src/main/resources/rawfile/fonts` 目录下(如使用了外部字体文件，需要将\*.ttf 文件复制过来)
0.82：
只需将外部字体文件复制到 `entry/src/main/resources/rawfile/fonts` 目录下

步骤二：
打开 `entry/src/main/ets/pages/Index.ets`，添加以下代码

```ts
// 0.72/0.77
RNApp({
  rnInstanceConfig: {
    fontResourceByFontFamily: {
      'anticon': $rawfile('fonts/AntDesign.ttf'),
      'Entypo': $rawfile('fonts/Entypo.ttf'),
      'EvilIcons': $rawfile('fonts/EvilIcons.ttf'),
      'Feather': $rawfile('fonts/Feather.ttf'),
      'FontAwesome': $rawfile('fonts/FontAwesome.ttf'),
      'FontAwesome5Brands-Regular': $rawfile('fonts/FontAwesome5_Brands.ttf'),
      'FontAwesome5Free-Regular': $rawfile('fonts/FontAwesome5_Regular.ttf'),
      'FontAwesome5Free-Solid': $rawfile('fonts/FontAwesome5_Solid.ttf'),
      'FontAwesome6Brands-Regular': $rawfile('fonts/FontAwesome6_Brands.ttf'),
      'FontAwesome6Free-Regular': $rawfile('fonts/FontAwesome6_Regular.ttf'),
      'FontAwesome6Free-Solid': $rawfile('fonts/FontAwesome6_Solid.ttf'),
      'Fontisto': $rawfile('fonts/Fontisto.ttf'),
      'fontcustom': $rawfile('fonts/Foundation.ttf'),
      'Ionicons': $rawfile('fonts/Ionicons.ttf'),
      'Material Design Icons': $rawfile('fonts/MaterialCommunityIcons.ttf'),
      'Material Icons': $rawfile('fonts/MaterialIcons.ttf'),
      'Octicons': $rawfile('fonts/Octicons.ttf'),
      'simple-line-icons': $rawfile('fonts/SimpleLineIcons.ttf'),
      'zocial': $rawfile('fonts/Zocial.ttf'),
      // 以下三种为外部字体，这里是举例说明，以用户实际为准
      'icomoon': $rawfile('fonts/icomoon.ttf'),
      'fontello': $rawfile('fonts/fontello.ttf'),
      'poppy-icon': $rawfile('fonts/test.ttf')
    }
    // ...
  }
})
```

```ts
// 0.82
RNApp({
  rnInstanceConfig: {
    fontResourceByFontFamily: {
      'AntDesign': $rawfile('assets/node_modules/@react-native-vector-icons/ant-design/fonts/AntDesign.ttf'),
      'Entypo': $rawfile('assets/node_modules/@react-native-vector-icons/entypo/fonts/Entypo.ttf'),
      'EvilIcons': $rawfile('assets/node_modules/@react-native-vector-icons/evil-icons/fonts/EvilIcons.ttf'),
      'Feather': $rawfile('assets/node_modules/@react-native-vector-icons/feather/fonts/Feather.ttf'),
      'FontAwesome': $rawfile('assets/node_modules/@react-native-vector-icons/fontawesome/fonts/FontAwesome.ttf'),
      'FontAwesome5Brands-Regular': $rawfile('assets/node_modules/@react-native-vector-icons/fontawesome5/fonts/FontAwesome5_Brands.ttf'),
      'FontAwesome5Free-Regular': $rawfile('assets/node_modules/@react-native-vector-icons/fontawesome5/fonts/FontAwesome5_Regular.ttf'),
      'FontAwesome5Free-Solid': $rawfile('assets/node_modules/@react-native-vector-icons/fontawesome5/fonts/FontAwesome5_Solid.ttf'),
      'FontAwesome6Brands-Regular': $rawfile('assets/node_modules/@react-native-vector-icons/fontawesome6/fonts/FontAwesome6_Brands.ttf'),
      'FontAwesome6Free-Regular': $rawfile('assets/node_modules/@react-native-vector-icons/fontawesome6/fonts/FontAwesome6_Regular.ttf'),
      'FontAwesome6Free-Solid': $rawfile('assets/node_modules/@react-native-vector-icons/fontawesome6/fonts/FontAwesome6_Solid.ttf'),
      'Fontisto': $rawfile('assets/node_modules/@react-native-vector-icons/fontisto/fonts/Fontisto.ttf'),
      'fontcustom': $rawfile('assets/node_modules/@react-native-vector-icons/foundation/fonts/Foundation.ttf'),
      'Ionicons': $rawfile('assets/node_modules/@react-native-vector-icons/ionicons/fonts/Ionicons.ttf'),
      'MaterialDesignIcons': $rawfile('assets/node_modules/@react-native-vector-icons/material-design-icons/fonts/MaterialDesignIcons.ttf'),
      'MaterialIcons-Regular': $rawfile('assets/node_modules/@react-native-vector-icons/material-icons/fonts/MaterialIcons.ttf'),
      'Octicons': $rawfile('assets/node_modules/@react-native-vector-icons/octicons/fonts/Octicons.ttf'),
      'simple-line-icons': $rawfile('assets/node_modules/@react-native-vector-icons/simple-line-icons/fonts/SimpleLineIcons.ttf'),
      'zocial': $rawfile('assets/node_modules/@react-native-vector-icons/zocial/fonts/Zocial.ttf'),
      // 以下三种为外部字体，这里是举例说明，以用户实际为准
      "home": $rawfile('fonts/home.ttf'),
      "pencil": $rawfile('fonts/pencil.ttf'),
      "fontello": $rawfile('fonts/fontello.ttf')
    }
    // ...
  }
})
```

#### 提醒：自定义字体也需要用同样的方法在此注册

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

> [!TIP]请使用 Api 11 及以上版本，低版本会导致 font 注册不成功，图标显示不出来。

本文档内容基于以下版本验证通过：

1. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;
3. RNOH：0.82.1; SDK：HarmonyOS 6.0.0.47 (API Version 21); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。	


| 名称 | 描述 | 类型 | 是否必需 | 支持的平台 | 是否支持HarmonyOS  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| size       | 图标的尺寸。                                          | number | No       | iOS/Android      | yes               |
| name       | 要显示的图标                                          | string | Yes       | iOS/Android      | yes               |
| color       | 图标颜色                 | string | No       | iOS/Android      | yes               |


## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。	


| 名称 | 描述 | 类型 | 是否必需 | 支持的平台 | 是否支持HarmonyOS  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| getImageSource       | 将字体文件绘制成 Bitmap 位图供 Image 组件使用                                          | Function | No       | iOS/Android      | No               |
| getImageSourceSync       | 将字体文件绘制成 Bitmap 位图供 Image 组件使用                                        | Function | No       | iOS/Android      | No               |


## 遗留问题

- [ ] getImageSource 和 getImageSourceSync 原生方法可以将字体文件绘制成 Bitmap 位图供 `Image` 组件使用，Harmony OS 侧暂时不支持

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/oblador/react-native-vector-icons/blob/master/LICENSE) ，请自由地享受和参与开源。