> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-safe-modules</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/emilioicai/react-native-safe-modules">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/emilioicai/react-native-safe-modules/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-safe-modules)

Please go to the Releases page of the third-party library to check the compatible version information:

| Version                        | Package Name                                  | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 1.0.3 | @react-native-oh-tpl/react-native-safe-modules | [Github](https://github.com/react-native-oh-library/react-native-safe-modules) | [Github Releases](https://github.com/react-native-oh-library/react-native-safe-modules/releases) | 0.72 |
| 1.1.0                        | @react-native-ohos/react-native-safe-modules       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-safe-modules) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-safe-modules/releases) | 0.77 |

## Installation and Usage

Go to the project directory and execute the following commands:

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-safe-modules

# 0.77
npm install @react-native-ohos/react-native-safe-modules
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-safe-modules

# 0.77
yarn add @react-native-ohos/react-native-safe-modules
```

<!-- tabs:end -->

The following code shows the basic use scenario of the library:

> [!WARNING] When using, the imported library name remains unchanged.

```js
import React from "react";
import { View, Button } from "react-native";
import SafeModule from "react-native-safe-modules";

const App = () => {
  const myModule = SafeModule.create({
    moduleName: "MyNativemodule",
    mock: {
      someAPI: () => "doSomething",
    },
  });
  myModule.someAPI();

  const NativeLottieView = SafeModule.component({
    viewName: "LottieAnimationView",
    mockComponent: View,
  });

  return (
    <View style={{ flex: 1, justifyContent: "center", alignItems: "center" }}>
      <NativeLottieView
        style={{ backgroundColor: "red", width: 100, height: 100 }}
      />
    </View>
  );
};

export default App;
```

## Constraints and Limitations

### Compatibility

The following versions have been verified:

1. RNOH:0.72.28; SDK:HarmonyOS NEXT DB2; IDE:DevEco Studio 5.0.3.500; ROM:3.0.0.28;
2. RNOH: 0.77.1;SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;

## API

### SafeModule.create(options)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                     | Description                                                                                                                                                                                                                                                                                                                                                                                                  | Type            | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------- | -------- | ----------- | ----------------- |
| options.moduleName       | The name, or array of names, to look for the module at on the NativeModules namespace.                                                                                                                                                                                                                                                                                                                       | string/string[] | yes      | iOS,Android | yes               |
| options.mock             | The mock implementation of the native module.                                                                                                                                                                                                                                                                                                                                                                | object          | yes      | iOS,Android | yes               |
| options.getVersion       | A function that returns the version of the native module. Only needed if you are specifying overrides and not exporting a VERSION property on your native module. Defaults to x => x.VERSION.                                                                                                                                                                                                                | Function        | no       | iOS,Android | yes               |
| options.versionOverrides | A map of version numbers to overridden implementations of the corresponding property/method. If an overridden property or method is a function, it will be called during SafeModule.create(...) with two arguments, the original value of that property on the original module, and the original module itself. The return value of this function will be put on the return value of SafeModule.create(...). | object          | no       | iOS,Android | yes               |
| options.isEventEmitter   | A flag indicating that the native module is expected to be an EventEmitter. Puts the EventEmitter instance on the emitter property of the resulting module. Defaults to false.                                                                                                                                                                                                                               | boolean         | no       | iOS,Android | yes               |

### SafeModule.module(options)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                     | Description                                                                                                                                                                                                                                                                                                                                                                                                  | Type            | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------- | -------- | ----------- | ----------------- |
| options.moduleName       | The name, or array of names, to look for the module at on the NativeModules namespace.                                                                                                                                                                                                                                                                                                                       | string/string[] | yes      | iOS,Android | yes               |
| options.mock             | The mock implementation of the native module.                                                                                                                                                                                                                                                                                                                                                                | object          | yes      | iOS,Android | yes               |
| options.getVersion       | A function that returns the version of the native module. Only needed if you are specifying overrides and not exporting a VERSION property on your native module. Defaults to x => x.VERSION.                                                                                                                                                                                                                | Function        | no       | iOS,Android | yes               |
| options.versionOverrides | A map of version numbers to overridden implementations of the corresponding property/method. If an overridden property or method is a function, it will be called during SafeModule.create(...) with two arguments, the original value of that property on the original module, and the original module itself. The return value of this function will be put on the return value of SafeModule.create(...). | object          | no       | iOS,Android | yes               |
| options.isEventEmitter   | A flag indicating that the native module is expected to be an EventEmitter. Puts the EventEmitter instance on the emitter property of the resulting module. Defaults to false.                                                                                                                                                                                                                               | boolean         | no       | iOS,Android | yes               |

### SafeModule.component(options)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                       | Description                                                                                                                                                        | Type                    | Required | Platform    | HarmonyOS Support |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------- | -------- | ----------- | ----------------- |
| options.viewName           | The component name passed in.                                                                                                                                      | string/string[]         | yes      | iOS,Android | yes               |
| options.mockComponent      | Pass in a mock component. When viewName cannot be found, the component will return this mock component.                                                            | React.ComponentType\<T> | yes      | iOS,Android | yes               |
| options.componentOverrides | Get the components defined according to the version. If the same as viewName, override the native component's React component. Need to ensure the returned React component is valid. | object                  | no       | no          | no                |
| options.propOverrides      | Get the component properties defined according to the version. If it is the same property of the same component, override the native component's properties according to the version. Need to ensure the overridden properties exist in the native component. | object                  | no       | no          | no                |
| options.mock               | The mock implementation of the native module. Whatever members exist in the native module, you can use this property to simulate and write them yourself.        | object                  | no       | no          | no                |
| options.getVersion         | A function that returns the version of the native module. Only needed if you are specifying overrides and not exporting a VERSION property on your native module. Defaults to x => x.VERSION. | Function                | no       | no          | no                |

## Known Issues

## Others

- Component interface issue: This interface cannot be used normally on both iOS and Android. No matter what viewName is input, it will only return the mockComponent passed by the user and cannot obtain the encapsulated component. HarmonyOS behaves consistently with it: [issue#19](https://github.com/emilioicai/react-native-safe-modules/issues/19).

## License

This project is licensed under [The MIT License (MIT)](https://github.com/emilioicai/react-native-safe-modules/blob/master/LICENSE).
