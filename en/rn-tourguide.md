> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>rn-tourguide</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/xcarpentier/rn-tourguide">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/xcarpentier/rn-tourguide/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
         <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


This project is based on [rn-tourguide](https://github.com/react-native-oh-library/rn-tourguide).

This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is:`@react-native-ohos/rn-tourguide`, The version correspondence details are as follows:

| Version                   | Package Name                                      | Repository         | Release                    |Support RN version|
| ------------------------- | ------------------------------------------------- | ------------------ | -------------------------- |-------------------|
| 3.3.0  | @react-native-oh-tpl/rn-tourguide | [Github](https://github.com/react-native-oh-library/rn-tourguide) | [Github Releases](https://github.com/react-native-oh-library/rn-tourguide/releases) |0.72       |
| 3.4.0     | @react-native-ohos/rn-tourguide   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_rn-tourguide) | [GitCode Releases]() |0.77       |

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash

# 0.72
npm install @react-native-oh-tpl/rn-tourguide

# 0.77
npm install @react-native-ohos/rn-tourguide
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/rn-tourguide

# 0.77
yarn add @react-native-ohos/rn-tourguide
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```jsx
import * as React from 'react'
import {
  Image,
  Platform,
  StyleSheet,
  Text,
  TouchableOpacity,
  View,
} from 'react-native'
import {
  TourGuideProvider,
  TourGuideZone,
  TourGuideZoneByPosition,
  useTourGuideController
} from 'rn-tourguide'

const uri =
  'https://pbs.twimg.com/profile_images/1223192265969016833/U8AX9Lfn_400x400.jpg'

export default function () {
  return (
    <TourGuideProvider {...{ borderRadius: 16, androidStatusBarVisible: true }}>
      <AppContent />
    </TourGuideProvider>
  )
}

const AppContent = () => {
  const iconProps = { size: 40, color: '#888' }

  const { start, canStart, stop, eventEmitter } = useTourGuideController()

  React.useEffect(() => {
    if (canStart) {
      start()
    }
  }, [canStart]) 

  React.useEffect(() => {
    eventEmitter?.on('start', () => console.log('start'))
    eventEmitter?.on('stop', () => console.log('stop'))
    eventEmitter?.on('stepChange', () => console.log(`stepChange`))
    return () => eventEmitter?.off('*', () => {})
  }, [])
  return (
    <View style={styles.container}>
      <TourGuideZone
        keepTooltipPosition
        zone={1}
        text={'A react-native-copilot remastered! 🎉'}
        borderRadius={16}
      >
        <Text style={styles.title}>
          {'Welcome to the demo of\n"rn-tourguide"'}
        </Text>
      </TourGuideZone>
      <View style={styles.middleView}>
        <TouchableOpacity style={styles.button} onPress={() => start()}>
          <Text style={styles.buttonText}>START THE TUTORIAL!</Text>
        </TouchableOpacity>

        <TourGuideZone zone={2} shape={'rectangle_and_keep'}>
          <TouchableOpacity style={styles.button} onPress={() => start(4)}>
            <Text style={styles.buttonText}>Step 4</Text>
          </TouchableOpacity>
        </TourGuideZone>
        <TouchableOpacity style={styles.button} onPress={() => start(2)}>
          <Text style={styles.buttonText}>Step 2</Text>
        </TouchableOpacity>
        <TouchableOpacity style={styles.button} onPress={stop}>
          <Text style={styles.buttonText}>Stop</Text>
        </TouchableOpacity>
        <TourGuideZone
          zone={6}
          shape='circle'
          text={'With animated SVG morphing with awesome flubber 🍮💯'}
        >
          <Image source={{uri}} style={styles.profilePhoto} />
        </TourGuideZone>
      </View>
      <View style={styles.row}>
        <TourGuideZone zone={3} shape={'circle'} tooltipBottomOffset={200}>
          <Text style={styles.text}>Text1</Text>
        </TourGuideZone>
        <Text style={styles.text}>Text2</Text>
        <Text style={styles.text}>Text3</Text>
     
        <TourGuideZone zone={4} shape={'rectangle'}>
          <Text style={styles.text}>Text4</Text>
        </TourGuideZone>
        <TourGuideZone zone={5} shape={'circle'}>
          <Text style={styles.text}>Text5</Text>
        </TourGuideZone>
      </View>
      {Platform.OS !== 'web' ? (
        <TourGuideZoneByPosition
          zone={1}
          shape={'circle'}
          isTourGuide
          top={250}
          left={50}
          width={64}
          height={64}
        />
      ) : null}
    </View>
  )
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    paddingTop: 40,
  },
  title: {
    fontSize: 24,
    textAlign: 'center',
  },
  profilePhoto: {
    width: 140,
    height: 140,
    borderRadius: 70,
    marginVertical: 20,
  },
  middleView: {
    flex: 1,
    alignItems: 'center',
  },
  button: {
    backgroundColor: '#2980b9',
    paddingVertical: 10,
    paddingHorizontal: 15,
    margin: 2,
  },
  buttonText: {
    color: 'white',
    fontSize: 16,
  },
  row: {
    width: '100%',
    padding: 15,
    flexDirection: 'row',
    justifyContent: 'space-between',
  },
  text: {
    fontSize: 20,
  }
})

```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-svg. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-svg](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-svg-capi.md#link) to add it to your project.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

1. RNOH: 0.72.27; SDK: HarmonyOS 5.1.1 Release SDK; IDE: DevEco Studio 5.1.1 Release; ROM: 5.0.1.120;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
## Properties

详情见[rn-tourguide](https://github.com/xcarpentier/rn-tourguide)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### TourGuideProvider
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| tooltipComponent  |  tooltip component       | React.ComponentType<TooltipProps>  | NO | ALL      | YES |
| tooltipStyle  |   tooltip style      | StyleProp<ViewStyle>  | NO | ALL      | YES |
| labels  |   Button text display in tooltip(skip、previous、next、finish)      | Labels | NO | ALL      | YES |
| startAtMount  |         | boolean/string | NO | ALL      | YES |
| androidStatusBarVisible  | android status bar visible        | boolean | NO | Android      | NO |
| backdropColor  |   background color | string | NO | ALL      | YES |
| verticalOffset |  vertical offset | number | NO | ALL      | YES |
| wrapperStyle  |   wrap style    | StyleProp<ViewStyle> | NO | ALL      | YES |
| maskOffset  |  offset around zone | number | NO | ALL      | YES |
| borderRadius  |    round corner when rectangle | number | NO | ALL      | YES |
| animationDuration  |  Animation duration | number | NO | ALL      | YES |
| children  |  React.ReactNode components      | React.ReactNode | YES | ALL      | YES |
| dismissOnPress  |  whether to display touchable | boolean | NO | ALL      | YES |
| preventOutsideInteraction  |    Block default events | boolean | NO | ALL      | YES |

### TourGuideZone
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| zone  | A positive number indicating the order of the step in the entire walkthrough.        | number  | YES | ALL      | YES |
| tourKey  |        | string  | NO | ALL      | YES |
| isTourGuide  |  return children without wrapping id false        | boolean  | NO | ALL      | YES |
| text  |     text in tooltip     | string  | NO | ALL      | YES |
| shape  |     which shape     | Shape  | NO | ALL      | YES |
| maskOffset  |   offset around zone    | number  | NO | ALL      | YES |
| borderRadius  |   round corner when rectangle      | number  | NO | ALL      | YES |
| children  |   React.ReactNode components       | React.ReactNode  | NO | ALL      | YES |
| style  |         | StyleProp<ViewStyle>  | NO | ALL      | YES |
| keepTooltipPosition  |  tooltip positioning    | boolean  | NO | ALL      | YES |
| tooltipBottomOffset  |   The distance between the tooltip and the bottom of the container      | number  | NO | ALL      | YES |
| borderRadiusObject  |   Mask layer highlight area rounded corner settings      | BorderRadiusObject  | NO | ALL      | YES |

### Tooltip
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| isFirstStep  | Is it the first step | boolean  | NO | ALL      | YES |
| isLastStep  |  Is it the last step   | boolean  | NO | ALL      | YES |
| currentStep  |  current step | IStep  | YES | ALL      | YES |
| labels  |     Button text display in tooltip(skip、previous、next、finish)     | Labels  | NO | ALL      | YES |
| handleNext  |  A function that handle next step  | Function  | NO | ALL      | YES
| handlePrev  |  A function that handle prev step     | Function  | NO | ALL      | YES
| handleStop  |  A function that handle stop       | Function  | NO | ALL      | YES

### TourGuideZoneByPosition
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| zone  |         | number  | YES | ALL      | YES |
| tourKey  |         | string  | NO | ALL      | YES |
| isTourGuide  |  return children without wrapping id false        | boolean  | NO | ALL      | YES |
| top  |   tour guide zone distance from top    | number/string  | NO | ALL      | YES |
| left  | tour guide zone distance from left        | number/string  | NO | ALL      | YES |
| right  |   tour guide zone distance from right      | number/string  | NO | ALL      | YES |
| bottom  |  tour guide zone distance from bottom       | number/string  | NO | ALL      | YES |
| width  |   The width of the highlight area of ​​the mask layer  | number/string  | NO | ALL      | YES |
| height  |     The height of the highlight area of ​​the mask layer    | number/string  | NO | ALL      | YES |
| shape  |   which shape      | Shape  | NO | ALL      | YES |
| borderRadiusObject  |   Mask layer highlight area rounded corner settings      | BorderRadiusObject  | NO | ALL      | YES |
| containerStyle  |   Mask layer wrapping layer style      | StyleProp<ViewStyle>  | NO | ALL      | YES |
| keepTooltipPosition  |   tooltip positioning       | boolean  | NO | ALL      | YES |
| tooltipBottomOffset  |   The distance between the tooltip and the bottom of the container      | number  | NO | ALL      | YES |
| text  |    text in tooltip     | string  | NO | ALL      | YES |

### useTourGuideController
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| start  | start tour guide         | Funtion  | YES | ALL      | YES |
| eventEmitter  | event emitter           | Funtion/undefined  | YES | ALL      | YES |
| getCurrentStep  | Get the mask layer pop-up component         | Funtion/undefined  | YES | ALL      | YES |
| canStart  | whether to support  tour guide         | boolean/undefined  | YES | ALL      | YES |
| tourKey  | tour guide key         | string  | YES | ALL      | YES |
| TourGuideZone  | boot area         | Funtion  | YES | ALL      | YES |
| TourGuideZoneByPosition  | tourGuide area location | Funtion  | YES | ALL      | YES |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/xcarpentier/rn-tourguide/blob/master/LICENSE).
