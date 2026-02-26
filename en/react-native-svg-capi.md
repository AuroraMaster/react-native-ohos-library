> Template version: v0.4.0

<p align="center">
  <h1 align="center"> <code>react-native-svg(CAPI)</code> </h1>
</p>

This project is based on [react-native-svg](https://github.com/software-mansion/react-native-svg) .

This third-party library has been migrated to Gitcode and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-svg`, The version correspondence details are as follows:

| Name                                  | Version              | Release Information                                          | Supported RN Version | Supported Autolink | Compile API Version | Community Baseline Version | npm Address                                                  |
| ------------------------------------- | -------------------- | ------------------------------------------------------------ | -------------------- | ------------------ | ------------------- | -------------------------- | ------------------------------------------------------------ |
| @react-native-ohos/react-native-svg   | ~15.13.0             | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-svg/releases) | 0.82.*               | No                 | API15+              | 15.15.0                    | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-svg) |
| @react-native-ohos/react-native-svg   | ~15.12.1             | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-svg/releases) | 0.77.*               | No                 | API15+              | 15.12.0                    | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-svg) |
| @react-native-ohos/react-native-svg   | ~ 15.0.2             | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-svg/releases) | 0.72.*               | Yes                | API15+              | 15.0.0                     | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-svg) |
| @react-native-oh-tpl/react-native-svg | <= 15.0.1@deprecated | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-harmony-svg/releases) | 0.72.*               | No                 | API12+              | 15.0.0                     | [Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/react-native-svg) |

## 1. Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install react-native-svg@15.0.0
npm install @react-native-ohos/react-native-svg

# 0.77
npm install react-native-svg@15.12.0
npm install @react-native-ohos/react-native-svg

# 0.82
npm install react-native-svg@15.15.0
npm install @react-native-ohos/react-native-svg
```

#### **yarn**

```bash
# 0.72
yarn add react-native-svg@15.0.0
yarn add @react-native-ohos/react-native-svg

# 0.77
yarn add react-native-svg@15.12.0
yarn add @react-native-ohos/react-native-svg

# 0.82
yarn add react-native-svg@15.15.0
yarn add @react-native-ohos/react-native-svg
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import { StyleSheet,SafeAreaView } from 'react-native';
import { Svg,Path } from 'react-native-svg';

export default function App() {
  return (
    <SafeAreaView style={styles.container}>
      <Svg width="100" height="100">
        <Path d="M90 0 L0 180 L180 180 Z" fill="red" />
      </Svg>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex:1,
    backgroundColor: 'grey',
  },
});
```

## 2. Manual Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~15.13.0 | No | 0.82 |
| ~15.12.1                               |  No                   |  0.77                |
| ~15.0.2                              |  Yes                  |  0.72                |
| <= 15.0.1@deprecated            |  No                   |  0.72                |

Projects using AutoLink need to be configured according to this document, AutoLink framework guide.：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you are using supports Autolink and the project has integrated Autolink, you can skip the ManualLink configuration.

<details>
  <summary>ManualLink: This step provides guidance for manually configuring native dependencies.</summary>


Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1 Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2 Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@react-native-ohos/react-native-svg": "file:../../node_modules/@react-native-ohos/react-native-svg/harmony/svg.har"
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

### 2.3 Configuring CMakeLists and Introducing SVGPackage

> If you are using version <= 15.0.1, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-svg/src/main/cpp" ./svg)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_svg)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "SVGPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<SVGPackage>(ctx),
    };
}
```

### 2.4.  Introducing SvgPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { SvgPackage } from '@react-native-ohos/react-native-svg/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new SvgPackage(ctx),
  ];
}
```
</details>

## 2.5 Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

### On the ArkTs side, importing and registering font files is an optional configuration step.（Non-mandatory configuration items，this module always requires manual configuration）

> [!TIP] This item is not mandatory. It only needs to be configured when using the fontFamily Properties property in the Text to specify a custom font.

Step 1:
Copy the font files to the entry/src/main/resources/rawfile/assets/fonts directory (if external font files are used, you need to copy the *.ttf files over).

Step 2：
Open `entry/src/main/ets/pages/Index.ets` and add the following code:

    const fonts: Record<string, Resource> = {
        "Noto Sans Pau Cin Hau": $rawfile("assets/fonts/Noto Sans Pau Cin Hau.ttf") ,
        "NotoSansVai-Regular": $rawfile("assets/fonts/NotoSansVai-Regular.ttf") ,
        "HarmonyOS_Sans_Condensed_Regular_Italic": $rawfile("assets/fonts/HarmonyOS_Sans_Condensed_Regular_Italic.ttf")
        "HarmonyOS_Sans_Digit_Medium": $rawfile("assets/fonts/HarmonyOS_Sans_Digit_Medium.ttf")
    }
    
    @Entry
    @Component
    struct Index {
        //...
        build() {
            Column(){
                //...
    
                RNApp({
                rnInstanceConfig: {
                    //...
                    fontResourceByFontFamily: fonts
                },
                //...
            }
    
        }
        //...
    }

## 3. Constraints

### 3.1 Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
4. RNOH: 0.82.1; SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1 Release; ROM: 6.0.0.120 SP7;

### 3.2. API requirements

> [!TIP] All versions of the current third-party libraries have implemented version isolation, supporting compilation in `API12+` projects and execution on `API12+` ROMs.

> [!TIP] The following features depend on specific API versions. Compiling the project with an API version lower than specified or running the ROM with an API version lower than specified may result in limited functionality.

1. Version >=15.0.2 for 0.72 introduced [OH_ArkUI_CreateSnapshotOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-type-h#oh_arkui_createsnapshotoptions)，[OH_ArkUI_SnapshotOptions_SetScale](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-type-h#oh_arkui_snapshotoptions_setscale)，[OH_ArkUI_GetNodeSnapshot](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-node-h#oh_arkui_getnodesnapshot), achieves the ForeignObject functionality . This API requires compilation in a project that supports `API15+` and must run on a ROM that supports `API15+` to take effect.
2. Version >=15.12.1 for 0.77 introduced [OH_ArkUI_CreateSnapshotOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-type-h#oh_arkui_createsnapshotoptions)，[OH_ArkUI_SnapshotOptions_SetScale](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-type-h#oh_arkui_snapshotoptions_setscale)，[OH_ArkUI_GetNodeSnapshot](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-node-h#oh_arkui_getnodesnapshot), achieves the ForeignObject functionality . This API requires compilation in a project that supports `API15+` and must run on a ROM that supports `API15+` to take effect.

## Properties

For details, see [react-native-svg](https://github.com/software-mansion/react-native-svg/blob/main/USAGE.md)

The following are the currently supported component properties：

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**Svg**: Parent component for drawing components

|        Name         |                        Description                         |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :--------------------------------------------------------: | :-------------: | :------- | :------- | :---------------- |
|        width        |                      Component width                       | number\| string | Yes      | All      | Yes               |
|       height        |                      Component height                      | number\| string | Yes      | All      | Yes               |
|       viewBox       |                     Component viewport                     |     string      | No       | All      | Yes               |
|        color        |                           Color                            |     string      | No       | All      | Yes               |
|        title        |                    Component title name                    |     string      | No       | All      | Yes               |
| preserveAspectRatio |              Whether to force unified scaling              |     string      | No       | All      | Yes               |
|        style        | Controls the visual appearance and layout of the component |     object      | No       | All      | Yes               |

**G**: A container used to group other SVG elements

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
| opacity |   Opacity   | number\| string | No       | All      | Yes               |

**Path**: Path drawing component that generates closed custom shapes based on the drawing path

|  Name   |           Description           |  Type  | Required | Platform | HarmonyOS Support |
| :-----: | :-----------------------------: | :----: | -------- | -------- | ----------------- |
|    d    | Command string for path drawing | string | Yes      | All      | Yes               |
| opacity |             Opacity             | number | No       | All      | Yes               |

**Rect**: Rectangle drawing component that generates rectangular shapes based on corner positions, width and height

|  Name   |            Description             |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :--------------------------------: | :-------------: | -------- | -------- | ----------------- |
|    x    | Translation distance on the x-axis | number\| string | No       | All      | Yes               |
|    y    | Translation distance on the y-axis | number\| string | No       | All      | Yes               |
|  width  |           Element width            | number\| string | Yes      | All      | Yes               |
| height  |           Element height           | number\| string | Yes      | All      | Yes               |
|   rx    |  Defines the radius on the x-axis  | number\| string | No       | All      | Yes               |
|   ry    |  Defines the radius on the y-axis  | number\| string | No       | All      | Yes               |
| opacity |              Opacity               | number\| string | No       | All      | Yes               |

**Image**: Image element that supports JPEG and PNG formats

> [!WARNING]
>
> Note: Image depends on SDK and ROM versions higher than Canary3 Sp2.

|        Name         |                         Description                          |               Type               | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------------------------------------------------------: | :------------------------------: | -------- | -------- | ----------------- |
|          x          |              Translation distance on the x-axis              |         number\| string          | No       | All      | Yes               |
|          y          |              Translation distance on the y-axis              |         number\| string          | No       | All      | Yes               |
|        width        |                        Element width                         |         number\| string          | Yes      | All      | Yes               |
|       height        |                        Element height                        |         number\| string          | Yes      | All      | Yes               |
|        href         |                   Image resource reference                   |         source\| string          | Yes      | All      | Yes               |
|      xlinkHref      |        Used to specify the URL of the image to embed         | RNImageProps['source'] \| string | No       | All      | Yes               |
| preserveAspectRatio | Controls how to maintain the aspect ratio of the image within the given container size |              string              | No       | All      | Yes               |
|       opacity       |                           Opacity                            |         source\| string          | No       | All      | Yes               |

**Circle**: Circle drawing component that generates circular shapes based on the center and radius

|  Name   |                   Description                    |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :----------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|    r    |                  Circle radius                   | number\| string | Yes      | All      | Yes               |
|   cx    | Translation distance of the center on the x-axis | number\| string | No       | All      | Yes               |
|   cy    | Translation distance of the center on the y-axis | number\| string | No       | All      | Yes               |
| opacity |                     Opacity                      |     number      | No       | All      | Yes               |

**Polygon**: Polygon drawing component used to create shapes with at least three sides

|  Name   |                         Description                          |      Type      | Required | Platform | HarmonyOS Support |
| :-----: | :----------------------------------------------------------: | :------------: | -------- | -------- | ----------------- |
| points  | Defines the x and y coordinates of each corner of the polygon | string\| array | Yes      | All      | Yes               |
| opacity |                           Opacity                            |     number     | No       | All      | Yes               |

**Polyline**: Polyline component used to create a trajectory composed of line segments

|  Name   |                         Description                          |      Type      | Required | Platform | HarmonyOS Support |
| :-----: | :----------------------------------------------------------: | :------------: | -------- | -------- | ----------------- |
| points  | Defines the x and y coordinates of each endpoint of the polyline | string\| array | Yes      | All      | Yes               |
| opacity |                           Opacity                            |     number     | No       | All      | Yes               |

**Defs**: A container used to group other SVG elements

> Note: This component has no Properties.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--: | :---------: | :--: | :------- | -------- | ----------------- |
|  /   |      /      |  /   | /        | All      | Yes               |

**LinearGradient**: Used to define linear gradients

|       Name        |                         Description                          |                  Type                   | Required | Platform | HarmonyOS Support |
| :---------------: | :----------------------------------------------------------: | :-------------------------------------: | -------- | -------- | ----------------- |
|        x1         |              Translation distance on the x-axis              |             number\| string             | No       | All      | Yes               |
|        y1         |              Translation distance on the y-axis              |             number\| string             | No       | All      | Yes               |
|        x2         |              Translation distance on the x-axis              |             number\| string             | No       | All      | Yes               |
|        y2         |              Translation distance on the y-axis              |             number\| string             | No       | All      | Yes               |
|   gradientUnits   | Specifies the coordinate system used by the element's Properties | 'userSpaceOnUse' \| 'objectBoundingBox' | No       | All      | Yes               |
| gradientTransform | Specifies the transformation from the element's current coordinate system to the target coordinate system |  ColumnMajorTransformMatrix \| string   | No       | All      | Yes               |

**RadialGradient**: Used to define radial gradients

> [!WARNING]
>
> Note: RadialGradient depends on SDK and ROM versions higher than Canary3 Sp2.

|       Name        |                         Description                          |                  Type                   | Required | Platform | HarmonyOS Support |
| :---------------: | :----------------------------------------------------------: | :-------------------------------------: | -------- | -------- | ----------------- |
|        fx         |           X-axis coordinate of the starting circle           |             number\| string             | No       | All      | Yes               |
|        fy         |           Y-axis coordinate of the starting circle           |             number\| string             | No       | All      | Yes               |
|        rx         |             X-axis radius of the ending ellipse              |             number\| string             | No       | All      | Yes               |
|        ry         |             Y-axis radius of the ending ellipse              |             number\| string             | No       | All      | Yes               |
|        cx         |            X-axis coordinate of the ending circle            |             number\| string             | No       | All      | Yes               |
|        cy         |            Y-axis coordinate of the ending circle            |             number\| string             | No       | All      | Yes               |
|         r         |                 Radius of the ending circle                  |             number\| string             | No       | All      | Yes               |
|   gradientUnits   | Specifies the coordinate system used by the element's Properties | 'userSpaceOnUse' \| 'objectBoundingBox' | No       | All      | Yes               |
| gradientTransform | Specifies the transformation from the element's current coordinate system to the target coordinate system |  ColumnMajorTransformMatrix \| string   | No       | All      | Yes               |

**Stop**: Defines color stops on a gradient

|    Name     |               Description               |  Type  | Required | Platform | HarmonyOS Support |
| :---------: | :-------------------------------------: | :----: | -------- | -------- | ----------------- |
|  stopColor  |             Gradient color              | string | No       | All      | Yes               |
| stopOpacity |         Gradient color opacity          | string | No       | All      | Yes               |
|   offset    | Relative position of the gradient color | string | No       | All      | Yes               |

**Mask**: Defines an alpha mask used to composite the current object onto the background

|       Name       |                         Description                          |    Type    | Required | Platform | HarmonyOS Support |
| :--------------: | :----------------------------------------------------------: | :--------: | -------- | -------- | ----------------- |
|        id        |                      Unique identifier                       |   string   | No       | All      | Yes               |
|        x         |         Horizontal coordinate of the top-left corner         | NumberProp | No       | All      | Yes               |
|        y         |          Vertical coordinate of the top-left corner          | NumberProp | No       | All      | Yes               |
|      width       |                        Element width                         | NumberProp | No       | All      | Yes               |
|      height      |                        Element height                        | NumberProp | No       | All      | Yes               |
|    maskUnits     | Defines the coordinate system used by x, y, width, height (default: objectBoundingBox; values: objectBoundingBox\|userSpaceOnUse) | TMaskUnits | No       | All      | Yes               |
| maskContentUnits | Defines the coordinate system used by the content (default: userSpaceOnUse; values: objectBoundingBox\|userSpaceOnUse) | TMaskUnits | No       | All      | Yes               |

**Use**: This element can reuse SVG elements

|   Name    |                         Description                          |      Type       | Required | Platform | HarmonyOS Support |
| :-------: | :----------------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|     x     |              Translation distance on the x-axis              | number\| string | No       | All      | Yes               |
|     y     |              Translation distance on the y-axis              | number\| string | No       | All      | Yes               |
|   width   |                        Element width                         | number\| string | No       | All      | Yes               |
|  height   |                        Element height                        | number\| string | No       | All      | Yes               |
|   href    |                   Image resource reference                   | source\| string | Yes      | All      | Yes               |
| xlinkHref | Specifies a URI pointing to an element defined in the SVG document |     string      | No       | All      | Yes               |
|  opacity  |                           Opacity                            | number\| string | No       | All      | Yes               |

**Ellipse**: Ellipse drawing component based on a center coordinate and their x-radius and y-radius

|  Name   |                   Description                    |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :----------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|   cx    | Translation distance of the center on the x-axis | number\| string | No       | All      | Yes               |
|   cy    | Translation distance of the center on the y-axis | number\| string | No       | All      | Yes               |
|   rx    |         Defines the radius on the x-axis         | number\| string | No       | All      | Yes               |
|   ry    |         Defines the radius on the y-axis         | number\| string | No       | All      | Yes               |
| opacity |                     Opacity                      | number\| string | No       | All      | Yes               |

**ClipPath**: This element defines a clipping path that can be used as the value of the clipPath Property of other elements

| Name |           Description            |  Type  | Required | Platform | HarmonyOS Support |
| :--: | :------------------------------: | :----: | -------- | -------- | ----------------- |
|  id  | Unique identifier of the element | string | No       | All      | Yes               |

**Marker**: Used to add markers to drawing components

|     Name     |                         Description                          |      Type       | Required | Platform | HarmonyOS Support |
| :----------: | :----------------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|      id      |             Assigns a unique name to the element             |     string      | Yes      | All      | Yes               |
|   viewBox    |       Position and size of the viewport in user space        |     string      | No       | All      | Yes               |
|     refX     |          X-coordinate of the marker reference point          | number\| string | No       | All      | Yes               |
|     refY     |          Y-coordinate of the marker reference point          | number\| string | No       | All      | Yes               |
| markerUnits  | Coordinate system for the markerWidth and markerHeight Properties, and the content of the marker |     string      | No       | All      | Yes               |
|    orient    | How to rotate the marker when placing it at the corresponding position on the shape |     string      | No       | All      | Yes               |
| markerWidth  | Represents the width of the viewport into which the marker is placed | number\| string | No       | All      | Yes               |
| markerHeight | Represents the height of the viewport into which the marker is placed | number\| string | No       | All      | Yes               |

**Pattern**: Used to define a graphic object that can be referenced to tile and redraw the graphic object to cover an area

|        Name         |                         Description                          |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|         id          |             Assigns a unique name to the element             |     string      | Yes      | All      | Yes               |
|          x          |          X-coordinate of the marker reference point          | number\| string | No       | All      | Yes               |
|          y          |          Y-coordinate of the marker reference point          | number\| string | No       | All      | Yes               |
|        width        | Represents the width of the viewport into which the marker is placed | number\| string | No       | All      | Yes               |
|       height        | Represents the height of the viewport into which the marker is placed | number\| string | No       | All      | Yes               |
|    patternUnits     | Indicates which coordinate system the geometric Properties of the pattern element use |     string      | No       | All      | Yes               |
| patternContentUnit  | Indicates which coordinate system the geometric Properties of the pattern element use |     string      | No       | All      | Yes               |
|  patternTransform   | Defines a list of transform definitions applied to the pattern tile |     string      | No       | All      | Yes               |
|       viewBox       | Defines the position and size of the viewport in user space  |     string      | No       | All      | Yes               |
| preserveAspectRatio | Indicates how an element with a viewBox providing a given aspect ratio must fit into a viewport with a different aspect ratio |     string      | No       | All      | Yes               |

**Symbol**: This element is used to define a graphic template object that can be instantiated by a <use> element

|        Name         |                         Description                          |  Type  | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------------------------------------------------------: | :----: | -------- | -------- | ----------------- |
|         id          |             Assigns a unique name to the element             | string | Yes      | All      | Yes               |
|       viewBox       | Defines the position and size of the viewport in user space  | string | No       | All      | Yes               |
| preserveAspectRatio | Indicates how an element with a viewBox providing a given aspect ratio must fit into a viewport with a different aspect ratio | string | No       | All      | Yes               |

**Line**: A basic SVG shape used to create a line connecting two points

|  Name   |              Description              |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :-----------------------------------: | :-------------: | -------- | -------- | ----------------- |
|   x1    | Start point of the line on the x-axis | number\| string | No       | All      | Yes               |
|   y1    | Start point of the line on the y-axis | number\| string | No       | All      | Yes               |
|   x2    |  End point of the line on the x-axis  | number\| string | No       | All      | Yes               |
|   y2    |  End point of the line on the y-axis  | number\| string | No       | All      | Yes               |
| opacity |                Opacity                | number\| string | No       | All      | Yes               |

**Text**: Draws graphic elements composed of text

|       Name        |                         Description                          |      Type       | Required | Platform | HarmonyOS Support |
| :---------------: | :----------------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|         x         |        X-coordinate of the start of the text baseline        | number\|string  | No       | All      | Yes               |
|         y         |        Y-coordinate of the start of the text baseline        | number\|string  | No       | All      | Yes               |
|        dx         | Horizontally moves the text position from the previous text element | number\|string  | No       | All      | Yes               |
|        dy         | Vertically moves the text position from the previous text element | number\| string | No       | All      | Yes               |
|      rotate       |          Direction to rotate each individual glyph           |      array      | No       | All      | Yes               |
|      opacity      |                           Opacity                            |     number      | No       | All      | Yes               |
|    inlineSize     |                 Horizontal or vertical size                  |     number      | No       | All      | No                |
| alignmentBaseline |         Specifies the alignment baseline of the text         |     string      | No       | All      | Yes               |
|   baselineShift   |              Sets vertical position adjustment               | number\| string | No       | All      | Yes               |
|   lengthAdjust    |       Adjusts text to fit specific layout constraints        |     string      | No       | All      | Yes               |
|    textLength     |       Specifies the length the text should be rendered       |     number      | No       | All      | Yes               |

**TSpan**: Draws text or sub-text within Text

|    Name    |                         Description                          |      Type       | Required | Platform | HarmonyOS Support |
| :--------: | :----------------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|     x      |        X-coordinate of the start of the text baseline        | number\|string  | No       | All      | Yes               |
|     y      |        Y-coordinate of the start of the text baseline        | number\|string  | No       | All      | Yes               |
|     dx     | Horizontally moves the text position from the previous text element | number\|string  | No       | All      | Yes               |
|     dy     | Vertically moves the text position from the previous text element | number\| string | No       | All      | Yes               |
|   rotate   |          Direction to rotate each individual glyph           |      array      | No       | All      | Yes               |
|  opacity   |                           Opacity                            |     number      | No       | All      | Yes               |
| inlineSize |                 Horizontal or vertical size                  |     number      | No       | All      | Yes               |

**TextPath**: To render text along a path shape, enclose the text in a TextPath element with an href Property and reference a Path element

|    Name     |                        Description                         |      Type       | Required | Platform | HarmonyOS Support |
| :---------: | :--------------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|    href     |   URL of the path or basic shape used to render the text   |     string      | No       | All      | No                |
|  xlinkHref  |   URL of the path or basic shape used to render the text   |     string      | No       | All      | No                |
|   method    |   Method for rendering individual glyphs along the path    |     string      | No       | All      | No                |
|   spacing   |              Spacing between drawn characters              |     string      | No       | All      | No                |
|    side     |   Which side of the path the text should be rendered on    |     string      | No       | All      | No                |
|   midLine   |                          Midline                           |     string      | No       | All      | No                |
| startOffset | Offset at which the text starts being drawn along the path | number\| string | No       | All      | No                |

**SvgAst**: This component renders SVG by passing in an AST

|   Name   |                  Description                  |  Type  | Required | Platform | HarmonyOS Support |
| :------: | :-------------------------------------------: | :----: | :------- | :------- | :---------------- |
|   ast    |   AST tree obtained by parsing SVG strings    | JsxAST | Yes      | All      | Yes               |
| override | Overrides SVG styles (e.g., width and height) | object | No       | All      | Yes               |

**SvgFromUri**: This component renders SVG by passing in a URI address

|   Name   |                  Description                  |  Type  | Required | Platform | HarmonyOS Support |
| :------: | :-------------------------------------------: | :----: | :------- | :------- | :---------------- |
|   uri    |             SVG resource address              | string | Yes      | All      | Yes               |
| override | Overrides SVG styles (e.g., width and height) | object | No       | All      | Yes               |

**SvgFromXml**: This component renders SVG by passing in a string

|   Name   |                  Description                  |  Type  | Required | Platform | HarmonyOS Support |
| :------: | :-------------------------------------------: | :----: | :------- | :------- | :---------------- |
|   xml    |              String of SVG code               | string | Yes      | All      | Yes               |
| override | Overrides SVG styles (e.g., width and height) | object | No       | All      | Yes               |

**SvgXml**: This component renders SVG by passing in a string

|   Name   |                  Description                  |  Type  | Required | Platform | HarmonyOS Support |
| :------: | :-------------------------------------------: | :----: | :------- | :------- | :---------------- |
|   xml    |              String of SVG code               | string | Yes      | All      | Yes               |
| override | Overrides SVG styles (e.g., width and height) | object | No       | All      | Yes               |

**SvgUri**: This component renders SVG by passing in a URI address

|   Name   |                  Description                  |   Type   | Required | Platform | HarmonyOS Support |
| :------: | :-------------------------------------------: | :------: | :------- | :------- | :---------------- |
|   uri    |             SVG resource address              |  string  | Yes      | All      | Yes               |
| override | Overrides SVG styles (e.g., width and height) |  object  | No       | All      | Yes               |
| onError  |              Triggered on error               | function | No       | All      | Yes               |
|  onLoad  |      Triggered after successful loading       | function | No       | All      | Yes               |
| fallback |            Element during loading             | function | No       | All      | Yes               |

**ForeignObject**: This element can nest non-SVG content into SVG

|            Name             |                 Description                 |      Type       | Required | Platform | HarmonyOS Support |
| :-------------------------: | :-----------------------------------------: | :-------------: | :------- | :------- | ----------------- |
|              x              |     Translation distance on the x-axis      | number\| string | No       | All      | Yes               |
|              y              |     Translation distance on the y-axis      | number\| string | No       | All      | Yes               |
|            width            |                Element width                | number\| string | No       | All      | Yes               |
|           height            |               Element height                | number\| string | No       | All      | Yes               |
| SvgNodeCommonProps.opacity  |                 Set opacity                 |     number      | No       | All      | Yes               |
|  SvgNodeCommonProps.matrix  |           Set transform animation           |  Array<number>  | No       | All      | Yes               |
|   SvgNodeCommonProps.mask   | Specify the Mask element for masking effect |     string      | No       | All      | Yes               |
| SvgNodeCommonProps.clipPath |    Specify and associate a clipping path    |     string      | No       | All      | Yes               |
| SvgNodeCommonProps.clipRule |              Set clipping rule              |     string      | No       | All      | Yes               |
|  SvgRenderableCommonProps   |                   Object                    |     object      | No       | All      | No                |
|     SvgGroupCommonProps     |                   Object                    |     object      | No       | All      | No                |

**Common Properties**:

Support status of Common props component Properties on the HarmonyOS side

|                  Name                  |                         Description                          |          Type          | Default   | Required | Platform |
| :------------------------------------: | :----------------------------------------------------------: | :--------------------: | --------- | :------- | :------- |
|                  fill                  |               Sets the color of the fill area                |         string         | '#000'    | No       | All      |
|              fillOpacity               |              Sets the opacity of the fill area               |         number         | 1         | No       | All      |
|                fillRule                |                      Sets the fill rule                      |         number         | 1         | No       | All      |
|                clipRule                |                    Sets the clipping rule                    |         string         | 'evenodd' | No       | All      |
|                clipPath                |           Specifies and associates a clipping path           |         string         | 'none'    | No       | All      |
|                 stroke                 |   Sets the border color (no border by default if not set)    |         string         | none      | No       | All      |
|              strokeWidth               |                    Sets the border width                     |         number         | 1         | No       | All      |
|             strokeOpacity              |                        Border opacity                        |         number         | 1         | No       | All      |
|            strokeDasharray             |      Pattern paradigm of dashed lines used for stroking      |         number         | none      | No       | All      |
|            strokeDashoffset            | Specifies the distance from the start of the path to the dash pattern |         number         | 1         | No       | All      |
|             strokeLinecap              |          Sets the shape of the two ends of the path          |         string         | 'butt'    | No       | All      |
|             strokeLinejoin             |     Indicates the shape used at the corners of the path      |         string         | 'miter'   | No       | All      |
|            strokeMiterlimit            |  Sets a limit on the ratio of miter length to stroke-width   |         number         | 4         | No       | All      |
|              vectorEffect              |  Indicates the vector effect to use when drawing the object  |         string         | none      | No       | All      |
|               translate                |                      Sets displacement                       |      numberArray       | [0,0]     | No       | All      |
|               translateX               |                   Sets x-axis displacement                   |         number         | 0         | No       | All      |
|               translateY               |                   Sets y-axis displacement                   |         number         | 0         | No       | All      |
|                 origin                 |     Changes the origin of transformation for an element      |      numberArray       | [0,0]     | No       | All      |
|                originX                 | Changes the x-coordinate of the origin of transformation for an element (invalid when used alone; must be used with other properties such as rotation) |         number         | 0         | No       | All      |
|                originY                 | Changes the y-coordinate of the origin of transformation for an element (invalid when used alone; must be used with other properties such as rotation) |         number         | 0         | No       | All      |
|                 scale                  |                   Defines the scaling size                   |      numberArray       | [1,1]     | No       | All      |
|                 scaleX                 |               Defines the x-axis scaling size                |         number         | 1         | No       | All      |
|                 scaleY                 |               Defines the y-axis scaling size                |         number         | 1         | No       | All      |
|                rotation                |                   Sets the rotation angle                    |         number         | 0         | No       | All      |
|                   x                    |               Identifies an x-axis coordinate                |         number         | 0         | No       | All      |
|                   y                    |                Identifies a y-axis coordinate                |         number         | 0         | No       | All      |
| transform<sup>changed in 15.13.0</sup> | Defines a list of transform rules applied to the element and its child elements,version code < 15.13.0,transform type is string, version code >= 15.13.0 transform type also supports arrry type. | string\|TransformArray | -         | No       | All      |
|                 marker                 |   Specifies the marker style for all vertices of the path    |         string         | -         | No       | All      |
|              markerStart               | Specifies the marker style used for the start point of the path |         string         | -         | No       | All      |
|               markerMid                | Specifies the marker style used for the middle vertices of the path |         string         | -         | No       | All      |
|               markerEnd                | Specifies the marker style used for the end point of the path |         string         | -         | No       | All      |
|                  mask                  | Specifies a mask effect for the element using the Mask element |         string         | -         | No       | All      |
|                   id                   |                       Sets the node id                       |         string         | -         | No       | All      |
|  opacity  | Sets opacity |         number         | 1         | No       | All      |
|                display                 |            Controls how the element is displayed             |         string         | 'block'   | No       | All      |
|             pointerEvents              |        Sets how the element responds to click events         |         string         |           | No       | All      |

**FontProps**: Support status of FontProps component Properties on the HarmonyOS side

|         Name          |                         Description                          |    Type    | Default | Required | Platform |
| :-------------------: | :----------------------------------------------------------: | :--------: | :------ | :------- | :------- |
|       fontSize        | Font size from baseline to baseline when setting multi-line text to solid lines in a multi-line layout environment |   string   | medium  | No       | All      |
|      fontWeight       | Thickness or lightness of the glyph used to render text relative to other fonts in the same font family |   string   | normal  | No       | All      |
|         font          |                 Sets a font for text layout                  | FontObject | none    | No       | All      |
|       fontStyle       |                Specifies text rendering style                |   string   | normal  | No       | All      |
|      fontVariant      |                    Sets text font variant                    |            |         | No       | All      |
|      fontStretch      |                 Controls font stretch degree                 |   string   | normal  | No       | All      |
|      fontFamily       |                     Specifies text font                      |   string   | normal  | No       | All      |
|      textAnchor       | Used to specify the alignment of text relative to its anchor point |   string   | start   | No       | All      |
|    textDecoration     |                 Sets text decoration effects                 |   string   | -       | No       | All      |
|     letterSpacing     |           Sets character spacing or letter spacing           |   number   | 1       | No       | All      |
|      wordSpacing      |           Sets the distance between English words            |   number   | 1       | No       | All      |
|        kerning        |             Sets the spacing between characters              |   number   | 0       | No       | All      |
|  fontFeatureSettings  |                     Font feature control                     |   string   | normal  | No       | All      |
| fontVariantLigatures  |                  Controls ligatures in text                  |   string   | normal  | No       | All      |
| fontVariationSettings |    Sets the width, height, inclination, etc., of the font    |   string   | normal  | No       | All      |

## 5. Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|         Name         |              Description              |   Type   | Required | Platform | HarmonyOS Support |
| :------------------: | :-----------------------------------: | :------: | :------: | :------: | :---------------: |
|        parse         |     Parse SVG string into JsxAST      | function |    No    |   All    |        Yes        |
| err<sup>15.0.x</sup> |               Print log               | function |    No    |   All    |        Yes        |
|      camelCase       | Capitalize the first letter of string | function |    No    |   All    |        Yes        |
|      fetchText       |     Parse SVG string into JsxAST      | function |    No    |   All    |        Yes        |

## 6.Known Issues

- [ ] isPointInFill: Determine whether the point coordinate is inside the fill area **Not implemented**
- [ ] isPointInStroke: Determine whether the point coordinate is on the stroke **Not implemented**
- [ ] getTotalLength: Get the total length of the path **Not implemented**
- [ ] getPointAtLength: Get point coordinate information at a given length along the path **Not implemented**
- [ ] getBBox: Get the bounding box information of the component **Not implemented**
- [ ] getCTM: Get the matrix information relative to the parent component **Not implemented**
- [ ] getScreenCTM: Get the screen matrix information of the component **Not implemented**
- [ ] getRawResource: Get the resource file on Android **Not implemented**
- [X] foreignObject: This component allows SVG to use external components **Implemented**
- [ ] filter: This component can apply various visual effects to SVG graphics **Not implemented**
- [ ] TextPath: Properties `href`,`xlinkHref`,`startOffset`, `method`, `spacing`, `midLine`, `side` **Not implemented**
- [ ] Text, TSpan: Properties `rotate`, `fontFamily`, `wordSpacing` **Not implemented**
- [ ] Xml: The `err` property from the community library `react-native-svg/src/ReactNativeSVG` is referenced but not exposed externally **Not implemented**[#2845](https://github.com/software-mansion/react-native-svg/pull/2845)


## 7.Others

## 8.License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-svg/blob/harmony/LICENSE).

