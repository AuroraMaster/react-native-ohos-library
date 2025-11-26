> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-country-picker-modal</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-country-picker-modal">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-country-picker-modal/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

本项目基于 [react-native-country-picker-modal](https://github.com/xcarpentier/react-native-country-picker-modal) 开发。

请到三方库的 Releases 发布地址查看配套的版本信息：

| Version | Package name                                           | Repository                                                                              | Release                                                                                                  | Support RN version |
|---------|--------------------------------------------------------|-----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|--------------------|
| 2.0.0   | @react-native-oh-tpl/react-native-country-picker-modal | [Github](https://github.com/react-native-oh-library/react-native-country-picker-modal/) | [Github Releases](https://github.com/react-native-oh-library/react-native-country-picker-modal/releases) | 0.72               |
| 2.1.0   | @react-native-ohos/react-native-country-picker-modal   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-country-picker-modal)  | [GitCode Releases]()                                                                                     | 0.77               |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：



<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-country-picker-modal

# 0.77
npm install @react-native-ohos/react-native-country-picker-modal
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-country-picker-modal

# 0.77
yarn add @react-native-ohos/react-native-country-picker-modal
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import React, {useState} from 'react';
import {
  Text,
  StyleSheet,
  PixelRatio,
  Switch,
  Button,
  ScrollView,
  View,
  ViewProps,
} from 'react-native';
import CountryPicker, {
  CountryModalProvider,
  CountryCode,
  Country,
  DARK_THEME,
} from 'react-native-country-picker-modal';

const styles = StyleSheet.create({
  container: {
    paddingVertical: 10,
    justifyContent: 'center',
    alignItems: 'center',
  },
  welcome: {
    fontSize: 17,
    textAlign: 'center',
    margin: 5,
  },
  instructions: {
    fontSize: 10,
    textAlign: 'center',
    color: '#888',
    marginBottom: 0,
  },
  data: {
    maxWidth: 250,
    padding: 10,
    marginTop: 7,
    backgroundColor: '#ddd',
    borderColor: '#888',
    borderWidth: 1 / PixelRatio.get(),
    color: '#777',
  },
  row: {
    flexDirection: 'row',
    alignItems: 'center',
  },
});

const Row = (
  props: ViewProps & {children?: React.ReactNode; fullWidth?: boolean},
) => (
  <View
    {...props}
    style={[
      styles.row,
      props.style,
      props.fullWidth && {
        width: '100%',
        justifyContent: 'space-between',
        padding: 10,
        paddingHorizontal: 50,
      },
    ]}
  />
);
interface OptionProps {
  title: string;
  value: boolean;
  onValueChange(value: boolean): void;
}
const Option = ({value, onValueChange, title}: OptionProps) => (
  <Row fullWidth>
    <Text style={styles.instructions}>{title}</Text>
    <Switch {...{value, onValueChange}} />
  </Row>
);

export function CountryPickerTest() {
  const [countryCode, setCountryCode] = useState<CountryCode>('AF');
  const [country, setCountry] = useState<Country>();
  const [withCountryNameButton, setWithCountryNameButton] =
    useState<boolean>(false);
  const [withCurrencyButton, setWithCurrencyButton] = useState<boolean>(false);
  const [withFlagButton, setWithFlagButton] = useState<boolean>(true);
  const [withCallingCodeButton, setWithCallingCodeButton] =
    useState<boolean>(false);
  const [withFlag, setWithFlag] = useState<boolean>(true);
  const [withEmoji, setWithEmoji] = useState<boolean>(true);
  const [withFilter, setWithFilter] = useState<boolean>(true);
  const [withAlphaFilter, setWithAlphaFilter] = useState<boolean>(false);
  const [withCallingCode, setWithCallingCode] = useState<boolean>(false);
  const [withCurrency, setWithCurrency] = useState<boolean>(false);
  const [withModal, setWithModal] = useState<boolean>(true);
  const [visible, setVisible] = useState<boolean>(false);
  const [dark, setDark] = useState<boolean>(false);
  const [disableNativeModal, setDisableNativeModal] = useState<boolean>(false);
  const onSelect = (country: Country) => {
    setCountryCode(country.cca2);
    setCountry(country);
  };
  const switchVisible = () => setVisible(!visible);
  return (
    <CountryModalProvider>
      <ScrollView contentContainerStyle={styles.container}>
        <Text style={styles.welcome}>Welcome to Country Picker !</Text>
        <Option
          title="With country name on button"
          value={withCountryNameButton}
          onValueChange={setWithCountryNameButton}
        />
        <Option
          title="With currency on button"
          value={withCurrencyButton}
          onValueChange={setWithCurrencyButton}
        />
        <Option
          title="With calling code on button"
          value={withCallingCodeButton}
          onValueChange={setWithCallingCodeButton}
        />
        <Option
          title="With flag"
          value={withFlag}
          onValueChange={setWithFlag}
        />
        <Option
          title="With emoji"
          value={withEmoji}
          onValueChange={setWithEmoji}
        />
        <Option
          title="With filter"
          value={withFilter}
          onValueChange={setWithFilter}
        />
        <Option
          title="With calling code"
          value={withCallingCode}
          onValueChange={setWithCallingCode}
        />
        <Option
          title="With currency"
          value={withCurrency}
          onValueChange={setWithCurrency}
        />
        <Option
          title="With alpha filter code"
          value={withAlphaFilter}
          onValueChange={setWithAlphaFilter}
        />
        <Option
          title="Without native modal"
          value={disableNativeModal}
          onValueChange={setDisableNativeModal}
        />
        <Option
          title="With modal"
          value={withModal}
          onValueChange={setWithModal}
        />
        <Option title="With dark theme" value={dark} onValueChange={setDark} />
        <Option
          title="With flag button"
          value={withFlagButton}
          onValueChange={setWithFlagButton}
        />
        <CountryPicker
          theme={dark ? DARK_THEME : {}}
          {...{
            countryCode,
            withFilter,
            excludeCountries: ['FR'],
            withFlag,
            withCurrencyButton,
            withCallingCodeButton,
            withCountryNameButton,
            withAlphaFilter,
            withCallingCode,
            withCurrency,
            withEmoji,
            withModal,
            withFlagButton,
            onSelect,
            disableNativeModal,
            preferredCountries: ['US', 'GB'],
            modalProps: {
              visible,
            },
            onClose: () => setVisible(false),
            onOpen: () => setVisible(true),
          }}
        />
        <Text style={styles.instructions}>Press on the flag to open modal</Text>
        <Button
          title={'Open modal from outside using visible props'}
          onPress={switchVisible}
        />
        {country !== null && (
          <Text style={styles.data}>{JSON.stringify(country, null, 0)}</Text>
        )}
      </ScrollView>
    </CountryModalProvider>
  );
}


```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.403; ROM: 3.0.0.25;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;


## 属性
详细请查看 [react-native-country-picker-modal的文档介绍](https://github.com/xcarpentier/react-native-country-picker-modal)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description               | Type                                      | Required | Platform                                | HarmonyOS Support                                        |
|-----------------------|---------------------------| --------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| countryCode           | 国家或地区代码                   | [CountryCode](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L252)       | Yes     | All | Yes |
| region                | 区域代码                      | [Region](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L272)                                           | No       | All                                         | Yes                                            |
| subregion             | 子区域代码                     | [Subregion](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L282) | No     | All                          | Yes                             |
| countryCodes          | 国家代码                      | [CountryCode](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L252) | No     | All | Yes |
| theme                 | 主题                        | [Theme](https://github.com/xcarpentier/react-native-country-picker-modal/blob/7611d34fa35744dbec3fbcdd9b4401494b1ba8c4/src/CountryTheme.ts#L5) | No       | All | Yes |
| translation           | 语言代码                      | [TranslationLanguageCode](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L309) | No     | All | Yes |
| modalProps            | 模态框属性                  | [ModalProps](https://facebook.github.io/react-native/docs/modal#props) | No       | All | Yes |
| filterProps           | 国家过滤器属性          | [CountryFilterProps](https://facebook.github.io/react-native/docs/textinput#props) | No        | All | Yes |
| flatListProps         | 继承FlatList组件的属性        | [FlatListProps<Country>](https://facebook.github.io/react-native/docs/flatlist#props) | No        | All | Yes |
| withAlphaFilter       | 启用字母索引过滤器              | boolean                                       | No        | All | Yes |
| withCallingCode       | 显示电话区号         | boolean                                       | No        | All | Yes |
| withCurrency          | 显示货币信息                    | boolean                                                      | No        | All | Yes |
| withEmoji             | 显示国旗                      | boolean                                | No        | All | Yes |
| withCountryNameButton | 使用带国家名称的按钮                | boolean                                                      | No        | All | Yes |
| withCurrencyButton    | 使用带货币信息的按钮                | boolean                                   | No        | All | Yes |
| withCallingCodeButton | 使用带电话区号的按钮                | boolean                                   | No        | All | Yes |
| withFlagButton        | 使用带国旗的按钮                  | boolean                                   | No        | All | Yes |
| withCloseButton       | 显示关闭按钮                    | boolean                               | No        | All | Yes |
| withFilter            | 启用筛选功能                    | boolean                                   | No        | All | Yes |
| withFlag              | 显示国旗                      | boolean                                | No        | All | Yes |
| withModal             | 使用模态框模式                   | boolean                                | No        | All | Yes |
| visible               | 组件显示/隐藏                   | boolean                                                      | No        | All | Yes |
| containerButtonStyle  | 按钮容器样式                    | StyleProp<ViewStyle>                     | No        | All | Yes |
| renderFlagButton      | 自定义渲染国旗按钮                 | (props: (FlagButton['props'])): ReactNode ([FlagButton props](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/FlagButton.tsx#L73)) | No        | All | Yes |
| renderCountryFilter   | 自定义渲染国家过滤器                | (props: CountryFilter['props']): ReactNode ([CountryFilter props is TextInputProps](https://facebook.github.io/react-native/docs/textinput#props)) | No        | All | Yes |
| onSelect              | 选择国家后的回调函数                | (country: Country): void ([Country](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L263)) | Yes     | All | Yes |
| onOpen                | 组件打开时的回调函数                | (): void | Yes  | All | Yes |
| onClose               | 组件关闭时的回调函数                | (): void                                 | Yes     | All | Yes |
| closeButtonImage      | 关闭按钮的图片源                  | [ImageSourcePropType](https://facebook.github.io/react-native/docs/image#props) | No        | All | Yes |
| closeButtonStyle      | 关闭按钮容器样式                  | StyleProp<ViewStyle>                    | No        | All | Yes |
| closeButtonImageStyle | 关闭按钮图片样式                  | StyleProp<ViewStyle>          | No        | All | Yes |
| disableNativeModal    | 需使用CountryModalProvider包裹整个应用 | boolean | No        | All | Yes |
| preferredCountries    | 首选国家列表                    | [CountryCode](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L254) preferred countries they appear first (`withAlphaFilter` must be false) | No        | All | Yes |


## 遗留问题

- [ ] 搜索条件没有按照translation属性进行过滤 [issue#534](https://github.com/xcarpentier/react-native-country-picker-modal/issues/534) 

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/LICENSE.md) ，请自由地享受和参与开源。
