> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-syan-image-picker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/syanbo/react-native-syan-image-picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/syanbo/react-native-syan-image-picker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-syan-image-picker) 

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.5.3@deprecated  | [@react-native-oh-tpl/react-native-syan-image-picker Releases(deprecated)](https://github.com/react-native-oh-library/react-native-syan-image-picker/releases) | 0.72       |
| 0.5.4             | [@react-native-ohos/react-native-syan-image-picker Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-syan-image-picker/releases)   | 0.72       |
| 0.6.0             | [@react-native-ohos/react-native-syan-image-picker Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-syan-image-picker/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-syan-image-picker
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-syan-image-picker
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:
Create an imagePicker.js file

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import {
  StyleSheet,
  View,
  Image,
  ScrollView,
  Dimensions,
  Button
} from 'react-native';
import RNCVideo from 'react-native-video';
import SYImagePicker, { SelectedPhoto } from "react-native-syan-image-picker";

const {width} = Dimensions.get('window');

interface State {
  photos: SelectedPhoto[]
  video: SelectedPhoto[]
}

interface ItemType {
  height: number,
  original_uri: string,
  size: number,
  width: number,
  uri: string,
}

export default class App extends React.Component<{}, State> {
  constructor(props: any) {
    super(props);
    this.state = {
      photos: [],
      video: [],
    };
  }
  /**
  * Enable compression. Select a photo to crop and compress, and enable Base64 encoding.
  **/
  handleOpenImagePicker = () => {
    SYImagePicker.showImagePicker(
        {
            isCamera: true,
            imageCount: 1, // Cropping can be enabled only when **imageCount** is set to **1**.
            quality: 10,
            compress: true, // Enable compression.
            enableBase64: true,
            isCrop: true,
        }, (err, photos) => {
            if (!err) {
                this.setState({video: []});
                this.setState({
                    photos: photos,
                });
                {photos.map((item, index) => {
                        console.log("rn_syan_image_picker showImagePicker result: ",
                            "uri:" + item.uri + "-- " +
                            "width:" + item.width + "-- " +
                            "height:" + item.height + "-- " +
                            "type:" + item.type + "-- " +
                            "size:" + item.size + "-- " +
                            "original_uri:" + item.original_uri + "-- " +
                            "base64:" + item.base64 + "-- ");
                    })
                }
            } else {
                console.log(err);
            }
        },
    );
  };
  handleOpenImagePicker1 = () => {
    SYImagePicker.showImagePicker(
        {
            isCamera: true,
            imageCount: 1,
            quality: 90,
            compress: true,
            enableBase64: true,
            isCrop: true,
        }, (err, photos) => {
            if (!err) {
                this.setState({video: []});
                this.setState({
                    photos: photos,
                });
                {photos.map((item, index) => {
                    console.log("rn_syan_image_picker showImagePicker result: ",
                        "uri:" + item.uri + "-- " +
                        "width:" + item.width + "-- " +
                        "height:" + item.height + "-- " +
                        "type:" + item.type + "-- " +
                        "size:" + item.size + "-- " +
                        "original_uri:" + item.original_uri + "-- " +
                        "base64:" + item.base64 + "-- ");
                })
                }
            } else {
                console.log(err);
            }
        },
    );
  };
  /**
   * Disable compression. Select multiple photos and enable Base64 encoding.
   **/
  handleAsyncSelectPhoto = async () => {
    SYImagePicker.removeAllPhoto()
    try {
      const photos = await SYImagePicker.asyncShowImagePicker({
        imageCount: 8, // Set the number of photos to select.
        enableBase64: true, // Enable Base64 encoding.
      });
      // The selection is successful.
      this.setState({
        photos: [...this.state.photos, ...photos],
      });
    } catch (err) {
      console.log(err);
      // Cancel selection. The value of err.message is "Cancelled".
    }
  };
  /**
  * Clear cache.
  **/
  handleDeleteCache = () => {
    SYImagePicker.deleteCache();
  };

  /**
  * Delete the first image using the index
  **/
  handleRemoveAtIndex=()=>{
    const {photos} = this.state;
    if(!!photos && photos.length > 0){
        SYImagePicker.removePhotoAtIndex(0);
    }
  };

  /**
  * Remove all selected photos.
  **/
  handleRemoveAll=()=>{
    SYImagePicker.removeAllPhoto();
  };

  /**
  * Take a photo
  **/
  handleLaunchCamera = async () => {
    SYImagePicker.openCamera(
        {isCrop: true, showCropCircle: true, showCropFrame: false, videoMaximumDuration: 5},
        (err, photos) => {
            if (!err) {
                this.setState({video: []});
                this.setState({
                    photos: photos,
                });
                {photos.map((item, index) => {
                        console.log("rn_syan_image_picker handleLaunchCamera result: ",
                            "uri:" + item.uri + "-- " +
                            "width:" + item.width + "-- " +
                            "height:" + item.height + "-- " +
                            "type:" + item.type + "-- " +
                            "size:" + item.size + "-- " +
                            "original_uri:" + item.original_uri + "-- " +
                            "base64:" + item.base64 + "-- ");
                    })
                }
            }
        },
    );
  };

  /**
  * Select videos.
  **/
  handleOpenVideoPicker = () => {
    SYImagePicker.openVideoPicker(
        {allowPickingMultipleVideo: true, videoCount: 10},
        (err, res) => {
            if (!err) {
                this.setState({photos: []});
                this.setState({
                    video: res,
                });
                {res.map((item, index) => {
                    console.log("rn_syan_image_picker handleOpenVideoPicker result: ",
                        "uri:" + item.uri + "-- " +
                        "width:" + item.width + "-- " +
                        "height:" + item.height + "-- " +
                        "type:" + item.type + "--" +
                        "size:" + item.size + "-- " +
                        "original_uri:" + item.original_uri + "-- " +
                        "base64:" + item.base64 + "-- ");
                })}
            }
        },
    );
  };

  render() {
    const { photos } = this.state;
    const { video } = this.state; 
    return (
      <View style={{marginTop: 100}}>
         <Button title={'Enable compression(quality=10)'} onPress={this.handleOpenImagePicker}/>
         <Button title={'Enable compression(quality=90)'} onPress={this.handleOpenImagePicker1}/>
         <Button title={'Clear cache'} onPress={this.handleDeleteCache}/>
         <Button title={'Delete the first image using the index'} onPress={this.handleRemoveAtIndex}/>
         <Button title={'Remove all selected photos'} onPress={this.handleRemoveAll}/>
         <Button title={'Take a photo'} onPress={this.handleLaunchCamera}/>
         <Button title={'Select videos'} onPress={this.handleOpenVideoPicker}/>
         <ScrollView contentContainerStyle={styles.scroll}>
            {video.map((item: ItemType, index: number) => {
              const videoSource = {
                uri: item.uri, isNetwork: false
              };
              return (
                <RNCVideo
                  style={styles.video}
                  source={videoSource}>
                </RNCVideo>
              );
            })}
                
            {photos.map((item: ItemType, index: number) => {
              let source = {uri: item.original_uri};
                return (
                  <Image
                   key={`image-${index}`}
                   style={styles.image}
                   source={source}
                   resizeMode={'contain'}
                  />
                );
              })
            }
         </ScrollView>
      </View>
    )
  }
}

const styles = StyleSheet.create({
    scroll: {
        padding: 5,
        flexWrap: 'wrap',
        flexDirection: 'row',
    },
    image: {
        margin: 10,
        width: (width - 80) / 3,
        height: (width - 80) / 3,
        backgroundColor: '#F0F0F0',
    },
    video: {
        margin: 10,
        width: (width - 80) / 3,
        height: (width - 80) / 4,
    }
});

```

## Use Codegen

Version >= @react-native-ohos/react-native-syan-image-picker@0.5.4, compatible with codegen-lib for generating bridge code.

This repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-syan-image-picker@0.5.4 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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

### 2.Configure Entry

**(1)Create ImageCropAbility.ets under entry/src/main/ets/entryability**

```
import UIAbility from '@ohos.app.ability.UIAbility'
import window from '@ohos.window'

const TAG = 'ImageEditAbility';

export default class ImageCropAbility extends UIAbility {

  onWindowStageCreate(windowStage: window.WindowStage) {
    this.setWindowOrientation(windowStage, window.Orientation.PORTRAIT)
    windowStage.loadContent('pages/ImageEdit', (err, data) => {
      if (err.code) {
        console.info(TAG,'Failed to load the content. Cause: %{public}s',
          JSON.stringify(err) ?? '')
        return;
      }
      console.info(TAG,'Succeeded in loading the content')
    });
    try {
      windowStage.getMainWindowSync().setWindowLayoutFullScreen(true, (err)=>{
        if (err.code) {
          console.error('Failed to enable the full-screen mode. Cause: ' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in enabling the full-screen mode.');
      })
    } catch (exception) {
      console.error('Failed to set the system bar to be invisible. Cause: ' + JSON.stringify(exception));
    }
  }

  setWindowOrientation(stage: window.WindowStage, orientation: window.Orientation): void {
    console.info(TAG,"into setWindowOrientation :")
    if (!stage || !orientation) {
      return;
    }
    stage.getMainWindow().then(windowInstance => {
      windowInstance.setPreferredOrientation(orientation);
    })
  }

  onBackground() {
    this.context.terminateSelf();
  }
}
```

**(2)Register ImageCropAbility.ets in entry/src/main/module.json5.**

```
"abilities":[{
        "name": "ImageCropAbility",
        "srcEntry": "./ets/entryability/ImageCropAbility.ets",
        "description": "$string:EntryAbility_desc",
        "icon": "$media:icon",
        "startWindowIcon": "$media:startIcon",
        "startWindowBackground": "$color:start_window_background",
        "removeMissionAfterTerminate": true,

}
...
]

```

**(3)Create ImageEdit.ets under entry/src/main/ets/pages.**

```
import { ImageCrop } from '@react-native-ohos/react-native-syan-image-picker';

@Entry
@Component
struct ImageEdit {

 build() {
  Row(){
   Column(){
    ImageCrop();
   }
   .width('100%')
  }
  .height('100%')
 }
}
```

**(4)Add configuration in entry/src/main/resources/base/profile/main_pages.json.**

```
{
 "src": [
  "pages/Index",
  "pages/ImageEdit"
 ]
}
```

### 3. Introducing Native Code

Currently, two methods are available:


Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-syan-image-picker": "file:../../node_modules/@react-native-ohos/react-native-syan-image-picker/harmony/syan_image_picker.har"
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

### 4. Introducing SyanImagePickerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+   import {SyanImagePickerPackage} from '@react-native-ohos/react-native-syan-image-picker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SyanImagePickerPackage(ctx)
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

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified successfully in the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 5.1.0.150 (API Version 12); IDE: DevEco Studio 5.1.1.830; ROM: 5.1.0.150;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 5.0.0.71(API Version 12 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 5.1.0.150;



## ImagePickerOption(Configuration Options for Selecting Photos or Data)
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                            | Description                                                  | Type    | Required |  Platform   | HarmonyOS Support |
| ------------------------------- | ------------------------------------------------------------ | ------- | :------: | :---------: | :---------------: |
| imageCount                      | Maximum number of photos that can be selected. The default value is **6**.                                     | number  |   yes    | iOS/Android |        yes        |
| isCamera                        | Whether the user is allowed to take a photo using the built-in camera. The default value is **true**.                            | boolean |   yes    | iOS/Android |        yes        |
| isCrop                          | Whether to allow cropping. The default value is **false**. This option is valid only when **imageCount** is set to **1**.               | boolean |   yes    | iOS/Android |        yes        |
| compress                        | Whether to compress photos.                                                | boolean |   yes    | iOS/Android |        yes        |
| quality                         | Compression quality.                                                    | number  |   yes    | iOS/Android |        yes        |
| enableBase64                    | Whether to return Base64 encoding. Disabled by default.                              | boolean |   yes    | iOS/Android |        yes        |
| videoCount                      | Number of selected videos.                                              | number  |   yes    | iOS/Android |        yes        |
| allowPickingMultipleVideo       | Whether to allow selecting multiple videos.                                            | boolean |   yes    | iOS/Android |        yes        |
| isRecordSelected                | Whether a photo is selected.                                                | bool    |   yes    | iOS/Android |        yes        |
| CropW                           | Cropping width. The default value is 60% of the screen width.                                   | number  |   yes    | iOS/Android |        yes        |
| CropH                           | Cropping height. The default value is 60% of the screen height.                                   | number  |   yes    | iOS/Android |        yes        |
| isGif                           | Whether to allow selecting GIFs. The default value is **false** and no callback for GIF data is provided.                 | boolean |   yes    | iOS/Android |        no         |
| showCropCircle                  | Whether to display a circular cropping area. The default value is **false**.                             | boolean |   yes    | iOS/Android |        yes        |
| circleCropRadius                | Cropping radius of a circle. The default value is half of the screen width.                              | number  |   yes    | iOS/Android |        yes        |
| showCropFrame                   | Whether to display the cropping area. The default value is **true**.                                  | boolean |   yes    |   Android   |        no         |
| showCropGrid                    | Whether to hide the cropping area. The default value is **false**.                             | boolean |   yes    |   Android   |        no         |
| freeStyleCropEnabled            | Whether the cropping frame can be dragged.                                            | boolean |   yes    |   Android   |        no         |
| rotateEnabled                   | Whether to allow rotating the photo when it is being cropped.                                          | boolean |   yes    |   Android   |        no         |
| scaleEnabled                    | Whether to allow scaling the photo when it is being cropped.                                      | boolean |   yes    |   Android   |        no         |
| compressFocusAlpha              | Whether to preserve image opacity during compression. (Enabling this will increase the size of the PNG image after compression, but the opacity will be retained.)| boolean |   yes    | iOS/Android |        no         |
| minimumCompressSize             | Minimum size for compressing. Photos smaller than 100 KB are not compressed (Android).                            | number  |   yes    |   Android   |        no         |
| allowPickingOriginalPhoto       | Whether to allow selecting native photos.                                                | boolean |   yes    | iOS/Android |        yes        |
| MaxSecond                       | Maximum video duration. The default value is 180 seconds.                               | number  |   yes    |   Android   |        no         |
| videoMaximumDuration            | Maximum video shooting duration, in seconds. The default value is 10 minutes.                    | number  |   yes    | iOS/Android |        yes        |
| isWeChatStyle                   | Whether the WeChat style is used for the selection screen (Android only).                         | boolean |   yes    |   Android   |        no         |
| sortAscendingByModificationDate | Whether to sort photos by modification time in ascending order. The default value is **YES**. If it is set to **NO**, the latest photo will be displayed first, and the built-in camera button will be placed at the top.| boolean |   yes    | iOS/Android |        no         |
| MinSecond                       | Minimum video duration. The default value is 1 second.                                 | number  |   yes    |   Android   |        no         |
| showSelectedIndex               | Whether to display the sequence number. By default, the sequence number is not displayed.                                   | boolean |   yes    | iOS/Android |        no         |

## SelectedPhoto（Returned Result of the Selected Photo or Video）
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name         | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| width        | Photo width.                                                    | number | yes      | iOS/Android | yes               |
| height       | Photo height.                                                    | number | yes      | iOS/Android | yes               |
| original_uri | Original photo path.                                                | string | yes      | iOS/Android | yes               |
| uri          | Photo path.                                                    | string | yes      | iOS/Android | yes               |
| type         | File type.                                                    | string | yes      | iOS/Android | yes               |
| size         | Photo size, in bytes.                                      | number | yes      | iOS/Android | yes               |
| base64       | Base64 encoding of a photo, which is not returned if **enableBase64** is set to **false**.| string | yes      | iOS/Android | yes               |

## API
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                        | Type                                                     | Required | Platform    | HarmonyOS Support |
| -------------------- | ---------------------------------- | -------------------------------------------------------- | -------- | ----------- | ----------------- |
| showImagePicker      | Opens the image picker and selects photos.          | callback: (err: null \| string, photos: SelectedPhoto[]) | yes      | iOS/Android | yes               |
| asyncShowImagePicker | Opens the image picker and selects photos.          | Promise<SelectedPhoto[]>                                 | yes      | iOS/Android | yes               |
| openCamera           | Opens the camera to take a photo or select a photo.| callback: (err: null \| string, photos: SelectedPhoto[]) | yes      | iOS/Android | yes               |
| asyncOpenCamera      | Opens the camera to take a photo or select a photo.| Promise<SelectedPhoto[]>                                 | yes      | iOS/Android | yes               |
| deleteCache          | Clears cache.                          | void                                                     | yes      | iOS/Android | yes               |
| removePhotoAtIndex   | Removes the index of the selected photo.              | void                                                     | yes      | iOS/Android | yes               |
| removeAllPhoto       | Removes all selected photos.              | void                                                     | yes      | iOS/Android | yes               |
| openVideoPicker      | Opens the video picker and selects videos.           | callback: (err: null \| string, photos: SelectedPhoto[]) | yes      | iOS/Android | yes               |

## Known Issues

- [] isRecordSelected: whether a photo is selected [issues#2](https://github.com/react-native-oh-library/react-native-syan-image-picker/issues/2)
- [] isGif: whether to allow selecting GIFs [issues#5](https://github.com/react-native-oh-library/react-native-syan-image-picker/issues/5)
- [] compressFocusAlpha: whether to preserve image opacity during compression [issues#13](https://github.com/react-native-oh-library/react-native-syan-image-picker/issues/13)
- [ ] sortAscendingByModificationDate: whether to sort photos by modification time in ascending order [issues#19](https://github.com/react-native-oh-library/react-native-syan-image-picker/issues/19)
- [ ] showSelectedIndex: whether to display the sequence number [issues#21](https://github.com/react-native-oh-library/react-native-syan-image-picker/issues/21)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/syanbo/react-native-syan-image-picker/blob/master/LICENSE).
