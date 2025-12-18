>模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-image-crop-picker</code> </h1>
</p>

> [!Tip] [Github 地址](https://github.com/react-native-oh-library/react-native-image-crop-picker)

## 1.安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                     | 支持RN版本 |
|--------| ------------------------------------------------------------ | ---------- |
| <= 0.40.3-0.0.14@deprecated | [@react-native-oh-tpl/react-native-image-crop-picker Releases(deprecated)](https://github.com/react-native-oh-library/react-native-image-crop-picker/releases) | 0.72       |
| 0.40.5 | [@react-native-ohos/react-native-image-crop-picker Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-crop-picker/releases)                        | 0.72       |
| 0.50.2  | [@react-native-ohos/react-native-image-crop-picker Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-crop-picker/releases)                        | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-image-crop-picker
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-image-crop-picker
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!TIP] 使用时 import 的库名不变。

```
import ImagePicker from 'react-native-image-crop-picker';
import { openPicker } from 'react-native-image-crop-picker';
import React from 'react';
import { Text, StyleSheet, TextInput, View, Button, ScrollView, Switch } from 'react-native';

const ImageCropPickDemo = () => {
  const TAG: string = 'ImageCropPickerTurboModule';
  const [maxFiles, setMaxFiles] = React.useState('');
  const [imageQuality, setImageQuality] = React.useState('');
  const [imagePath, setImagePath] = React.useState('');
  const [clearImagePath, setClearImagePath] = React.useState('');
  const [cropperTitle, setCropperTitle] = React.useState('');
  const [chooseText, setChooseText] = React.useState('');
  const [chooseColor, setChooseColor] = React.useState('');
  const [cancelText, setCancelText] = React.useState('');
  const [cancelColor, setCancelColor] = React.useState('');
  const [cropperRotate, setCropperRotate] = React.useState(false);
  const [showCropGuidelines, setShowCropGuidelines] = React.useState(true);
  const [showCropFrame, setShowCropFrame] = React.useState(true);
  const [multiple, setMultiple] = React.useState(false);
  const [includeExif, setIncludeExif] = React.useState(false);
  const [avoidEmptySpace, setAvoidEmptySpace] = React.useState(false);
  const [writeTempFile, setTempFile] = React.useState(true);
  const [includeBase64, setBase64] = React.useState(false);
  const [freeStyleCropEnabled, setFreeStyleCropEnabled] = React.useState(false);
  const [cropperCircleOverlay, setCropperCircleOverlay] = React.useState(false);
  const [forceJpg, setForceJpg] = React.useState(false);
  const [showsSelectedCount, setShowsSelectedCount] = React.useState(true);
  const [selectedButton, setSelectedButton] = React.useState('any');
  const [useFrontCamera, setUseFrontCamera] = React.useState(false);
  const [croppingCamera, setCroppingCamera] = React.useState(false);
  const [writeTempFileCamera, setTempFileCamera] = React.useState(true);
  const [includeBase64Camera, setBase64Camera] = React.useState(false);
  const [includeExifCamera, setIncludeExifCamera] = React.useState(false);
  const [avoidEmptySpaceCamera, setAvoidEmptySpaceCamera] = React.useState(false);
  const [freeStyleCropEnabledCamera, setFreeStyleCropEnabledCamera] = React.useState(false);
  const [forceJpgCamera, setForceJpgCamera] = React.useState(false);
  const [mediaTypeCamera, setMediaTypeCamera] = React.useState('any');
  const [imageQualityCamera, setImageQualityCamera] = React.useState('');
  const [cropperTitleCamera, setCropperTitleCamera] = React.useState('');
  const [chooseTextCamera, setChooseTextCamera] = React.useState('');
  const [chooseColorCamera, setChooseColorCamera] = React.useState('');
  const [cancelTextCamera, setCancelTextCamera] = React.useState('');
  const [cancelColorCamera, setCancelColorCamera] = React.useState('');
  const [cropperRotateCamera, setCropperRotateCamera] = React.useState(false);
  const [showCropGuidelinesCamera, setShowCropGuidelinesCamera] = React.useState(true);
  const [showCropFrameCamera, setShowCropFrameCamera] = React.useState(true);
  const [writeTempFileCropper, setTempFileCropper] = React.useState(true);
  const [forceJpgCropper, setForceJpgCropper] = React.useState(false);
  const [includeBase64Cropper, setBase64Cropper] = React.useState(false);
  const [includeExifCropper, setIncludeExifCropper] = React.useState(false);
  const [avoidEmptySpaceCropper, setAvoidEmptySpaceCropper] = React.useState(false);
  const [freeStyleCropEnabledCropper, setFreeStyleCropEnabledCropper] = React.useState(false);
  const [imageQualityCropper, setimageQualityCropper] = React.useState('');

  const handleButtonPress = (buttonName: any) => {
    setSelectedButton(buttonName);
  };

  const handleMediaType = (buttonName: any) => {
    setMediaTypeCamera(buttonName);
  };

  return (
    <ScrollView style={styles.container}>
      <Text style={styles.title}>Camera, Gallery, Cropping Functionality</Text>
      <View style={styles.container}>

        <View style={styles.TextInputBox}>

          <Text style={styles.inputLable}>multiple:</Text>
          <Button
            title={`${multiple}`}
            onPress={() => multiple ? setMultiple(false) : setMultiple(true)}
          />

          <Text style={styles.inputLable}>writeTempFile:</Text>
          <Button
            title={`${writeTempFile}`}
            onPress={() => writeTempFile ? setTempFile(false) : setTempFile(true)}
          />
        </View>

        <View style={styles.TextInputBox}>

          <Text style={styles.inputLable}>includeBase64:</Text>
          <Button
            title={`${includeBase64}`}
            onPress={() => includeBase64 ? setBase64(false) : setBase64(true)}
          />

          <Text style={styles.inputLable}>includeExif:</Text>
          <Button
            title={`${includeExif}`}
            onPress={() => includeExif ? setIncludeExif(false) : setIncludeExif(true)}
          />

        </View>

        <View style={styles.TextInputBox}>

          <Text style={styles.inputLable}>avoidEmptySpaceAroundImage :</Text>
          <Button
            title={`${avoidEmptySpace}`}
            onPress={() => avoidEmptySpace ? setAvoidEmptySpace(false) : setAvoidEmptySpace(true)}
          />

        </View>

        <View style={styles.TextInputBox}>

          <Text style={styles.inputLable}>freeStyleCropEnabled :</Text>
          <Button
            title={`${freeStyleCropEnabled}`}
            onPress={() => freeStyleCropEnabled ? setFreeStyleCropEnabled(false) : setFreeStyleCropEnabled(true)}
          />

        </View>

        <View style={styles.TextInputBox}>

          <Text style={styles.inputLable}>forceJpg:</Text>
          <Button
            title={`${forceJpg}`}
            onPress={() => forceJpg ? setForceJpg(false) : setForceJpg(true)}
          />

          <Text style={styles.inputLable}>showsSelectedCount:</Text>
          <Button
            title={`${showsSelectedCount}`}
            onPress={() => showsSelectedCount ? setShowsSelectedCount(false) : setShowsSelectedCount(true)}
          />

        </View>


        <View style={styles.TextInputBox}>
          <Text style={styles.inputLable}>mediaType:</Text>
          <Button
            title='photo'
            onPress={() => handleButtonPress('photo')}
            accessibilityState={{ selected: selectedButton === 'photo' }}
          />
          <Button
            title='video'
            onPress={() => handleButtonPress('video')}
            accessibilityState={{ selected: selectedButton === 'video' }}
          />
          <Button
            title='any'
            onPress={() => handleButtonPress('any')}
            accessibilityState={{ selected: selectedButton === 'any' }}
          />
        </View>
        <View style={styles.TextInputBox}>
          <Text style={{ color: 'red' }}>mediaType is {selectedButton}</Text>
        </View>

        <View style={styles.TextInputBox}>
          <Text style={styles.inputLable}>minFiles:</Text>
          <Text style={styles.inputLable}>1</Text>
        </View>

        <View style={styles.TextInputBox}>
          <Text style={styles.inputLable}>maxFiles:</Text>
          <TextInput
            keyboardType="numeric"
            maxLength={1}
            style={styles.numberInput}
            onChangeText={setMaxFiles}
            value={maxFiles}
          />
          <Text style={styles.lableType}>(number)</Text>
        </View>

        <View style={styles.TextInputBox}>
          <Text style={styles.inputLable}>compressImageQuality:</Text>
          <TextInput
            style={styles.numberInput}
            onChangeText={setImageQuality}
            value={imageQuality}
          />
          <Text style={styles.lableType}>(0.1 到 1)</Text>
        </View>

        <View >
          <View style={styles.buttonSty}>
            <Button
              title='openPicker'
              onPress={() => {
                openPicker({
                  multiple: multiple,
                  writeTempFile: writeTempFile,
                  includeBase64: includeBase64,
                  includeExif: includeExif,
                  avoidEmptySpaceAroundImage: avoidEmptySpace,
                  freeStyleCropEnabled: freeStyleCropEnabled,
                  forceJpg: forceJpg,
                  showsSelectedCount: showsSelectedCount,
                  mediaType: selectedButton,
                  minFiles: 1,
                  maxFiles: maxFiles,
                  compressImageQuality: imageQuality,
                }).then((image: any) => {
                  console.log(TAG + ' openPicker result ' + JSON.stringify(image))
                });
              }}
            />
          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>cropping:</Text>
            <Button
              title={`${croppingCamera}`}
              onPress={() => croppingCamera ? setCroppingCamera(false) : setCroppingCamera(true)}
            />

            <Text style={styles.inputLable}>writeTempFile:</Text>
            <Button
              title={`${writeTempFileCamera}`}
              onPress={() => writeTempFileCamera ? setTempFileCamera(false) : setTempFileCamera(true)}
            />

          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>includeBase64:</Text>
            <Button
              title={`${includeBase64Camera}`}
              onPress={() => includeBase64Camera ? setBase64Camera(false) : setBase64Camera(true)}
            />

            <Text style={styles.inputLable}>includeExif:</Text>
            <Button
              title={`${includeExifCamera}`}
              onPress={() => includeExifCamera ? setIncludeExifCamera(false) : setIncludeExifCamera(true)}
            />

          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>avoidEmptySpaceAroundImage :</Text>
            <Button
              title={`${avoidEmptySpaceCamera}`}
              onPress={() => avoidEmptySpaceCamera ? setAvoidEmptySpaceCamera(false) : setAvoidEmptySpaceCamera(true)}
            />

          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>freeStyleCropEnabled :</Text>
            <Button
              title={`${freeStyleCropEnabledCamera}`}
              onPress={() => freeStyleCropEnabledCamera ? setFreeStyleCropEnabledCamera(false) : setFreeStyleCropEnabledCamera(true)}
            />

          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>useFrontCamera:</Text>
            <Button
              title={`${useFrontCamera}`}
              onPress={() => useFrontCamera ? setUseFrontCamera(false) : setUseFrontCamera(true)}
            />

            <Text style={styles.inputLable}>forceJpg:</Text>
            <Button
              title={`${forceJpgCamera}`}
              onPress={() => forceJpgCamera ? setForceJpgCamera(false) : setForceJpgCamera(true)}
            />
          </View>

          <View style={styles.TextInputBox}>
            <Text style={styles.inputLable}>mediaType:</Text>
            <Button
              title='photo'
              onPress={() => handleMediaType('photo')}
              accessibilityState={{ selected: mediaTypeCamera === 'photo' }}
            />
            <Button
              title='video'
              onPress={() => handleMediaType('video')}
              accessibilityState={{ selected: mediaTypeCamera === 'video' }}
            />
            <Button
              title='any'
              onPress={() => handleMediaType('any')}
              accessibilityState={{ selected: mediaTypeCamera === 'any' }}
            />
          </View>
          <View style={styles.TextInputBox}>
            <Text style={{ color: 'red' }}>mediaType is {mediaTypeCamera}</Text>
          </View>

          <View style={styles.TextInputBox}>
            <Text style={styles.inputLable}>compressImageQuality:</Text>
            <TextInput
              style={styles.numberInput}
              onChangeText={setImageQualityCamera}
              value={imageQualityCamera}
            />
            <Text style={styles.lableType}>(0.1 to 1)</Text>
          </View>

          <View style={styles.TextInputBox}>
            <Text style={styles.textLable}>cropperToolbarTitle:</Text>
          </View>

          <View style={styles.TextInputBox}>

            <TextInput
              style={styles.textInput}
              maxLength={5}
              onChangeText={(value: any) => setCropperTitleCamera(value)}
              value={cropperTitleCamera}
            />
          </View>

          <View style={styles.TextInputBox}>
            <Text style={styles.textLable}>cropperChooseText:</Text>
          </View>

          <View style={styles.TextInputBox}>

            <TextInput
              style={styles.textInput}
              maxLength={5}
              onChangeText={(value: any) => setChooseTextCamera(value)}
              value={chooseTextCamera}
            />
          </View>

          <View style={styles.TextInputBox}>
            <Text style={styles.textLable}>cropperChooseColor:#FF0000</Text>
          </View>

          <View style={styles.TextInputBox}>

            <TextInput
              style={styles.textInput}
              maxLength={7}
              onChangeText={(value: any) => setChooseColorCamera(value)}
              value={chooseColorCamera}
            />
          </View>

          <View style={styles.TextInputBox}>
            <Text style={styles.textLable}>cropperCancelText:</Text>
          </View>

          <View style={styles.TextInputBox}>

            <TextInput
              style={styles.textInput}
              maxLength={5}
              onChangeText={(value: any) => setCancelTextCamera(value)}
              value={cancelTextCamera}
            />
          </View>

          <View style={styles.TextInputBox}>
            <Text style={styles.textLable}>cropperCancelColor: #FF0000</Text>
          </View>

          <View style={styles.TextInputBox}>

            <TextInput
              style={styles.textInput}
              maxLength={7}
              onChangeText={(value: any) => setCancelColorCamera(value)}
              value={cancelColorCamera}
            />
          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>cropperRotateButtonsHidden:</Text>
            <Button
              title={`${cropperRotateCamera}`}
              onPress={() => cropperRotateCamera ? setCropperRotateCamera(false) : setCropperRotateCamera(true)}
            />
          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>showCropGuidelines:</Text>
            <Button
              title={`${showCropGuidelinesCamera}`}
              onPress={() => showCropGuidelinesCamera ? setShowCropGuidelinesCamera(false) : setShowCropGuidelinesCamera(true)}
            />
          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>showCropFrame:</Text>
            <Button
              title={`${showCropFrameCamera}`}
              onPress={() => showCropFrameCamera ? setShowCropFrameCamera(false) : setShowCropFrameCamera(true)}
            />
          </View>

          <View style={styles.buttonSty}>
            <Button
              title="openCamera"
              onPress={() => {
                ImagePicker.openCamera({
                  cropping: croppingCamera,
                  writeTempFile: writeTempFileCamera,
                  includeBase64: includeBase64Camera,
                  includeExif: includeExifCamera,
                  avoidEmptySpaceAroundImage: avoidEmptySpaceCamera,
                  freeStyleCropEnabled: freeStyleCropEnabledCamera,
                  useFrontCamera: useFrontCamera,
                  forceJpg: forceJpgCamera,
                  mediaType: mediaTypeCamera,
                  compressImageQuality: imageQualityCamera,
                  cropperToolbarTitle: cropperTitleCamera,
                  cropperChooseText: chooseTextCamera,
                  cropperChooseColor: chooseColorCamera,
                  cropperCancelText: cancelTextCamera,
                  cropperCancelColor: cancelColorCamera,
                  cropperRotateButtonsHidden: cropperRotateCamera,
                  showCropGuidelines: showCropGuidelinesCamera,
                  showCropFrame: showCropFrameCamera,
                }).then((image: any) => {
                  console.log(TAG + ' openCamera result ' + JSON.stringify(image))
                });
              }}
            />
          </View>

          <View style={styles.TextInputBox}>
            <Text style={styles.textLable}>Please enter the address of the image that needs to be cropped:</Text>
          </View>

          <View style={styles.TextInputBox}>

            <TextInput
              style={styles.textInput}
              onChangeText={(value: any) => setImagePath(value)}
              value={imagePath}
            />

          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>writeTempFile:</Text>
            <Button
              title={`${writeTempFileCropper}`}
              onPress={() => writeTempFileCropper ? setTempFileCropper(false) : setTempFileCropper(true)}
            />

            <Text style={styles.inputLable}>forceJpg:</Text>
            <Button
              title={`${forceJpgCropper}`}
              onPress={() => forceJpgCropper ? setForceJpgCropper(false) : setForceJpgCropper(true)}
            />
          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>includeBase64:</Text>
            <Button
              title={`${includeBase64Cropper}`}
              onPress={() => includeBase64Cropper ? setBase64Cropper(false) : setBase64Cropper(true)}
            />

            <Text style={styles.inputLable}>includeExif:</Text>
            <Button
              title={`${includeExifCropper}`}
              onPress={() => includeExifCropper ? setIncludeExifCropper(false) : setIncludeExifCropper(true)}
            />

          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>avoidEmptySpaceAroundImage :</Text>
            <Button
              title={`${avoidEmptySpaceCropper}`}
              onPress={() => avoidEmptySpaceCropper ? setAvoidEmptySpaceCropper(false) : setAvoidEmptySpaceCropper(true)}
            />

          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>freeStyleCropEnabled :</Text>
            <Button
              title={`${freeStyleCropEnabledCropper}`}
              onPress={() => freeStyleCropEnabledCropper ? setFreeStyleCropEnabledCropper(false) : setFreeStyleCropEnabledCropper(true)}
            />

          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>cropperCircleOverlay :</Text>
            <Button
              title={`${cropperCircleOverlay}`}
              onPress={() => cropperCircleOverlay ? setCropperCircleOverlay(false) : setCropperCircleOverlay(true)}
            />

          </View>

          <View style={styles.TextInputBox}>
            <Text style={styles.inputLable}>compressImageQuality:</Text>
            <TextInput
              style={styles.numberInput}
              onChangeText={setimageQualityCropper}
              value={imageQualityCropper}
            />
            <Text style={styles.lableType}>(0.1 to 1)</Text>
          </View>


          <View style={styles.TextInputBox}>
            <Text style={styles.textLable}>cropperToolbarTitle:</Text>
          </View>

          <View style={styles.TextInputBox}>

            <TextInput
              style={styles.textInput}
              maxLength={5}
              onChangeText={(value: any) => setCropperTitle(value)}
              value={cropperTitle}
            />
          </View>

          <View style={styles.TextInputBox}>
            <Text style={styles.textLable}>cropperChooseText:</Text>
          </View>

          <View style={styles.TextInputBox}>

            <TextInput
              style={styles.textInput}
              maxLength={5}
              onChangeText={(value: any) => setChooseText(value)}
              value={chooseText}
            />
          </View>

          <View style={styles.TextInputBox}>
            <Text style={styles.textLable}>cropperChooseColor:#FF0000</Text>
          </View>

          <View style={styles.TextInputBox}>

            <TextInput
              style={styles.textInput}
              maxLength={7}
              onChangeText={(value: any) => setChooseColor(value)}
              value={chooseColor}
            />
          </View>

          <View style={styles.TextInputBox}>
            <Text style={styles.textLable}>cropperCancelText:</Text>
          </View>

          <View style={styles.TextInputBox}>

            <TextInput
              style={styles.textInput}
              maxLength={5}
              onChangeText={(value: any) => setCancelText(value)}
              value={cancelText}
            />
          </View>

          <View style={styles.TextInputBox}>
            <Text style={styles.textLable}>cropperCancelColor:#FF0000</Text>
          </View>

          <View style={styles.TextInputBox}>

            <TextInput
              style={styles.textInput}
              maxLength={7}
              onChangeText={(value: any) => setCancelColor(value)}
              value={cancelColor}
            />
          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>cropperRotateButtonsHidden:</Text>
            <Button
              title={`${cropperRotate}`}
              onPress={() => cropperRotate ? setCropperRotate(false) : setCropperRotate(true)}
            />
          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>showCropGuidelines:</Text>
            <Button
              title={`${showCropGuidelines}`}
              onPress={() => showCropGuidelines ? setShowCropGuidelines(false) : setShowCropGuidelines(true)}
            />
          </View>

          <View style={styles.TextInputBox}>

            <Text style={styles.inputLable}>showCropFrame:</Text>
            <Button
              title={`${showCropFrame}`}
              onPress={() => showCropFrame ? setShowCropFrame(false) : setShowCropFrame(true)}
            />
          </View>



          <View style={styles.buttonSty}>
            <Button
              title='openCropper'
              onPress={() => {

                ImagePicker.openCropper({
                  path: imagePath,
                  width: 300,
                  height: 400,
                  writeTempFile: writeTempFileCropper,
                  includeBase64: includeBase64Cropper,
                  includeExif: includeExifCropper,
                  avoidEmptySpaceAroundImage: avoidEmptySpaceCropper,
                  freeStyleCropEnabled: freeStyleCropEnabledCropper,
                  compressImageQuality: imageQualityCropper,
                  forceJpg: forceJpgCropper,
                  cropperCircleOverlay: cropperCircleOverlay,
                  cropperToolbarTitle: cropperTitle,
                  cropperChooseText: chooseText,
                  cropperChooseColor: chooseColor,
                  cropperCancelText: cancelText,
                  cropperCancelColor: cancelColor,
                  cropperRotateButtonsHidden: cropperRotate,
                  showCropGuidelines: showCropGuidelines,
                  showCropFrame: showCropFrame,
                }).then(((image: any) => {
                  console.log(TAG + ' openCropper result ' + JSON.stringify(image))
                }))
              }}
            />
          </View>

        </View>
      </View>

      <Text style={styles.title}> Delete File</Text>

      <View style={styles.buttonBox}>
        <View style={styles.buttonSty}>
          <Button
            title='clean'
            onPress={() => {
              ImagePicker.clean({}).then((image: any) => {
                console.log(TAG + ' clean result ' + JSON.stringify(image))
              });
            }}
          />
        </View>

        <View style={styles.TextInputBox}>
          <Text style={styles.textLable}>Please enter the address of the image that needs to be cleared:</Text>
        </View>

        <View style={styles.TextInputBox}>

          <TextInput
            style={styles.textInput}
            onChangeText={(value: any) => setClearImagePath(value)}
            value={clearImagePath}
          />
        </View>

        <View style={styles.buttonSty}>
          <Button
            title='cleanSingle'
            onPress={() => {
              console.log(TAG + " cleanSingle path " + clearImagePath)
              ImagePicker.cleanSingle('/data/storage/el2/base/haps/entry/temp/rn_image_crop_picker_lib_temp_' + clearImagePath).then((image: any) => {

              })
            }}
          />
        </View>

        <View style={styles.emptyView}></View>

      </View>

    </ScrollView>
  );
}
const styles = StyleSheet.create({
  container: {
  },
  TextInputBox: {
    flexDirection: 'row',
    alignItems: 'center',
    margin: 10,
  },
  textLable: {
    width: '100%'
  },
  emptyView: {
    width: 50,
    height: 500
  },
  inputLable: {
    width: 'auto'
  },
  lableType: {
    width: '18%'
  },
  numberInput: {
    width: 50,
    height: 30,
    color: 'black',
    borderColor: 'gray',
    borderWidth: 1
  },
  textInput: {
    width: '50%',
    height: 36,
    color: 'black',
    borderColor: 'gray',
    bordeWidth: 1
  },
  switchType: {
    width: 60,
    height: 36
  },
  buttonBox: {
    marginTop: 20,
  },
  buttonSty: {
    marginTop: 0,
    marginRight: 60,
    marginBottom: 20,
    marginLeft: 60,
    textAlign: 'center'
  },
  title: {
    fontWeight: '500',
    fontSize: 20,
    marginTop: 10,
  }
});
export default ImageCropPickDemo;
```

## 2. Link

|                             | 是否支持autolink | RN框架版本 |
|-----------------------------|-----------------|------------|
| ~0.50.2                     |  No              |  0.77     |
| ~0.40.5                     |  Yes             |  0.72     |
| <= 0.40.3-0.0.14@deprecated |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1 在工程根目录的 `oh-package.json5` 添加 overrides 字段

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
  }
}
```

### 2.2 引入原生端代码

目前有两种方法：

- 通过 har 包引入（推荐）
- 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-image-crop-picker": "file:../../node_modules/@react-native-ohos/react-native-image-crop-picker/harmony/image_crop_picker.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/link-source-code.md)

### 2.3 配置 CMakeLists 和引入 ImageCropPickerPackage

> 若使用的是 <= 0.40.3-0.0.14 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-image-crop-picker/src/main/cpp" ./image-crop-picker)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
+  ${IMAGE_CROP_PICKER_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_image_crop_picker)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ImageCropPickerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ImageCropPickerPackage>(ctx),
    };
}
```

### 2.4 在 ArkTs 侧引入 ImageCropPickerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { ImageCropPickerPackage } from '@react-native-ohos/react-native-image-crop-picker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ImageCropPickerPackage(ctx),
  ];
}
```

</details>

## 3. 必要的配置项

> [!TIP] 该模块的内容无法通过autolink自动生成，始终需要手动配置。

### 配置Entry(该模块始终需要手动配置)

**(1)在 entry/src/main/ets/entryability 下创建 ImageEditAbility.ets**

```
import UIAbility from '@ohos.app.ability.UIAbility'
import window from '@ohos.window'
import { BusinessError } from "@ohos.base";

const TAG = 'ImageEditAbility';

export default class ImageEditAbility extends UIAbility {

  onWindowStageCreate(windowStage: window.WindowStage) {
    this.setWindowOrientation(windowStage, window.Orientation.PORTRAIT)
    windowStage.loadContent('pages/ImageEdit', (err, data) => {
      let windowClass: window.Window = windowStage.getMainWindowSync()
      let isLayoutFullScreen = true
      windowClass.setWindowLayoutFullScreen(isLayoutFullScreen).then(() => {
        console.info('Succeeded in setting the window layout to full-screen mode.')
      }).catch((err: BusinessError) => {
       console.error(`Failed to set the window layout to full-screen mode. Code is ${err.code}, message is ${err.message}`)
      })

      let type = window.AvoidAreaType.TYPE_NAVIGATION_INDICATOR;
      let avoidArea = windowClass.getWindowAvoidArea(type);
      let bottomRectHeight = avoidArea.bottomRect.height; // 获取到导航区域的高度
      AppStorage.setOrCreate('bottomRectHeight', bottomRectHeight);

      type = window.AvoidAreaType.TYPE_SYSTEM;
      avoidArea = windowClass.getWindowAvoidArea(type);
      let topRectHeight = avoidArea.topRect.height; // 获取状态栏区域高度
      AppStorage.setOrCreate('topRectHeight', topRectHeight);

      windowClass.on('avoidAreaChange', (data) => {
        if (data.type === window.AvoidAreaType.TYPE_SYSTEM) {
          let topRectHeight = data.area.topRect.height;
          AppStorage.setOrCreate('topRectHeight', topRectHeight);
        } else if (data.type == window.AvoidAreaType.TYPE_NAVIGATION_INDICATOR) {
          let bottomRectHeight = data.area.bottomRect.height;
          AppStorage.setOrCreate('bottomRectHeight', bottomRectHeight);
        }
      });

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

**(2)在 entry/src/main/module.json5 注册 ImageEditAbility**

```
"abilities":[
    ...
+    {
+        "name": "ImageEditAbility",
+        "srcEntry": "./ets/entryability/ImageEditAbility.ets",
+        "description": "$string:EntryAbility_desc",
+        "icon": "$media:icon",
+        "startWindowIcon": "$media:startIcon",
+        "startWindowBackground": "$color:start_window_background",
+        "removeMissionAfterTerminate": true,
+ }

]

```

**(3)在 entry/src/main/ets/pages 下创建 ImageEdit.ets**

```
import { ImageEditInfo } from '@react-native-ohos/react-native-image-crop-picker';
import { CircleImageInfo } from '@react-native-ohos/react-native-image-crop-picker';
@Entry
@Component
struct ImageEdit {
  @State cropperCircleOverlay: boolean = false;

  aboutToAppear(): void {
    this.cropperCircleOverlay = AppStorage.Get('cropperCircleOverlay') || false
  }

  build() {
    Row() {
      Column() {
        if(!this.cropperCircleOverlay){
          ImageEditInfo()
        } else {
          CircleImageInfo()
        }
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

**(4)在 entry/src/main/resources/base/profile/main_pages.json 添加配置**

```
{
 "src": [
  "pages/Index",
  "pages/ImageEdit"
 ]
}
```

## 4. 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```
cd entry
ohpm install
```

然后编译、运行即可。

## 5. 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 6. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name        | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| openPicker  | 调用带裁剪功能的单图选择器                                   | function | no       | iOS/Android | yes               |
| clean       | 模块会生成临时图片，这些图片将在后续自动清理。若需强制清理，可使用 `clean` 方法清除所有临时文件，或通过 `cleanSingle(path)` 方法删除单个临时文件。 | function | no       | iOS/Android | yes               |
| openCropper | 裁剪图片并支持旋转                                           | function | no       | iOS/Android | yes               |
| cleanSingle | 删除单个缓存文件                                             | function | no       | iOS/Android | yes               |
| openCamera  | 从相机选择图片                                               | function | no       | iOS/Android | yes               |

## 7. 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**裁剪配置项**

| Name                                      | Type                                                         | Description                                                  | Required | Platform | HarmonyOS Support |
| ----------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| cropping                                  | bool (default false)                                         | 启用或禁用裁剪功能                                           | no       | All      | yes               |
| width                                     | number                                                       | 启用 `cropping` 选项时，结果图片的宽度                       | no       | All      | yes               |
| height                                    | number                                                       | 启用 `cropping` 选项时，结果图片的高度                       | no       | All      | yes               |
| multiple                                  | bool (default false)                                         | 启用或禁用多图选择功能                                       | no       | All      | yes               |
| writeTempFile (iOS only)                  | bool (default true)                                          | 设为 false 时，不会为选中的图片生成临时文件。当你使用 `includeBase64` 选项获取文件内容且无需从磁盘读取文件时，此设置可提升性能。 | no       | iOS      | yes               |
| includeBase64                             | bool (default false)                                         | 设为 true 时，图片文件内容将以 Base64 编码字符串的形式存在于 `data` 属性中。 提示：若要将此字符串用作图片源，可按以下方式使用：`<Image source={{uri: `data:image.mime;base64,𝑖𝑚𝑎𝑔𝑒.𝑚𝑖𝑚𝑒;𝑏𝑎𝑠𝑒64,{image.data}`}} />` | no       | All      | yes               |
| includeExif                               | bool (default false)                                         | 在响应中包含图片的 EXIF 数据                                 | no       | All      | yes               |
| avoidEmptySpaceAroundImage (iOS only)     | bool (default true)                                          | 设为 true 时，图片将始终填充遮罩区域。                       | no       | iOS      | no                |
| cropperActiveWidgetColor (Android only)   | string (default `"#424242"`)                                 | 裁剪图片时，指定活动组件（ActiveWidget）的颜色。             | no       | Android  | no                |
| cropperStatusBarColor (Android only)      | string (default `#424242`)                                   | 裁剪图片时，指定状态栏（StatusBar）的颜色。                  | no       | Android  | no                |
| cropperToolbarColor (Android only)        | string (default `#424242`)                                   | 裁剪图片时，指定工具栏（Toolbar）的颜色。                    | no       | Android  | no                |
| cropperToolbarWidgetColor (Android only)  | string (default `darker orange`)                             | 裁剪图片时，指定工具栏文本和按钮的颜色。                     | no       | Android  | no                |
| freeStyleCropEnabled                      | bool (default false)                                         | 允许用户自定义裁剪区域的矩形范围                             | no       | All      | yes               |
| cropperToolbarTitle                       | string (default `Edit Photo`)                                | 裁剪图片时，指定工具栏的标题。                               | no       | All      | yes               |
| cropperCircleOverlay                      | bool (default false)                                         | 启用或禁用圆形裁剪遮罩。                                     | no       | All      | yes                |
| disableCropperColorSetters (Android only) | bool (default false)                                         | 裁剪图片时，禁用裁剪库的颜色设置功能。                       | no       | Android  | no                |
| minFiles (iOS only)                       | number (default 1)                                           | 启用 `multiple` 选项时，最少选择的文件数量                   | no       | iOS      | no                |
| maxFiles (iOS only)                       | number (default 5)                                           | 启用 `multiple` 选项时，最多选择的文件数量                   | no       | iOS      | yes               |
| waitAnimationEnd (iOS only)               | bool (default true)                                          | 当视图控制器（ViewController）的 `completion` 回调块被调用后，Promise 才会解析 / 拒绝 | no       | iOS      | no                |
| smartAlbums (iOS only)                    | array ([supported values](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Fivpusic%2Freact-native-image-crop-picker%2Fblob%2Fmaster%2FREADME.md%23smart-album-types-ios)) (default ['UserLibrary', 'PhotoStream', 'Panoramas', 'Videos', 'Bursts']) | 可选择的智能相册列表                                         | no       | iOS      | no                |
| useFrontCamera                            | bool (default false)                                         | 打开相机时是否默认使用前置 / 自拍相机。请注意，并非所有 Android 设备都支持此参数，详见 [issue #1058](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Fivpusic%2Freact-native-image-crop-picker%2Fissues%2F1058) | no       | All      | yes               |
| compressVideoPreset (iOS only)            | string (default MediumQuality)                               | 选择视频压缩所使用的预设参数                                 | no       | iOS      | no                |
| compressImageMaxWidth                     | number (default none)                                        | 选择视频压缩所使用的预设参数                                 | no       | All      | no                |
| compressImageMaxHeight                    | number (default none)                                        | 按最大高度压缩图片                                           | no       | All      | no                |
| compressImageQuality                      | number (default 1 (Android)/0.8 (iOS))                       | 按指定质量压缩图片（取值范围 0-1，1 为最佳质量）。 在 iOS 上，大多数图片的质量值超过 0.8 后，视觉上的质量提升并不明显；而 0.8 的质量值相比 1 可将文件大小减少约一半或更多。 | no       | All      | yes               |
| loadingLabelText (iOS only)               | string (default "Processing assets...")                      | 选择器中图片加载时显示的文本                                 | no       | iOS      | no                |
| mediaType                                 | string (default any)                                         | 图片选择支持的媒体类型，可选值为：'photo'（照片）、'video'（视频）或 'any'（任意） | no       | All      | yes               |
| showsSelectedCount (iOS only)             | bool (default true)                                          | 是否显示已选中的资源数量                                     | no       | iOS      | no                |
| sortOrder (iOS only)                      | string (default 'none', supported values: 'asc', 'desc', 'none') | 打开图片选择器时，按创建日期对相册 / 图片详情视图中的媒体资源进行排序 | no       | iOS      | no                |
| forceJpg (iOS only)                       | bool (default false)                                         | 是否将照片转换为 JPG 格式。此设置也会将所有实况照片（Live Photo）转换为对应的 JPG 格式 | no       | iOS      | yes               |
| showCropGuidelines (Android only)         | bool (default true)                                          | 裁剪过程中是否在图片上方显示 3x3 网格线                      | no       | Android  | yes               |
| showCropFrame (Android only)              | bool (default true)                                          | 裁剪过程中是否显示裁剪框                                     | no       | Android  | yes               |
| hideBottomControls (Android only)         | bool (default false)                                         | 是否显示底部控制栏                                           | no       | Android  | no                |
| enableRotationGesture (Android only)      | bool (default false)                                         | 是否允许通过手势旋转图片                                     | no       | Android  | yes               |
| cropperChooseText (iOS only)              | string (default choose)                                      | 确认选择按钮的文本                                           | no       | iOS      | yes               |
| cropperChooseColor (iOS only)             | string (default `#FFCC00`)                                   | 确认选择按钮的十六进制颜色值。 [默认颜色由 TOCropViewController 控制](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2FTimOliver%2FTOCropViewController%2Fblob%2Fa942414508012b13102f776eb65dac655f31cabb%2FObjective-C%2FTOCropViewController%2FViews%2FTOCropToolbar.m%23L444). | no       | iOS      | yes               |
| cropperCancelText (iOS only)              | string (default Cancel)                                      | 取消按钮的文本                                               | no       | iOS      | yes               |
| cropperCancelColor (iOS only)             | string (default tint `iOS` color )                           | 默认值为 iOS 系统默认的 tint 颜色，[由 TOCropViewController 控制](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2FTimOliver%2FTOCropViewController%2Fblob%2Fa942414508012b13102f776eb65dac655f31cabb%2FObjective-C%2FTOCropViewController%2FViews%2FTOCropToolbar.m%23L433) | no       | iOS      | yes               |
| cropperRotateButtonsHidden (iOS only)     | bool (default false)                                         | 启用或禁用裁剪器的旋转按钮                                   | no       | iOS      | yes               |

## 8. 遗留问题

- [ ] react-native-image-crop-picker 图像将始终填充蒙版空间 [#4](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/4)
- [ ] Android Demo中 ActiveWidget 改变颜色 [#5](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/5)
- [ ] Android Demo中 改变状态栏颜色 [#6](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/6)
- [ ] Android Demo中 改变工具栏颜色 [#7](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/7)
- [ ] 裁剪图像时，禁用裁剪库的颜色设置器 [#8](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/8)
- [ ] 裁剪图像时，确定工具栏文本和按钮的颜色 [#9](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/9)
- [ ] 调用ViewController“completion”块，Promise将解析/拒绝， HarmonyOS 不支持 [#10](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/10)
- [ ] iOS支持智能相册列表  [#11](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/11)
- [ ] iOS视频压缩的预设 [#12](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/12)
- [ ] iOS智能相册排序  [#13](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/13)
- [ ] Android Demo 设置是否显示底部控件 [#14](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/14)
- [ ] 使用multiple选项时无法设置最小文件数 [#39](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/39)
- [ ] 使用multiple选项时无法设置是否显示选中的资产数量 [#40](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/40)
- [ ] photoAccessHelper选取完成之后没有loading过渡动画效果 [#45](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/45)
- [ ] @ohos.multimedia.image无法进行圆形效果裁切 [#46](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/46)
- [ ] @ohos.multimedia.image中PackingOption无法设置宽高属性 [#47](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/47)

## 9. 其他

## 10. 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ivpusic/react-native-image-crop-picker/blob/master/LICENSE) ，请自由地享受和参与开源。
