> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-intersection-observer</code> </h1>
</p>

This project is based on [react-native-intersection-observer@0.2.0](https://github.com/zhbhun/react-native-intersection-observer/tree/0.2.0).

Please visit the Release release address of the third-party library to view the corresponding version information:

| Version | Releases info                                                     | Support RN version |
| ---------- | ------------------------------------------------------------ | ---------- |
|  0.2.0  | [@react-native-oh-tpl/react-native-intersection-observer Releases](https://github.com/react-native-oh-library/react-native-intersection-observer/releases) | 0.72       |
| 0.3.0   | [@react-native-ohos/react-native-intersection-observer Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-intersection-observer/releases)     | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

## Installation and Usage

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
# 0.72 
npm install @react-native-oh-tpl/react-native-intersection-observer

# 0.77 
npm install @react-native-ohos/react-native-intersection-observer
```

#### **yarn**

```bash
# 0.72 
yarn add @react-native-oh-tpl/react-native-intersection-observer

# 0.77 
yarn add @react-native-ohos/react-native-intersection-observer
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useRef } from "react";
import { Text } from "react-native";
import {
  IOScrollView,
  IOScrollViewController,
  InView,
} from "react-native-intersection-observer";

function App() {
  const scrollViewRef = useRef<IOScrollViewController>(null);
  return (
    <IOScrollView ref={scrollViewRef}>
      <Text
        onPress={() => {
          scrollViewRef.current?.scrollToEnd();
        }}
      >
        Scroll to bottom
      </Text>
      <InView onChange={(inView: boolean) => console.log("Inview:", inView)}>
        <Text>
          Plain children are always rendered. Use onChange to monitor state.
        </Text>
      </InView>
    </IOScrollView>
  );
}

export default App;
```

## Constraints

#### Compatibility

The content in this document has been verified under the following environment:

1. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-intersection-observer](https://github.com/zhbhun/react-native-intersection-observer/blob/master/README.md)

#### **IOScrollView** **Component**

Props: Inherits [ScrollView Props](https://reactnative.dev/docs/scrollview#props)

| Name       | Description   | Type                                                         | Required | HarmonyOS Support |
| ---------- | ------------- | ------------------------------------------------------------ | -------- | ----------------- |
| rootMargin | `root margin` | { top: number; left: number; right: number; bottom: number } | false    | yes               |

Methods: Inherits [ScrollView Methods](https://reactnative.dev/docs/scrollview#methods)

#### **IOFlatList** **Component**

Props: Inherits [FlatList Props](https://reactnative.dev/docs/flatlist#props)

| Name       | Description   | Type                                                         | Required | HarmonyOS Support |
| ---------- | ------------- | ------------------------------------------------------------ | -------- | ----------------- |
| rootMargin | `root margin` | { top: number; left: number; right: number; bottom: number } | false    | yes               |

Methods: Inherits [FlatList Methods](https://reactnative.dev/docs/flatlist#methods)

#### **InView** **Component**

| Name        | Description                                                  | Type                        | Required | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | --------------------------- | -------- | ----------------- |
| as          | `Render the wrapping element as this element. Defaults to `View`.` | `ComponentType`             | false    | yes               |
| children    | Children expects a plain child, to have the `<InView />` deal with the wrapping element. | ReactNode                   | true     | yes               |
| triggerOnce | Only trigger this method once.                               | boolean                     | false    | yes               |
| onChange    | Call this function whenever the in view state changes. It will receive the `inView` boolean, alongside the current `IntersectionObserverEntry`. | `(inView: boolean) => void` | false    | yes               |

## Known Issues

## Others

## License

This project is licensed under [MIT License](https://github.com/zhbhun/react-native-intersection-observer/blob/master/LICENSE).
