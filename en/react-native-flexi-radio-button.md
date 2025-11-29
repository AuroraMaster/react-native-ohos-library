> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-flexi-radio-button</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/thegamenicorus/react-native-flexi-radio-button">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/thegamenicorus/react-native-flexi-radio-button/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/thegamenicorus/react-native-flexi-radio-button)

## Installation and Usage

| version  |  Support RN version |
| ---------- | ---------- |
| 0.2.2      | 0.72/0.77      |


#### **npm**

```bash
npm install react-native-flexi-radio-button@0.2.2
```

#### **yarn**
```bash
yarn add react-native-flexi-radio-button@0.2.2
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

### Basic Example
[see full basic example](https://github.com/thegamenicorus/react-native-flexi-radio-button/blob/master/examples/BasicExample/app.js)

|![basic_example_ios](https://cloud.githubusercontent.com/assets/21040043/18545904/67b5476e-7b65-11e6-8fc4-8160b39a4ab0.gif)|![basic_example_android](https://cloud.githubusercontent.com/assets/21040043/18545908/69b22f5a-7b65-11e6-87d7-c82c0d3057dd.gif)|
|---------------|----------|
```jsx

import {RadioGroup, RadioButton} from 'react-native-flexi-radio-button'

onSelect(index, value){
  this.setState({
    text: `Selected index: ${index} , value: ${value}`
  })
}

render(){
  return(
    <View style={styles.container}>
    
      <RadioGroup
        onSelect = {(index, value) => this.onSelect(index, value)}
      >
        <RadioButton value={'item1'} >
          <Text>This is item #1</Text>
        </RadioButton>

        <RadioButton value={'item2'}>
          <Text>This is item #2</Text>
        </RadioButton>

        <RadioButton value={'item3'}>
          <Text>This is item #3</Text>
        </RadioButton>
      </RadioGroup>
      
      <Text style={styles.text}>{this.state.text}</Text>
      
    </View>
  )
}
```
### Custom Example
[see full custom example](https://github.com/thegamenicorus/react-native-flexi-radio-button/blob/master/examples/CustomExample/app.js)

|![custom_ios](https://cloud.githubusercontent.com/assets/21040043/18546467/53bf8230-7b68-11e6-98f6-98899cce82b3.gif)|![cusom_android](https://cloud.githubusercontent.com/assets/21040043/18546744/cb912fce-7b69-11e6-9331-49e2337dcb04.gif)|
|---------------|----------|


modify in render()

```jsx
<RadioGroup
  size={24}
  thickness={2}
  color='#9575b2'
  highlightColor='#ccc8b9'
  selectedIndex={1}
  onSelect = {(index, value) => this.onSelect(index, value)}
>
  <RadioButton 
    style={{alignItems:'center'}}
    value='Yo!! I am a cat.' 
  >
    <Image
      style={{width:100, height: 100}}
      source={{uri:'https://cloud.githubusercontent.com/assets/21040043/18446298/fa576974-794b-11e6-8430-b31b30846084.jpg'}}
    />
  </RadioButton>

  <RadioButton 
    value='index1'
  > 
    <Text>Start from item index #1</Text>
  </RadioButton>

  <RadioButton 
    value='red color'
    color='red'
  >
    <Text>Red Dot</Text>
  <RadioButton 
    value='green color'
    color='green'
  >
    <Text>Green Dot</Text>
  </RadioButton>

  <RadioButton 
    value='blue color'
    color='blue'
  >
    <Text>Blue Dot</Text>
  </RadioButton>
</RadioGroup>
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.23; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio: 5.0.3.27; ROM: 3.0.0.19;
2. RNOH: 0.72.33; SDK: Openharmony 5.0.0.71(API Version 12 Release); IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

##### Radio Group:
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| size | Radio button size  | number  | no       | Android/IOS | yes       |
| thickness  | Radio button border width | number  | no       | Android/IOS | yes             |
| color  | Radio button color   | string  | no       | Android/IOS | yes             |
| activeColor  | Selected radio button color   | string  | no       | Android/IOS | yes             |
| highlightColor  | Selected radio button background | string  | no       | Android/IOS | yes             |
| selectedIndex  | Default selection index for radio group, can be updated to new value or null for explicit selection | number  | no | Android/IOS | yes  |
| style  | Custom styles to apply if provided | object  | no       | Android/IOS | yes             |
| onSelect  | Function to call when radio button is selected    | function(index, value)  | no       | Android/IOS | yes             |

##### Radio Button:

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| value  | The value will be passed as the second argument in the onSelect callback | any  | no       | Android/IOS | yes      |
| style  | Styles to be applied to the RadioButton component   | object  | no       | Android/IOS | yes      |
| color  | Button color  | string  | no       | Android/IOS | yes             |
| disabled  |  If true, all interactions for this component are disabled  | bool  | no       | Android/IOS | yes    |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/thegamenicorus/react-native-flexi-radio-button/blob/master/LICENSE).
