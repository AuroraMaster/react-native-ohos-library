> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/oblador/react-native-vector-icons/tree/v10.0.3)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-vector-icons@10.0.3
```

#### **yarn**

```bash
yarn add react-native-vector-icons@10.0.3
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

#### Websites Providing the Internal Font Icons

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
- [`MaterialCommunityIcons`](https://materialdesignicons.com/) from MaterialDesignIcons.com (v6.5.95 including _6596_ icons)
- [`Octicons`](http://octicons.github.com) designed by Github, Inc. (v16.3.1 with _250_ icons)
- [`Zocial`](http://zocial.smcllns.com/) by Sam Collins (v1.4.0 with _100_ icons)
- [`SimpleLineIcons`](https://simplelineicons.github.io/) crafted by Sabbir & Contributors (v2.5.5 with _189_ icons)

### Usage of the Internal Fonts

> [!ATTENTION] When using internal fonts, ensure that the .ttf files to be used exists in both **entry/src/main/ets/assets/fonts** and **entry/src/main/resource/rawfile/assets/assets/fonts**. Otherwise, the icon cannot be displayed properly.

```js
import FontAwesome from "react-native-vector-icons/FontAwesome";

<FontAwesome.Button
  name="glass"
  backgroundColor="#3b5998"
  size={20}
></FontAwesome.Button>;
```

### Usage of the External Fonts

> [!ATTENTION] When using external fonts, ensure that the .ttf files to be used exists in both **entry/src/main/ets/assets/fonts** and **entry/src/main/resource/rawfile/assets/assets/fonts**. Otherwise, the icon cannot be displayed properly.
> When external fonts are used, the .ttf and .json files are required regardless of whether the font is created by you or downloaded from the website. (The file directory is not fixed.)

#### Custom Font Files

To import a custom font file, the following names of the font file and font family are for reference only. Use the actual font file information.

```js
import { createIconSet } from "react-native-vector-icons";

const CustomTest = createIconSet(
  require("../assets/fonts/test.json"), // Import font resources from local assets.
  "poppy-icon",
  "../assets/fonts/test.ttf" // Import font resources from local assets.
);

<CustomFont.Button
  name="to-do"
  backgroundColor="#3b5998"
  size={20}
></CustomFont.Button>;
```

#### [Fonts from Fontello](http://fontello.com)

Download the font file and configuration file of a proper font from [Fontello](http://fontello.com), and import them.

```js
import { createIconSetFromFontello } from "react-native-vector-icons";
import fontelloConfig from "../assets/fonts/config.json";

const CustomFontello = createIconSetFromFontello(
  fontelloConfig,
  "fontello",
  "../assets/fonts/fontello.ttf" // Import font resources from local assets.
);

<CustomFontello.Button
  name="emo-happy"
  backgroundColor="#3b5998"
  size={20}
></CustomFontello.Button>;
```

#### [Fonts from IcoMoon](https://icomoon.io/app)

Download the font file and configuration file of a proper font from [IcoMoon](https://icomoon.io/app), and import them.

```js
import { createIconSetFromIcoMoon } from "react-native-vector-icons";
import icoMoonConfig from "../assets/fonts/selection.json"; // Import font resources from local assets.

const CustomFontIcoMoon = createIconSetFromIcoMoon(
  icoMoonConfig,
  "icomoon",
  "../assets/fonts/icomoon.ttf" // Import font resources from local assets.
);

<CustomFontIcoMoon.Button
  name="home2"
  backgroundColor="#3b5998"
  size={20}
></CustomFontIcoMoon.Button>;
```

### The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { ScrollView } from "react-native";

// Import the internal fonts of the original library.
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
  // Import the custom fonts.
  const CustomTest = createIconSet(
    require("../assets/fonts/test.json"), // Import font resources from local assets.
    "poppy-icon",
    "../assets/fonts/test.ttf" // Import font resources from local assets.
  );

  // Import the custom fonts from IcoMoon.
  const CustomIconMoon = createIconSetFromIcoMoon(
    icoMoonConfig,
    "icomoon",
    "../assets/fonts/icomoon.ttf" // Import font resources from local assets.
  );

  // Import the custom fonts from Fontello.
  const CustomFontello = createIconSetFromFontello(
    fontelloConfig,
    "fontello",
    "../assets/fonts/fontello.ttf" // Import font resources from local assets.
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

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### Introducing and Registering a Font File to ArkTs

Step 1:
Copy the font file in the `node_modules/react-native-vector-icons/Fonts` directory to the `entry/src/main/resources/rawfile/fonts` directory. If an external font file is used, copy the \*.ttf file.

Step 2:
Open the `entry/src/main/ets/pages/Index.ets` file and add the following code:

```ts
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
      // The following three external fonts are used as examples.
      'icomoon': $rawfile('fonts/icomoon.ttf'),
      'fontello': $rawfile('fonts/fontello.ttf'),
      'poppy-icon': $rawfile('fonts/test.ttf')
    }
    // ...
  }
})
```

#### Note: You need to register a custom font here in the same way.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

If their versions are earlier than API version 11, the font registration fails and the icon cannot be displayed.

This document is verified based on the following versions:

1. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Known Issues

- [ ] The native methods **getImageSource** and **getImageSourceSync** can be used to draw a font file into a bitmap for the `Image` component to use. Currently, the HarmonyOS platform does not support this feature.

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/oblador/react-native-vector-icons/blob/master/LICENSE).
