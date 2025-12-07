> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-contacts</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/morenoh149/react-native-contacts">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/morenoh149/react-native-contacts/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-contacts)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 7.0.7-0.0.3@deprecated     | [@react-native-oh-tpl/react-native-contacts Releases(deprecated)](https://github.com/react-native-oh-library/react-native-contacts/releases) | 0.72       |
| 7.0.8      | [@react-native-ohos/react-native-contacts Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-contacts/releases) | 0.72       |
| 8.0.7      | [@react-native-ohos/react-native-contacts Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-contacts/releases) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-contacts
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-contacts
```

<!-- tabs:end -->

快速使用：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { ScrollView, Button, Alert } from "react-native";
import Contacts from "react-native-contacts";

export const ContactsDemo = () => {
  let emailAddress: Contacts.EmailAddress = {
    label: "emailAddress",
    email: "test@163.com",
  };
  let phoneNumber: Contacts.PhoneNumber = {
    label: "phoneNumber",
    number: "13142536789",
  };

  let postalAddress: Contacts.PostalAddress = {
    label: "label",
    formattedAddress: "formattedAddress",
    street: "street",
    pobox: "pobox",
    neighborhood: "neighborhood",
    city: "city",
    region: "region",
    state: "state",
    postCode: "postCode",
    country: "country",
  };

  let birthday: Contacts.Birthday = {
    day: 1,
    month: 5,
    year: 2024,
  };

  let instantMessageAddress: Contacts.InstantMessageAddress = {
    username: "username",
    service: "service",
  };

  let urlAddress: Contacts.UrlAddress = {
    url: "url",
    label: "label",
  };
  let contact: Contacts.Contact = {
    company: "addcompany",
    emailAddresses: [emailAddress],
    displayName: "adddisplayName",
    familyName: "addfamilyName",
    givenName: "addgivenName",
    middleName: "addmiddleName",
    jobTitle: "addjobTitle",
    phoneNumbers: [phoneNumber],
    hasThumbnail: false,
    thumbnailPath: "addthumbnailPath",
    isStarred: false,
    postalAddresses: [postalAddress],
    prefix: "addprefix",
    suffix: "addsuffix",
    department: "adddepartment",
    birthday: birthday,
    imAddresses: [instantMessageAddress],
    urlAddresses: [urlAddress],
    note: "addnote",
  };

  return (
    <ScrollView>
      <Button
        title="requestPermission"
        onPress={() => {
          Contacts.requestPermission().then((data) => {
            console.log(`requestPermission:${JSON.stringify(data)}`);
            Alert.alert(`requestPermission:${JSON.stringify(data)}`);
          });
        }}
      />
      <Button
        title="checkPermission"
        onPress={() => {
          Contacts.checkPermission().then((data) => {
            console.log(`checkPermission:${JSON.stringify(data)}`);
            Alert.alert(`checkPermission:${JSON.stringify(data)}`);
          });
        }}
      />
      <Button
        title="getAll"
        onPress={() => {
          Contacts.getAll().then((contacts: Contacts.Contact[]) => {
            console.log(`getAll:${JSON.stringify(contacts)}`);
          });
        }}
      />
      <Button
        title="getAllWithoutPhotos"
        onPress={() => {
          Contacts.getAllWithoutPhotos().then(
            (contacts: Contacts.Contact[]) => {
              console.log(`getAllWithoutPhotos:${JSON.stringify(contacts)}`);
            }
          );
        }}
      />
      <Button
        title="getContactById"
        onPress={() => {
          Contacts.getContactById("1").then(
            (contact: Contacts.Contact | null) => {
              console.log(`getContactById:${JSON.stringify(contact)}`);
            }
          );
        }}
      />
      <Button
        title="getCount"
        onPress={() => {
          Contacts.getCount().then((count: number) => {
            console.log(`getCount:${count}`);
          });
        }}
      />
      <Button
        title="getPhotoForId"
        onPress={() => {
          Contacts.getPhotoForId("1").then((photoUrl: string) => {
            console.log(`getPhotoForId:${photoUrl}`);
          });
        }}
      />
      <Button
        title="addContact"
        onPress={() => {
          Contacts.addContact(contact).then((contact: Contacts.Contact) => {
            console.log(`addContact:${JSON.stringify(contact)}`);
          });
        }}
      />

      <Button
        title="openContactForm"
        onPress={() => {
          Contacts.openContactForm(contact).then(
            (contact: Contacts.Contact) => {
              console.log(`openContactForm:${JSON.stringify(contact)}`);
              Alert.alert(`openContactForm success`);
            }
          );
        }}
      />
      <Button
        title="openExistingContact"
        onPress={() => {
          Contacts.openExistingContact({
            recordID: "1",
            phoneNumbers: [
              {
                label: "phoneNumber2",
                number: "13521456721",
              },
            ],
          }).then((contact: Contacts.Contact) => {
            console.log(`openExistingContact:${JSON.stringify(contact)}`);
            Alert.alert(`openExistingContact success`);
          });
        }}
      />
      <Button
        title="viewExistingContact"
        onPress={() => {
          Contacts.viewExistingContact({
            recordID: "1",
            phoneNumbers: [
              {
                label: "phoneNumber2",
                number: "13521456721",
              },
            ],
          }).then((contact: Contacts.Contact) => {
            console.log(`viewExistingContact:${JSON.stringify(contact)}`);
            Alert.alert(`viewExistingContact success`);
          });
        }}
      />
      <Button
        title="editExistingContact"
        onPress={() => {
          Contacts.editExistingContact({
            recordID: "1",
            phoneNumbers: [
              {
                label: "phoneNumber2",
                number: "13521456721",
              },
            ],
          }).then((contact: Contacts.Contact) => {
            console.log(`editExistingContact:${JSON.stringify(contact)}`);
            Alert.alert(`editExistingContact success`);
          });
        }}
      />
      <Button
        title="updateContact"
        onPress={() => {
          Contacts.updateContact({
            recordID: "1",
            familyName: "updateContact",
            givenName: "updateContact",
            phoneNumbers: [
              {
                label: "phoneNumber2",
                number: "13521456721",
              },
              {
                label: "phoneNumber3",
                number: "13521456222",
              },
            ],
          }).then(() => {
            Alert.alert(`updateContact success`);
          });
        }}
      />
      <Button
        title="deleteContact"
        onPress={() => {
          Contacts.deleteContact({
            recordID: "3",
          }).then(() => {
            Alert.alert(`deleteContact success`);
          });
        }}
      />
      <Button
        title="getContactsMatchingString"
        onPress={() => {
          Contacts.getContactsMatchingString("addfamilyName").then(
            (contacts: Contacts.Contact[]) => {
              console.log(
                `getContactsMatchingString:${JSON.stringify(contacts)}`
              );
            }
          );
        }}
      />
      <Button
        title="getContactsByPhoneNumber"
        onPress={() => {
          Contacts.getContactsByPhoneNumber("789").then(
            (contacts: Contacts.Contact[]) => {
              console.log(
                `getContactsByPhoneNumber:${JSON.stringify(contacts)}`
              );
            }
          );
        }}
      />
      <Button
        title="getContactsByEmailAddress"
        onPress={() => {
          Contacts.getContactsByEmailAddress("test@163.com").then(
            (contacts: Contacts.Contact[]) => {
              console.log(
                `getContactsByEmailAddress:${JSON.stringify(contacts)}`
              );
            }
          );
        }}
      />
      <Button
        title="writePhotoToPath"
        onPress={() => {
          Contacts.writePhotoToPath("1", "file").then((data) => {
            console.log(`writePhotoToPath:${JSON.stringify(data)}`);
          });
        }}
      />
      <Button
        title="iosEnableNotesUsage"
        onPress={() => {
          Contacts.iosEnableNotesUsage(true);
          console.log(`iosEnableNotesUsage:true`);
        }}
      />
    </ScrollView>
  );
};
```

## 使用 Codegen

Version >= @react-native-ohos/react-native-contacts@7.0.8，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-contacts@7.0.8，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony" : "file:../react_native_openharmony",
    "@react-native-ohos/react-native-contacts": "file:../../node_modules/@react-native-ohos/react-native-contacts/harmony/contacts.har"
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

### 3.在 ArkTs 侧引入 ContactsPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {ContactsPackage} from '@react-native-ohos/react-native-contacts/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [new SamplePackage(ctx),
+   new ContactsPackage(ctx)];
}
```
### 配置 CMakeLists 和引入 ContactsPackage

> 若使用的是 <= 7.0.7-0.0.3 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-contacts/src/main/cpp" ./
contacts)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_contacts)
# RNOH_END: manual_package_linking_2
```
打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ContactsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ContactsPackage>(ctx)
    };
}
```

### 4.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

### 权限要求

[!TIP] "ohos.permission.READ_CONTACTS"，"ohos.permission.WRITE_CONTACTS"权限等级为<B>system_basic</B>，授权方式为<B>user_grant</B>，[使用 ACL 签名的配置指导](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/signing-0000001587684945-V3#section157591551175916)

打开`entry/src/main/module.json5`，添加：

```json
"requestPermissions": [
     ...
     {
        "name": "ohos.permission.READ_CONTACTS",
        "reason": "$string:read_contacts_reason",
        "usedScene": {
          "abilities": [
            "EntryAbility"
          ],
          "when": "always"
        }
      },
      {
        "name": "ohos.permission.WRITE_CONTACTS",
        "reason": "$string:write_contacts_reason",
        "usedScene": {
          "abilities": [
            "EntryAbility"
          ],
          "when": "always"
        }
      }
]
```

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                                         | Description                                                  | Type     | Required | Platform     | HarmonyOS Support |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | ------------ | ----------------- |
| getAll: Promise<Contact[]>                                   | returns all contacts as an array of objects                  | function | no       | Android,iOS | yes               |
| getAllWithoutPhotos:Promise<Contact[]>                       | same as `getAll` on Android, but on iOS it will not return uris for contact photos (because there's a significant overhead in creating the images) | function | no       | Android,iOS  | yes               |
| getContactById(contactId): Promise<Contact>                  | returns contact with defined contactId (or null if it doesn't exist) | function | no       | Android,iOS  | yes               |
| getCount(): Promise<number>                                  | returns the number of contacts                               | function | no       | Android,iOS  | yes               |
| getPhotoForId(contactId: string): Promise<string>            | Promise - returns a URI (or null) for a contacts photoURL    | function | no       | Android,iOS  | yes               |
| addContact(contact: Partial<Contact>): Promise<Contact>      | adds a contact to the AddressBook                            | function | no       | Android,iOS  | yes               |
| openContactForm(contact: Partial<Contact>): Promise<Contact \| null> | create a new contact and display in contactsUI               | function | no       | Android,iOS  | partially         |
| openExistingContact(contact: Contact): Promise<Contact>      | open existing contact (edit mode), where contact is an object with a valid recordID | function | no       | Android,iOS  | partially         |
| viewExistingContact(contact: { recordID: string })           | open existing contact (view mode), where contact is an object with a valid recordID | function | no       | Android,iOS  | partially         |
| editExistingContact(contact: Contact): Promise<Contact>      | add numbers to the contact, where the contact is an object with a valid recordID and an array of phoneNumbers | function | no       | Android,iOS  | no                |
| updateContact(contact: Partial<Contact> & {recordID: string}): Promise<void> | where contact is an object with a valid recordID             | function | no       | Android,iOS  | yes               |
| deleteContact(contact: Contact): Promise<void>               | where contact is an object with a valid recordID             | function | no       | Android,iOS  | yes               |
| getContactsMatchingString(str: string): Promise<Contact[]>   | where string is any string to match a name (first, middle, family) to | function | no       | Android,iOS  | yes               |
| getContactsByPhoneNumber(phoneNumber: string): Promise<Contact[]> | where string is a phone number to match to.                  | function | no       | Android,iOS  | yes               |
| getContactsByEmailAddress(emailAddress: string): Promise<Contact[]> | where string is an email address to match to.                | function | no       | Android,iOS  | yes               |
| checkPermission(): Promise<'authorized' \| 'denied' \| 'undefined'>; | checks permission to access Contacts ios only                | function | no       | iOS       | yes               |
| requestPermission(): Promise<'authorized' \| 'denied' \| 'undefined'> | request permission to access Contacts ios only               | function | no       | iOS       | yes               |
| writePhotoToPath(contactId: string, file: string): Promise<boolean> | writes the contact photo to a given path android only        | function | no       | Android | no                |


**Contacts**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| recordID | 联系人id | string | no | Android,iOS | yes |
| backTitle | 返回键标题 | string | no | Android,iOS | no |
| company | 公司 | string|no | Android,iOS | yes |
| emailAddresses | 电子邮箱地址 | EmailAddress[] | no | Android,iOS | yes |
| displayName | 展示名 | string | no | Android,iOS | yes |
| familyName | 姓氏 | string | no | Android,iOS | yes |
| givenName | 名字 | string | no | Android,iOS | yes |
| middleName | 中间名 | string | no | Android,iOS | yes |
| jobTitle | 职位名称 | string | no | Android,iOS | yes |
| phoneNumbers | 电话号码 | PhoneNumber[] | no | Android,iOS | yes |
| hasThumbnail | 有头像 | boolean | no | Android,iOS | no |
| thumbnailPath | 头像地址 | string | no | Android,iOS | no |
| isStarred | 是否标记 | boolean | no | Android,iOS | yes |
| postalAddresses | 邮件地址 | PostalAddress[] | no | Android,iOS | yes |
| prefix | 前缀 | string | no | Android,iOS | yes |
| suffix | 后缀 | string | no | Android,iOS | yes |
| department | 部门 | string | no | Android,iOS | yes |
| birthday | 生日 | Birthday | no | Android,iOS | yes |
| imAddresses | 即时消息地址 | InstantMessageAddress[] | no | Android,iOS | yes |
| urlAddresses | 图片地址 | UrlAddress[] | no | Android,iOS | no |
| note | 备注 | string | no | Android,iOS | yes |


**EmailAddress**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| label | 标题 | string | no | Android,iOS | yes |
| email | 地址 | string | no | Android,iOS | yes |

**PhoneNumber**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| label | 标题 | string | no | Android,iOS | yes |
| number | 号码 | string | no | Android,iOS | yes |

**PostalAddress**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| label | 标题 | string | no | Android,iOS | yes |
| formattedAddress | 格式化地址 | string | no | Android,iOS | yes |
| street | 街道 | string | no | Android,iOS | yes |
| pobox | 信箱 | string | no | Android,iOS | yes |
| neighborhood | 邻域 | string | no | Android,iOS | yes |
| city | 城市 | string | no | Android,iOS | yes |
| region | 区域 | string | no | Android,iOS | yes |
| state | 州 | string | no | Android,iOS | yes |
| postCode | 邮政编码 | string | no | Android,iOS | yes |
| country | 国家/地区 | string | no | Android,iOS | yes |

**InstantMessageAddress**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| username | 用户名 | string | no | Android,iOS | no |
| service | 服务地址 | string | no | Android,iOS | no |

**Birthday**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| day | 日 | number | no | Android,iOS | yes |
| month | 月 | number | no | Android,iOS | yes |
| year | 年 | number | no | Android,iOS | yes |

**UrlAddress**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| url | 路径 | string | no | Android,iOS | yes |
| label | 标题 | string | no | Android,iOS | yes |


## 遗留问题

- [ ] openContactForm：跳转到系统联系人界面只支持姓名和电话参数传递，需要系统联系人应用支持所有属性，另外创建成功之后无法返回联系人信息，联系人应用目前不支持。[issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)
- [ ] openExistingContact：联系人应用新增和编辑是同一个界面，目前参数只支持姓名和电话传递，编辑成功之后也无法拿到联系人信息[issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)
- [ ] viewExistingContact：查看界面只有姓名和电话信息，需要联系人应用补齐所有属性[issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)
- [ ] editExistingContact：没有单独的只支持编辑电话号码的页面，目前同编辑页面[issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)
- [ ] writePhotoToPath：系统联系人应用不支持[issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/morenoh149/react-native-contacts/blob/master/LICENSE) ，请自由地享受和参与开源。

