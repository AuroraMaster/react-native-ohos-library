> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-doc-viewer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/philipphecht/react-native-doc-viewer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/philipphecht/react-native-doc-viewer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-doc-viewer)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information:

| Third-party Library Version | Release Information                                                                                                                              | Supported RN Version |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| 2.7.8@deprecated            | [@react-native-oh-tpl/react-native-doc-viewer Releases(deprecated)](https://github.com/react-native-oh-library/react-native-doc-viewer/releases) | 0.72       |
| 2.7.9                       | [@react-native-ohos/react-native-doc-viewer Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-doc-viewer/releases)                | 0.72       |
| 2.8.0                       | [@react-native-ohos/react-native-doc-viewer Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-doc-viewer/releases)                | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-doc-viewer
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-doc-viewer
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from 'react';
import {
  AppRegistry,
  StyleSheet,
  Text,
  View,
  Platform,
  Button,
  Alert,
  ActivityIndicator,
  NativeAppEventEmitter,
  DeviceEventEmitter,
  NativeModules,
  NativeEventEmitter,
  TouchableHighlight
} from 'react-native';
import OpenFile from 'react-native-doc-viewer';
var RNFS = require('react-native-fs');
var SavePath = Platform.OS === 'ios' ? RNFS.MainBundlePath : RNFS.DocumentDirectoryPath;
export default class DocumentViewerExample extends Component {
 constructor(props) {
    super(props);
    this.state = {
      animating: false,
      progress: "",
      donebuttonclicked: false,
    }
    this.eventEmitter = new NativeEventEmitter(NativeModules.RNReactNativeDocViewer);
    this.eventEmitter.addListener('DoneButtonEvent', (data) => {
      /*
      *Done Button Clicked
      * return true
      */
      console.log(data.close);
      this.setState({donebuttonclicked: data.close});
    })
  }

  componentDidMount(){
    // download progress
    this.eventEmitter.addListener(
      'RNDownloaderProgress',
      (Event) => {
        console.log("Progress - Download "+Event.progress  + " %")
        this.setState({progress: Event.progress + " %"});
      }

    );
  }

  componentWillUnmount (){
    this.eventEmitter.removeListener();
  }
  /*
  * Handle WWW File Method
  * fileType Default == "" you can use it, to set the File Extension (pdf,doc,xls,ppt etc) when in the Url the File Extension is missing.
  */
  handlePress = () => {
    this.setState({animating: true});
    if(Platform.OS === 'ios'){
      OpenFile.openDoc([{
        url:"https://calibre-ebook.com/downloads/demos/demo.docx",
        fileNameOptional:"test filename"
      }], (error, url) => {
         if (error) {
          this.setState({animating: false});
         } else {
          this.setState({animating: false});
           console.log(url)
         }
       })
    }else{
      this.setState({animating: true});
      OpenFile.openDoc([{
        url:"https://www.huf-haus.com/fileadmin/Bilder/Header/ART_3/Header_HUF_Haus_ART_3___1_.jpg", // Local "file://" + filepath
        fileName:"sample",
        cache:false,
        fileType:"jpg"
      }], (error, url) => {
         if (error) {
          this.setState({animating: false});
           console.error(error);
         } else {
          this.setState({animating: false});
           console.log(url)
         }
       })
    }

  }


  /*
  * Handle Local File Method
  * fileType Default == "" you can use it, to set the File Extension (pdf,doc,xls,ppt etc) when in the Url the File Extension is missing.
  */
  handlePressLocal = () => {
    this.setState({animating: true});
    if(Platform.OS === 'ios'){
        OpenFile.openDoc([{url:SavePath+"/react-native-logo.jpg",
        fileNameOptional:"test filename"
      }], (error, url) => {
         if (error) {
          this.setState({animating: false});
         } else {
          this.setState({animating: false});
           console.log(url)
         }
       })
    }else{
      OpenFile.openDoc([{url:SavePath+"/demo.jpg",
        fileName:"sample",
        cache:false,
        fileType:"jpg"
      }], (error, url) => {
         if (error) {
          this.setState({animating: false});
         } else {
          this.setState({animating: false});
           console.log(url)
         }
       })

    }
  }

    handlePressLocalXLS = () => {
      this.setState({animating: true});
      if(Platform.OS === 'ios'){
          OpenFile.openDoc([{url:SavePath+"/SampleXLSFile_19kb.xls",
          fileNameOptional:"Sample XLS 94-2003"
        }], (error, url) => {
           if (error) {
            this.setState({animating: false});
           } else {
            this.setState({animating: false});
             console.log(url)
           }
         })
      }else{
        OpenFile.openDoc([{url:SavePath+"/demo.jpg",
          fileName:"sample",
          cache:false,
          fileType:"jpg"
        }], (error, url) => {
           if (error) {
            this.setState({animating: false});
           } else {
            this.setState({animating: false});
             console.log(url)
           }
         })

      }
    }


  /*
  * Binary in URL
  * Binary String in Url
  * fileType Default == "" you can use it, to set the File Extension (pdf,doc,xls,ppt etc) when in the Url you dont have an File Extensions
  */
  handlePressBinaryinUrl = () => {
    this.setState({animating: true});
    if(Platform.OS === 'ios'){
      OpenFile.openDocBinaryinUrl([{
        url:"https://storage.googleapis.com/need-sure/example",
        fileName:"sample",
        fileType:"xml"
      }], (error, url) => {
          if (error) {
            console.error(error);
            this.setState({animating: false});
          } else {
            console.log(url)
            this.setState({animating: false});
          }
        })
    }else{
      OpenFile.openDocBinaryinUrl([{
        url:"https://storage.googleapis.com/need-sure/example",
        fileName:"sample",
        fileType:"xml",
        cache:true
      }], (error, url) => {
          if (error) {
            console.error(error);
            this.setState({animating: false});
          } else {
            console.log(url)
            this.setState({animating: false});
          }
        })
    }
  }

  /*
  * Base64String
  * put only the base64 String without data:application/octet-stream;base64
  * fileType Default == "" you can use it, to set the File Extension (pdf,doc,xls,ppt etc) when in the Url you dont have an File Extensions
  */
  handlePressb64 = () => {
    if(Platform.OS === 'ios'){
      OpenFile.openDocb64([{
        base64:"{BASE64String}",
        fileName:"sample",
        fileType:"png"
      }], (error, url) => {
          if (error) {
            console.error(error);
          } else {
            console.log(url)
          }
        })
    }else{
      OpenFile.openDocb64([{
        base64:"{BASE64String}",
        fileName:"sample",
        fileType:"png",
        cache:true
      }], (error, url) => {
          if (error) {
            console.error(error);
          } else {
            console.log(url)
          }
        })
    }
  }

    /*
  * Video File
  */
  handlePressVideo = () => {
    if(Platform.OS === 'ios'){
      OpenFile.playMovie(video, (error, url) => {
                if (error) {
                    console.error(error);
                } else {
                    console.log(url)
                }
            })
    }else{
      Alert.alert("Android coming soon");
    }
  }
  render() {
    return (<View style={{paddingTop: 100}}>
    
        <Button
          onPress={this.handlePress.bind(this)}
          title="Press Me Open Doc Url"
          accessibilityLabel="See a Document"
        />
        <Button
          onPress={this.handlePressBinaryinUrl.bind(this)}
          title="Press Me Open BinaryinUrl"
          accessibilityLabel="See a Document"
        />
         <Button
          onPress={this.handlePressLocal.bind(this)}
          title="Press Me Open Doc Path"
          accessibilityLabel="See a Document"
        />
        <Button
          onPress={this.handlePressLocalXLS.bind(this)}
          title="Press Me Open XLS DOC Path"
          accessibilityLabel="See a Document"
        />
        <Button
          onPress={this.handlePressb64.bind(this)}
          title="Press Me Open Base64 String"
          accessibilityLabel="See a Document"
        />
        <Button
          onPress={()=>this.handlePressVideo("http://www.sample-videos.com/video/mp4/720/big_buck_bunny_720p_1mb.mp4")}
          title="Press Me Open Video"
          accessibilityLabel="See a Document"
        />
    </View>)
  }


}
```

## Use Codegen

Version >= @react-native-ohos/react-native-doc-viewer@2.7.9, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-viewer@2.7.9 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks. Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

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

1. Use the HAR file(recommended)；
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-doc-viewer": "file:../../node_modules/@react-native-ohos/react-native-doc-viewer/harmony/doc_viewer.har"
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

### 3.Introducing DocViewPackage Component to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { DocViewPackage } from "@react-native-ohos/react-native-doc-viewer/ts"

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new DocViewPackage(ctx)
  ];
}
```

### 4. Running

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

The following combinations have been verified:

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                | Type     | Required | Platform | HarmonyOS Support |
| ------------------ | -------------------------- | -------- | -------- | -------- | ----------------- |
| openDoc            | open a online document     | function | no       | All      | yes               |
| openDocBinaryinUrl | open a online document     | function | no       | All      | yes               |
| openDocb64         | open base64 string as document | function | no       | All      | yes               |

## Known Issues

## License

This project is licensed under [The MIT License (MIT)](https://github.com/philipphecht/react-native-doc-viewer/blob/master/LICENSE)