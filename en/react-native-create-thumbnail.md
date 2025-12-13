> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-create-thumbnail</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/souvik-ghosh/react-native-create-thumbnail">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/souvik-ghosh/react-native-create-thumbnail/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-create-thumbnail)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                     | Supported RN Version |
|-------| ------------------------------------------------------------ | ---------- |
| <= 2.0.0-0.0.4@deprecated | [@react-native-oh-tpl/react-native-create-thumbnail Releases(deprecated)](https://github.com/react-native-oh-library/react-native-create-thumbnail/releases) | 0.72       |
| 2.0.1 | [@react-native-ohos/react-native-create-thumbnail Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-create-thumbnail/releases)                        | 0.72       |
| 2.1.0 | [@react-native-ohos/react-native-create-thumbnail Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-create-thumbnail/releases)                        | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-create-thumbnail
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-create-thumbnail
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```js
import React, {useState } from 'react';
import {  StyleSheet, Text, Button ,ScrollView,View} from 'react-native';
import { createThumbnail } from 'react-native-create-thumbnail';

export default function CreateThumbnailDemo() {

  const [text, setText] = useState('');

  const CreateThumbnail = async()=> {
    let obj = await createThumbnail({ 
      url:'https://media.w3.org/2010/05/sintel/trailer.mp4',
      timeStamp: 10000
    });
    setText(JSON.stringify(obj))
  }

  return (
    <View style={styles.container}>
      <View style={styles.titleArea}>
        <Text style = {styles.title}>Math</Text>
      </View>
      <View style = {styles.inputArea}>
        <Text style={styles.baseText}>
          {text}
        </Text>
      </View>
      <ScrollView style={styles.scrollView}>
        <View style={ { flexDirection: 'column'}}>
          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>createThumbnail</Text>
             <Button title='Running' color='#841584' onPress={CreateThumbnail}></Button>
          </View>
    
        </View>
      </ScrollView>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: '100%',
    height: '100%',
    flexDirection: 'column',
    alignItems: 'center',
    backgroundColor: '#F1F3F5',
  }, 
  baseText: {
    fontWeight: 'bold',
    textAlign:'center',
    fontSize:16
  },

  titleArea:{
    width:'90%',
    height:'8%',
    alignItems:'center',
    flexDirection:'row',
  },

  title: {
    width:'90%',
    color:'#000000',
    textAlign:'left',
    fontSize: 30,
  },

  scrollView: {
    width:'90%',
    marginHorizontal: 20,
  },

  inputArea: {
    width:'90%',
    height:'30%',
    borderWidth:2,
    borderColor:'#000000',
    marginTop:8,
    justifyContent:'center',
    alignItems:'center',
  },
  baseArea: {
    width:'100%',
    height:60,
    borderRadius:4,
    borderColor:'#000000',
    marginTop:8,
    backgroundColor:'#FFFFFF',
    flexDirection: 'row',
    alignItems:'center',
    paddingLeft:8,
    paddingRight:8
  }
});
```

## Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~2.1.0                               |  No                   |  0.77                |
| ~2.0.1                               |  Yes                  |  0.72                |
| <= 2.0.0-0.0.4@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md.

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
    "@react-native-ohos/react-native-create-thumbnail": "file:../../node_modules/@react-native-ohos/react-native-create-thumbnail/harmony/createThumbnail.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] The source code is located in the harmony folder within the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-create-thumbnail": "file:../../node_modules/@react-native-ohos/react-native-create-thumbnail/harmony/createThumbnail"
  }
```

run the following instruction on the terminal:

```bash
cd entry
ohpm install --no-link
```

### 3.Configure CMakeLists and include CreateThumbnailPackage

> If you are using version <= 2.0.0-0.0.4, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-create-thumbnail/src/main/cpp" ./create-thumbnail)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_create_thumbnail)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "CreateThumbnailPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<CreateThumbnailPackage>(ctx),
    };
}
```

### 4. Introducing BlobUtilPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { CreateThumbnailPackage } from '@react-native-ohos/react-native-create-thumbnail/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new CreateThumbnailPackage(ctx)
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

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### **createThumbnail**
| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- |
|  createThumbnail    | thumbnail generator with storage/cache management and support for both local and remote videos  | function | NO | yes |

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|        Name         | Description  |   type   | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------: | :------: | :------: | :---------------: | :---------------: |
|  url | Path to video file (local or remote)   |    String    | yes  |   Android/ios    |    yes    |
|  timeStamp | Thumbnail timestamp (in milliseconds)   |    Number     | NO  |   Android/ios    |    yes    |
|  format | Thumbnail format, can be one of: jpeg, or png   |    String      | NO  |   Android/ios    |    yes    |
|  dirSize | Maximum size of the cache directory (in megabytes). When this directory is full, the previously generated thumbnails will be deleted to clear about half of it's size.   |    Number       | NO  |   Android/ios    |    yes    |
|  headers | Headers to load the video with. e.g. { Authorization: 'someAuthToken' }   |    Object      | NO  |   Android/ios    |    yes    |
|  cacheName | Cache name for this thumbnail to avoid duplicate generation. If specified, and a thumbnail already exists with the same cache name, it will be returned instead of generating a new one.   |    String     | NO  |   Android/ios    |    yes    |
## Return Value

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|        Name         | Description  |   type   | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------: | :------: | :------: | :---------------: | :---------------: |
|  path | Path to generated thumbnail   |    String    | NO  |   Android/ios    |    yes    |
|  size | Size (in bytes) of thumbnail   |    Number     | NO  |   Android/ios    |    yes    |
|  mime | Mimetype of thumbnail   |    String    | NO  |   Android/ios    |    yes    |
|  width | Thumbnail width   |    Number     | NO  |   Android/ios    |    yes    |
|  height | Thumbnail height   |    Number     | NO  |   Android/ios    |    yes    |



## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/souvik-ghosh/react-native-create-thumbnail/blob/master/LICENSE).
