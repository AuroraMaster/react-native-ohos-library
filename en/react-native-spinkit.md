> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-spinkit</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/maxs15/react-native-spinkit">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/maxs15/react-native-spinkit/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-spinkit)

The repository for this third-party library has been migrated to Gitcode, and it now supports direct download from npm. The new package name is: `@react-native-ohos/react-native-spinkit`. The specific version relationships are as follows:

| Version                        | Package Name       | Repository          |  Release            |Supported RN Version  |
| ------------------------------ | ----------------   | ------------------- | ------------------- | -------------------- |
| 1.5.1  | @react-native-oh-tpl/react-native-spinkit | [Github](https://github.com/react-native-oh-library/react-native-spinkit) | [Github Releases](https://github.com/react-native-oh-library/react-native-spinkit/releases) | 0.72 |
| 1.6.0 | @react-native-ohos/react-native-spinkit   | [Github](https://github.com/react-native-oh-library/react-native-spinkit) | [Github Releases](https://github.com/react-native-oh-library/react-native-spinkit/releases) | 0.77 |

## Installation and Usage

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
# 1.5.1
npm install @react-native-oh-tpl/react-native-spinkit

# 1.6.0
npm install @react-native-ohos/react-native-spinkit
```

#### **yarn**

```bash
# 1.5.1
yarn add @react-native-oh-tpl/react-native-spinkit

# 1.6.0
yarn add @react-native-ohos/react-native-spinkit
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import Spinkit from 'react-native-spinkit';

const SpinKitDemo: React.FC = (): JSX.Element => {
    return (
    	<Spinkit 
        	type='9CubeGrid' 
        	color='#e74032' 
        	size={60} 
			    style={{ backgroundColor: '#fcc424' }} 
          isVisible={true} 
		/>
    )
};

export default SpinKit;
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

 

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

- 1.5.1
```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-spinkit": "file:../../node_modules/@react-native-oh-tpl/react-native-spinkit/harmony/spinKit.har"
  }
```
- 1.6.0
```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-spinkit": "file:../../node_modules/@react-native-ohos/react-native-spinkit/harmony/spinKit.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.


> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Introducing SpinKitView Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
  // 1.5.1
+ import { SpinKitView } from "@react-native-oh-tpl/react-native-spinkit"

  // 1.6.0
+ import { SpinKitView } from "@react-native-ohos/react-native-spinkit"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === SpinKitView.NAME) {
+   SpinKitView({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+   })
+ }
 ...
}
```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added. 

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ SpinKitView.NAME
  ];
```
### 4. Introducing SpinKitPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
  // 1.5.1
+ import { RNSpinKitPackage } from '@react-native-oh-tpl/react-native-spinkit/ts';

  // 1.6.0
+ import { RNSpinKitPackage } from '@react-native-ohos/react-native-spinkit/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNSpinKitPackage(ctx)
  ];
}
```

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```


Then build and run the code.

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

This document is verified based on the following versions:
1. RNOH:0.72.96; SDK:HarmonyOS 5.1.1 Release SDK; IDE:DevEco Studio 5.1.1.840; ROM:6.0.0;
2. RNOH:0.77.18; SDK:HarmonyOS 5.1.1 Release SDK; IDE:DevEco Studio 5.1.1.840; ROM:6.0.0;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**SpinKit**:Loading Animation Rendering Component, Accepts All Parameters [View](https://reactnative.dev/docs/view#props) props�?

| props  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| type                  | Types of Load Animations                                    | string  | No       | All      | Yes               |
| type: Plane           | One Direction Flip Loading Animation                        | string  | No       | All      | Yes               |
| type: CircleFlip      | A circle flips to load animation                            | string  | No       | All      | Yes               |
| type: Bounce          | A circular nested loading animation | string | No | All | Yes |
| type: Wave | Five-bar group loading animation | string | No | All | Yes |
| type: WanderingCubes | Two squares skip loading animation | string | No | All | Yes |
| type: Pulse | A circular diffusion loading animation | string | No | All | Yes |
| type: ChasingDots | Two Circles Bounce Loading Animation | string | No | All | Yes |
| type: ThreeBounce | Three circles display the loading animation in sequence. | string | No | All | Yes |
| type: Circle | Multiple circular circular motion loading animation | string | No | All | Yes |
| type: 9CubeGrid | The nine squares display the loading animation in sequence | string | No | All | Yes |
| type: WordPress | Round wheel inline hollow circle rotating Loading animation | string | No | IOS | Yes |
| type: FadingCircle | Multiple square circular motion loading animation | string | No | All | Yes |
| type: FadingCircleAlt | Multiple circular circular motion loading animation | string | No | All | Yes |
| type: Arc | Rotating ring with notch loading animation | string | No | IOS | Yes |
| type: ArcAlt | Circular progress bar style loading animation | string | No | IOS | Yes |
| isVisible | Visibility of the spinner | boolean | No | All | Yes |
| color | Color of the spinner | string | No | All | Yes |
| size | Visibility of the spinner | number | No | All | Yes |


## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/maxs15/react-native-spinkit/blob/master/LICENSE).
