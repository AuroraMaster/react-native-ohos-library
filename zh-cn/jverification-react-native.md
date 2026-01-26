> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"><code>jverification-react-native</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jpush/jverification-react-native">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/jverification-react-native/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/jpush/jverification-react-native)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.4.7     | [@react-native-ohos/jverification-react-native Releases](https://github.com/react-native-oh-library/jverification-react-native/releases) | 0.72/0.77       |



进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/jverification-react-native
```

#### **yarn**

```bash
yarn add @react-native-ohos/jverification-react-native
```

另外还需按照[极光安全认证SDK-HarmonyOS集成指南](https://docs.jiguang.cn/jverification/client/harmonyos_guide)完成极光安全认证相关的配置

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import {
  View,
  StyleSheet,
  Button,
  Alert,
  ScrollView,
} from "react-native";
import JVerification from "jverification-react-native";

const customConfigParams = {
  showWindow: false,
  dialogWidth: 275, 
  dialogHeight: 400,
  /**
   * 手机号样式
   */
  numberSize: 30,
  numberColor: "#B22222",
  numberX: 0,
  numberY: 30,
  numberW: "100%",
  numberH: 100,
  /**
   * login
   */
  loginBtnText: "一键登录",
  loginBtnTextSize: 20,
  loginBtnTextColor: "rgb(0,0,0)",
  loginBtnImage: "loginBtn",
  loginBtnX: -1,
  loginBtnY: 20,
  loginBtnW: "60%",
  loginBtnH: 56,
  backgroundImage: "background",
  /**
   * 隐私协议页面
   */
  privacyWebNavTitleColor: "rgb(29,211,29)",
  privacyWebNavColor: "rgb(202,193,16)",
  privacyWebNavTitleSize: 20,
  privacyWebNavReturnImage: "back",
  /**
   * logo
   */
  logoHidden: false,
  logoImage: "logo",
  logoX: -1,
  logoY: 175,
  logoW: 100,
  logoH: 100,
  /**
   * slogan
   */
  sloganTextSize: 20,
  sloganTextColor: "rgb(216,213,30)",
  sloganX: -1,
  sloganY: 70,
  /**
   * 隐私协议部分
   */
  privacyOne: ["隐私条款1", "https://developer.huawei.com/consumer/cn/"],
  privacyTwo: ["隐私条款2", "https://developer.huawei.com/consumer/cn/support/"],
  privacyColor: ["#bed442ff", "#d61e9fff"],
  privacyText: ["登录即同意", "，并使用本机号码登录"],
  privacyTextSize: 15,
  privacyTextGravityMode: "center",
  privacyCheckEnable: false,
  privacyCheckedImage: "check",
  privacyUncheckedImage: "unCheck",
  privacyCheckboxSize: 20,
  privacyX: 5,
  privacyY: 5,
  privacyBookSymbolEnable: true,
};

const customConfigParamsCM = {
  showWindow: false,
  /**
   * 隐私协议部分
   */
  privacyOne: ["自定义协议1", "https://developer.huawei.com/consumer/cn/"],
  privacyTwo: ["自定义协议2", "https://developer.huawei.com/consumer/cn/support/"],
  privacyColor: ["rgb(30,73,216)", "rgb(39,39,9)"],
  privacyText: ["登录即同意", "，并使用本机号码登录。"],
  privacyTextSize: 16,
  privacyBookSymbolEnable: false,
  privacyX: 40,
  privacyY: 0,
  privacyTextGravityMode: "center",
  privacyCheckEnable: false,
  privacyCheckboxSize: 20,
  privacyCheckedImage: "check",
  privacyUncheckedImage: "unCheck",
  /**
   * 隐私协议页面
   */
  privacyWebNavTitleColor: "rgb(29,211,29)",
  privacyWebNavColor: "rgb(202,193,16)",
  privacyWebNavTitleSize: 20,
  /**
   * 导航栏、状态栏
   */
  statusBarMode: "light",
  navColor: "rgb(63,196,36)",
  navTitleColor: "rgb(211,208,29)",
  /**
   * login
   */
  loginBtnText: "一键登录",
  loginBtnTextSize: 20,
  loginBtnTextColor: "rgb(0,0,0)",
  loginBtnImage: "loginBtn",
  loginBtnDisabledImage: "background",
  loginBtnX: -1,
  loginBtnY: 335,
  loginBtnW: "60%",
  loginBtnH: 56,
  /**
   * 手机号样式
   */
  numberSize: 30,
  numberColor: "rgb(158,19,19)",
  numberX: 160,
  numberY: 250,
  numberW: "100%",
  numberH: 100,
};

let customViewParams = {};

class JverificationTest extends React.Component {
  state = { code: "", msg: "", operator: "", enable: true };
  render() {
    const { code, msg, operator, enable } = this.state;

    return (
      <ScrollView>
         <View style={styles.container}>
        <View style={styles.space}>
          <Button
            title="setLoggerEnable (true)"
            onPress={() => {
              JVerification.setLoggerEnable(false);
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="init"
            onPress={() => {
              JVerification.init(
                { appkey: "373cb7214054aae64525fdf4" },
                (result) => {
                  Alert.alert("SDK初始化", JSON.stringify(result));
                }
              );
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="isInitSuccess"
            onPress={() => {
              JVerification.isInitSuccess((result) => {
                Alert.alert("初始化是否成功", JSON.stringify(result));
              });
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="checkLoginEnable"
            onPress={() => {
              // SDK判断网络环境是否支持
              JVerification.checkLoginEnable((result) => {
                Alert.alert("网络环境是否支持", JSON.stringify(result.enable));
              });
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="getToken"
            onPress={() => {
              JVerification.getToken(5000, (result) => {
                Alert.alert("获取号码认证token", JSON.stringify(result));
              });
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="preLogin"
            onPress={() => {
              JVerification.preLogin(5000, (result) => {
                Alert.alert("获取预取号token", JSON.stringify(result));
              });
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="clearPreLoginCache"
            onPress={() => {
              JVerification.clearPreLoginCache();
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="addLoginCustomConfig CT CU"
            onPress={() => {
              JVerification.addLoginCustomConfig(
                customConfigParams,
                customViewParams
              );
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="addLoginCustomConfig CM"
            onPress={() => {
              JVerification.addLoginCustomConfig(
                customConfigParamsCM,
                customViewParams
              );
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="addLoginEventListener"
            onPress={() => {
              JVerification.addLoginEventListener((result) => {
                Alert.alert("addLoginEventListener: ", JSON.stringify(result));
              });
            }}
          />
        </View>
        
        <View style={styles.space}>
          <Button
            title="addUncheckBoxEventListener"
            onPress={() => {
              JVerification.addUncheckBoxEventListener((result) => {
                Alert.alert(
                  "addUncheckBoxEventListener: ",
                  JSON.stringify(result)
                );
              });
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="login"
            onPress={() => {
              JVerification.login(true);
            }}
          />
        </View>

        <View style={styles.space}>
          <Button
            title="dismissLoginPage"
            onPress={() => {
              JVerification.dismissLoginPage();
            }}
          />
        </View>
        
        </View>
      </ScrollView>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    flexDirection: "column",
    alignItems: "center",
    padding: 10,
    marginTop: 38
  },
  label: {
    fontSize: 30,
  },
  viewBox: {
    padding: 5,
    backgroundColor: "white",
    width: "100%",
    marginBottom: 10,
    matginTop: 10,
    justifyContent: "flex-start",
  },
  space: {
    flex: 1,
    marginTop: 10
  }
});

export default JverificationTest;

```

## Link

此步骤为手动配置原生依赖项的指导。

首先需要使用DevEco Studio打开项目里的HarmonyOS工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```
### 2.在工程根目录的 `build-profile.json5` 添加 products 字段

```json
{
  ...
  products: [
      {
        ...
        buildOption: {
          strictMode: {
            useNormalizedOHMUrl: true,
          },
        },
      },
  ]
}
```

### 3.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/jverification-react-native": "file:../../node_modules/@react-native-ohos/jverification-react-native/harmony/jverification_react_native.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```


方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 4.配置 CMakeLists 和引入 JVerificationPackage.h

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/jverification-react-native/src/main/cpp" ./jVerification_react_native)
# RNOH_BEGIN: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_jVerification_react_native)
# RNOH_BEGIN: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "JVerificationPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<JVerificationPackage>(ctx)
    };
}
```

### 5.在 ArkTs 侧引入 JVerificationPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+   import {JVerificationPackage} from '@react-native-ohos/jverification-react-native/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new JVerificationPackage(ctx)
  ];
}
```

### 6.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.90; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.112;
2. RNOH：0.72.90; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 6.0.0.858; ROM：5.0.0.102;
3. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.112;
4. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 6.0.0.858; ROM：5.0.0.102;

### 权限要求

- 由于此库涉及振动功能，使用对应接口时则需要配置对应的权限，权限需配置在**entry/src/main**目录下**module.json5**文件中。其中部分权限需弹窗向用户申请授权。具体权限配置见文档：[程序访问控制](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/Readme-CN.md#/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/app-permission-mgmt-overview.md)。

- 此库部分功能与接口需要**normal**权限：**ohos.permission.INTERNET**。

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| setLoggerEnable(enable: boolean): void  | 设置debug模式        | function | no | iOS/Android      | yes |
| init(params, callback)  | 初始化SDK        | function | no | iOS/Android      | yes |
| isInitSuccess(callback) | 初始化是否成功        | function | no | iOS/Android      | yes |
| checkLoginEnable(callback)  | 判断当前网络环境是否可以发起认证       | function | no | iOS/Android      | yes |
| getToken(time, callback) | 获取手机号校验token       | function | no | iOS/Android      | yes |
| preLogin(time, callback)  | 验证当前运营商网络是否可以进行一键登录操作，该方法会缓存取号信息      | function | no | iOS/Android      | yes |
| clearPreLoginCache()  | 清除预取号缓存      | function | no | iOS/Android      | yes |
| login(enable)  | 调起一键登录授权页面      | function | no | iOS/Android      | yes |
| addLoginEventListener(callback)  | 添加一键登录事件监听   | function | no | iOS/Android      | yes |
| addUncheckBoxEventListener(callback)  | 添加勾选框监听事件      | function | no | iOS/Android      | yes |
| dismissLoginPage()  | 隐藏登录授权页      | function | no | iOS/Android      | yes |
| removeListener(callback)  | 移除监听事件      | function | no | iOS/Android      | no |
| getVerifyCode(params,callback)  | 获取验证码      | function | no | iOS/Android      | no |
| setCodeTime(time)  | 获取两个验证码之间的间隔     | function | no | iOS/Android      | no |
| addCustomViewsClickCallback  | 添加自定义 view 回调      | function | no | iOS/Android      | no |
| addLoginCustomConfig(customConfigParams, customViewParams)  | 自定义配置参数      | function | no | iOS/Android      | yes |

### init参数params
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| appkey  | 极光应用唯一标识      | string | no | iOS/Android      | yes | 

### init参数callback
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| code  | 状态码      | number | no | iOS/Android      | yes |  
| content  | 初始化结果信息      | string | no | iOS/Android      | yes |  

### getToken参数time
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| time  | 设置初始化超时时间，单位毫秒，合法范围是(0,10000]，默认值为 5000      | number | no | iOS/Android      | yes |

### getToken参数callback
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| code  | 状态码      | number | no | iOS/Android      | yes |  
| content  | 获取Token结果信息      | string | no | iOS/Android      | yes |  
| operator  | 运营商信息      | string | no | iOS/Android      | yes |  

### preLogin参数time
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| time  | 设置超时时间，单位毫秒，合法范围是(0,30000]，默认值为 10000     | number | no | iOS/Android      | yes |

### preLogin参数callback
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| code  | 状态码      | number | no | iOS/Android      | yes |  
| content  | 是否可以进行一键登录操作结果信息      | string | no | iOS/Android      | yes |  

### login参数enable
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| enable  |  是否自动关闭授权页      | boolean | no | iOS/Android      | yes |  

### addLoginEventListener参数callback
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| code  |  状态码      | number | no | iOS/Android      | yes |  
| msg  |  一键登录事件监听信息      | string | no | iOS/Android      | yes |  
| operator  |  运营商信息      | string | no | iOS/Android      | yes |

### customConfigParams
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| backgroundImage  | 背景图片(联通、电信)，仅支持本地图片        | string | no | iOS/Android      | yes |
| statusBarHidden  | 状态栏是否隐藏        | boolean | no | iOS/Android      | no |
| statusBarMode  | 状态栏模式（仅移动）       | 'light'&#124;'dark' | no | iOS/Android      | yes |
| navHidden | 导航栏是否隐藏       | boolean | no | iOS/Android      | no |
| navTitle  | 导航栏标题        | string | no | iOS/Android      | no |
|navTitleSize  | 导航栏标题文字字体大小        | number | no | iOS/Android      | no |
| navTitleColor  | 导航栏标题文本颜色（仅移动）        | string | no | iOS/Android      | yes |
| navReturnHidden  | 导航栏返回按钮是否隐藏        | boolean | no | iOS/Android      | no |
| navReturnImage  | 导航栏左侧返回按钮图标        | string | no | iOS/Android      | no |
| navReturnX  | 导航栏左侧返回按钮图标距屏幕上端偏移        | number | no | Android      | no |
| navReturnY  | 导航栏左侧返回按钮图标距屏幕左侧偏移        | number | no | Android      | no |
| navReturnW  | 导航栏左侧返回按钮图标宽度        | number | no | Android      | no |
| navReturnH  | 导航栏左侧返回按钮图标高度        | number | no | Android      | no |
| logoHidden  | 是否隐藏logo (联通、电信)      | boolean | no | iOS/Android      | yes |
| logoImage  | logo图片(联通、电信)，仅支持本地图片        | string | no | iOS/Android      | yes |
| logoX  | logo的x轴偏移 (联通、电信)       | number | no | iOS/Android      | yes |
| logoY  | logo的y轴偏移 (联通、电信)       | number | no | iOS/Android      | yes |
| logoW  | logo宽度 (联通、电信)       | number | no | iOS/Android      | yes |
| logoH  | logo高度 (联通、电信)       | number | no | iOS/Android      | yes |
| numberSize  | 手机号字体大小(联通、电信、移动)        | number | no | iOS/Android      | yes |
| numberColor  | 手机号颜色(联通、电信、移动)        | number | no | iOS/Android      | yes |
| numberX  | 手机号x轴偏移(联通、电信、移动)        | number | no | iOS/Android      | yes |
| numberY  | 手机号y轴偏移(联通、电信、移动)        | number | no | iOS/Android      | yes |
| numberW  | 手机号文本宽度(联通、电信、移动)        | number | no | iOS/Android      | yes |
| numberH  | 手机号文本高度(联通、电信、移动)        | number | no | iOS/Android      | yes |
| sloganHidden  | slogan是否隐藏        | boolean | no | iOS/Android      | no |
| sloganTextSize  | slogan字号(联通、电信)        | number | no | iOS/Android      | yes |
| sloganTextColor  | slogan颜色(联通、电信)        | string | no | iOS/Android      | yes |
| sloganX  | slogan x轴偏转(联通、电信)        | number | no | iOS/Android      | yes |
| sloganY  | slogan y轴偏转(联通、电信)        | number | no | iOS/Android      | yes |
| sloganW  | slogan宽度        | number | no | iOS      | no |
| sloganH  | slogan高度        | number | no | iOS      | no |
| loginBtnText | 授权登录按钮文本内容(联通、电信、移动)        | string | no | iOS/Android       | yes |
| loginBtnTextSize | 授权登录按钮文本字号(联通、电信、移动)        | number | no | iOS/Android      | yes |
| loginBtnTextColor | 授权登录按钮文本颜色(联通、电信、移动)        | string | no | iOS/Android      | yes |
| loginBtnImage | 授权登录按钮背景图片(联通、电信、移动)，联通、电信仅支持本地图片        | string | no | Android      | yes |
| loginBtnNormalImage | 登录按钮正常图片        | string | no | iOS      | no |
| loginBtnDisabledImage | 登录按钮失效图片(仅移动)        | string | no | iOS      | yes |
| loginBtnSelectedImage | 登录按钮按下图片(联通、电信、移动)        | string | no | iOS     | no |
| loginBtnX | 登录按钮相对于屏幕左边x轴偏移(联通、电信、移动)        | number | no | iOS/Android      | yes |
| loginBtnY | 登录按钮相对于标题栏下边缘y偏移(联通、电信、移动)        | number | no | iOS/Android      | yes |
| loginBtnW | 登录按钮宽度(联通、电信、移动)        | number | no | iOS/Android      | yes |
| loginBtnH | 登录按钮高度(联通、电信、移动)        | number | no | iOS/Android      | yes |
| privacyOne | 隐私条款一(联通、电信、移动)        | Array<string> | no | iOS/Android      | yes |
| privacyTwo | 隐私条款二(联通、电信、移动)        | Array<string> | no | iOS/Android      | yes |
| privacyColor | 隐私条款颜色(联通、电信、移动)        | Array<string> | no | iOS/Android      | yes |
| privacyText | 隐私条款名称外的文字(联通、电信、移动)        | Array<string> | no | iOS/Android      | yes |
| privacyTextSize | 隐私条款文字字体大小(联通、电信、移动)        | number | no | iOS/Android      | yes |
| privacyTextGravityMode | 隐私条款文本对齐方式(联通、电信、移动)，目前仅支持left、center        | string | no | iOS/Android      | yes |
| privacyBookSymbolEnable | 隐私条款是否显示书名号(联通、电信、移动)        | boolean | no | iOS/Android      | yes |
| privacyX | 隐私条款相对于屏幕左边x轴偏移(仅移动)        | number or string | no | iOS/Android      | yes |
| privacyY | 隐私条款相对于授权页面底部下边缘y偏移(仅移动)        | number or string | no | iOS/Android      | yes |
| privacyW | 隐私条款宽度        | number or string | no | iOS/Android      | no |
| privacyH | 隐私条款高度        | number or string | no | iOS/Android      | no |
| privacyCheckboxHidden | checkBox是否隐藏，默认不隐藏        | boolean | no | iOS/Android      | no |
| privacyCheckedImage | checkBox选中时图片(联通、电信、移动)，联通、电信仅支持本地图片        | string | no | iOS/Android      | yes |
| privacyUncheckedImage | checkBox未选中时图片(联通、电信、移动)，联通、电信仅支持本地图片        | string | no | iOS/Android      | yes |
| privacyCheckboxSize | 设置隐私条款checkbox尺寸(联通、电信、移动)        | number | no | Android      | yes |
| privacyCheckEnable | 隐私协议是否勾选(联通、电信、移动)        | boolean | no | iOS/Android      | yes |
| privacyWebNavColor | 隐私协议页面导航栏颜色(联通、电信、移动)        | number | no | iOS/Android      | yes |
| privacyWebNavTitleSize | 隐私协议页面导航栏标题字号(联通、电信、移动)        | number | no | iOS/Android      | yes |
| privacyWebNavTitleColor | 隐私协议页面导航栏标题颜色(联通、电信、移动)        | number | no | iOS/Android      | yes |
| privacyWebNavReturnImage | 隐私协议页面导航栏返回按钮图片(联通、电信)，仅支持本地图片        | string | no | iOS/Android      | yes |
| navColor | 导航栏颜色(仅移动)        | number | no | iOS/Android      | yes |
| showWindow | 是否显示弹窗(当前仅支持移动)        | boolean | no | iOS/Android      | yes |
| logoConstraints | LOGO图片布局对象      | array | no | iOS      | no |
| numberConstraints | 号码栏布局对象      | array | no | iOS      | no |
| sloganConstraints | slogan布局对象      | array | no | iOS      | no |
| logBtnConstraints | 按钮布局对象      | array | no | iOS      | no |
| privacyConstraints | 隐私条款布局对象      | array | no | iOS      | no |
| checkViewConstraints | checkBox布局对象      | array | no | iOS      | no |
| loadingConstraints | loading布局对象      | array | no | iOS      | no |
| windowBackgroundImage | 弹框内部背景图片      | string | no | iOS      | no |
| windowBackgroundAlpha | 弹窗外侧透明度      | number | no | iOS      | no |
| windowCornerRadius | 弹窗圆角数值      | number | no | iOS      | no |
| windowConstraints | 弹窗布局对象      | array | no | iOS      | no |
| windowCloseBtnImgs | 弹窗close按钮图片      | array | no | iOS      | no |
| windowCloseBtnConstraints | 弹窗close按钮布局      | array | no | iOS    | no |

#### customViewParams

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- |----------| -------- |-------------------|
| customViewParams | 自定义view参数  | object | yes | iOS/Android  | no |

## 遗留问题
- [ ] removeListener，getVerifyCode，setCodeTime，addCustomViewsClickCallback，statusBarHidden，navHidden，navColor，navTitle，navTitleSize，navTitleColor，navReturnHidden，navReturnImage，navReturnX，navReturnY，navReturnW，navReturnH，sloganHidden，sloganW，sloganH，loginBtnNormalImage，loginBtnSelectedImage，privacyW，privacyH，privacyCheckboxHidden，logoConstraints，numberConstraints，sloganConstraints，logBtnConstraints，privacyConstraints，checkViewConstraints，loadingConstraints，windowBackgroundImage，windowBackgroundAlpha，windowCornerRadius，windowConstraints，windowCloseBtnImgs，windowCloseBtnConstraints，customViewParams，showWindow（联通、电信）这些接口属性在极光安全认证Harmony SDK中不支持[issue#6](https://github.com/react-native-oh-library/jverification-react-native/issues/6)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/jpush/jverification-react-native/blob/master/LICENSE)，请自由地享受和参与开源。
