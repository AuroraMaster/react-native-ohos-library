> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-view-pdf</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/rumax/react-native-PDFView">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/rumax/react-native-PDFView/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-PDFView)

## Installation and Usage

Find the matching version information in the release address of a third-party library: 

| Third-party Library Version | Release Information    | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <=0.14.0-0.0.2@deprecated | [@react-native-oh-tpl/react-native-view-pdf Releases(deprecated)](https://github.com/react-native-oh-library/react-native-PDFView/releases) | 0.72       |
| 0.14.1      | [@react-native-ohos/react-native-view-pdf Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-pdfview/releases) | 0.72       |
| 0.15.0      | [@react-native-ohos/react-native-view-pdf Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-pdfview/releases) | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-view-pdf
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-view-pdf
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { View } from "react-native";
import PDFView from "react-native-view-pdf";

export function PdfViewExample() {
  return (
    <View style={{ flex: 1 }}>
      <PDFView
        style={{ flex: 1 }}
        resource="https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf"
        resourceType="url"
        onLoad={() => {}}
        onError={(error: any) => {}}
      ></PDFView>
    </View>
  );
}
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~0.15.0                              |  No                   |  0.77                |
| ~0.14.1                              |  Yes                  |  0.72                |
| <=0.14.0-0.0.2@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

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

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-view-pdf": "file:../../node_modules/@react-native-ohos/react-native-view-pdf/harmony/pdf_view.har"
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

### 3. Introducing RNPDFView Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { RNPDFView } from '@react-native-ohos/react-native-view-pdf'

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === RNPDFView.NAME) {
+   RNPDFView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ RNPDFView.NAME
  ];
```
### 4.Configure CMakeLists and introduce ViewPdfPackage

> If you are using version <=0.14.0-0.0.2, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-view-pdf/src/main/cpp" ./pdf_view)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_pdf_view)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ViewPdfPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ViewPdfPackage>(ctx),
    };
}
```

### 5. Introducing PDFViewPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { PDFViewPackage } from '@react-native-ohos/react-native-view-pdf/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new PDFViewPackage(ctx)
  ];
}
```
</details>

## Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

The following combinations have been verified:

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name              | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| resource          | A resource to render. It's possible to render PDF from file, url (should be encoded) or base64 | string   | yes      | all      | yes               |
| resourceType      | Should correspond to resource and can be: file, url or base64 | string   | no       | all      | yes               |
| fileFrom          | iOS: In case if resourceType is set to file, there are different way to search for it on iOS file system. Currently documentsDirectory, libraryDirectory, cachesDirectory, tempDirectory and bundle are supported. <br>harmony: files, cache, temp | string   | no       | iOS      | yes               |
| onLoad            | Callback that is triggered when loading is completed         | function | no       | all      | yes               |
| onError           | Callback that is triggered when loading has failed. And error is provided as a function parameter | style    | no       | all      | yes               |
| style             | css style                                                    | string   | no       | all      | yes               |
| fadeInDuration    | Fade in duration (in ms, defaults to 0.0) to smoothly fade the webview into view when pdf loading is completed | number   | no       | all      | yes               |
| enableAnnotations | Android ONLY: Boolean to enable Android view annotations (default is false). | boolean  | no       | Android  | no                |
| urlProps          | Extended properties for url type that allows to specify HTTP Method, HTTP headers and HTTP body | map      | no       | all      | no                |
| onPageChanged     | Callback that is invoked when page is changed. Provides active page and total pages information | function | no       | Android  | no                |
| onScrolled        | Callback that is invoked when PDF is scrolled. Provides offset value in a range between 0 and 1. Currently only 0 and 1 are supported. | function | no       | all      | no                |

### Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name   | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ------ | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| reload | Allows to reload the PDF document. This can be useful in such cases as network issues, document is expired, etc. To reload the document you will need a `ref` to the component: | function | yes      | all      | yes               |

## Known Issues

- [ ] The urlProps property is not supported. The native HarmonyOS component WebView does not support urlProps.[issue: #5](https://github.com/react-native-oh-library/react-native-PDFView/issues/5)
- [ ] The onScrolled property is not supported. The onScrolled callback function is not executed when the native HarmonyOS component webview loads a PDF file. [issue: #6](https://github.com/react-native-oh-library/react-native-PDFView/issues/6)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/rumax/react-native-PDFView/blob/master/LICENSE).
