> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-drop-shadow</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/hoanglam10499/react-native-drop-shadow">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/hoanglam10499/react-native-drop-shadow/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/hoanglam10499/react-native-drop-shadow/tree/1.0.0)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-drop-shadow@1.0.0
```

#### **yarn**

```bash
yarn add react-native-drop-shadow@1.0.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import DropShadow from "react-native-drop-shadow";
```

```js
export default function usage() {
  return (
    <DropShadow
      style={{
        shadowColor: "#000",
        shadowOffset: {
          width: 0,
          height: 0,
        },
        shadowOpacity: 1,
        shadowRadius: 5,
      }}
    >
      ...
    </DropShadow>
  );
}
```

 Usage with `FlatList`

```js
export default function withFlatList() {
  return (
    <FlatList
      data={[""]}
      keyExtractor={(item, index) => "List-" + index}
      CellRendererComponent={DropShadow} // <==== add line
      renderItem={({ item, index }) => (
        <DropShadow
          style={{
            shadowColor: "#000",
            shadowOffset: {
              width: 0,
              height: 0,
            },
            shadowOpacity: 1,
            shadowRadius: 5,
          }}
        >
          ...
        </DropShadow>
      )}
    />
  );
}
```

Usage with `Animated.View`

To make this work in place of an `Animated.View`, you need to use `Animated.createAnimatedComponent` to create an animatable version of `DropShadow`. For example: Animated.ViewAnimated.createAnimatedComponentDropShadow

```js
const AnimatedDropShadow = Animated.createAnimatedComponent(DropShadow);

export default function withAnimatedViews() {
  return (
    <AnimatedDropShadow
      style={{
        shadowColor: "#000",
        shadowOffset: {
          width: 0,
          height: 0,
        },
        shadowOpacity: 1,
        shadowRadius: 5,
      }}
    >
      ...
    </AnimatedDropShadow>
  );
}
```
You can then use `AnimatedDropShadow` in place of `Animated.View`.

## Constraints
- The bitmap size in Android is limited to 2048x2048, though this may vary depending on the API version.
- Using bitmaps to render shadows impacts performance, especially if multiple shadows and animations are rendered simultaneously.

### Compatibility

This document is verified based on the following versions:

react-native-harmony: 0.72.23; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio: 5.0.3.27; ROM: 3.0.0.19;

react-native-harmony: 0.72.33; SDK: Openharmony 5.0.0.71(API Version 12 Release); IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name          | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| style         | Shadow style. Common style attributes can be used.                      | style  | no       | Android/IOS | yes               |
| shadowColor   | Shadow color. CSS color values or RGBA values can be used.                   | string | no       | Android/IOS | yes               |
| shadowOffset  | Shadow offset.                                            | number | no       | Android/IOS | yes               |
| shadowOpacity | Shadow opacity. The value ranges from **0** to **1**. **0** indicates completely transparent, and **1** indicates completely opaque.| number | no       | Android/IOS | yes               |
| shadowRadius  | Shadow radius, which controls the level of blur applied to the shadow.                  | number | no       | Android/IOS | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/hoanglam10499/react-native-drop-shadow/blob/master/LICENSE).