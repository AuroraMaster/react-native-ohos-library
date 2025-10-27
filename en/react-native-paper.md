> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-paper</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/react-native-paper">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/callstack/react-native-paper/blob/main/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/callstack/react-native-paper/tree/v5.12.3)


## Installation and Usage

<!-- tabs:start -->

#### **yarn**

```bash
yarn add react-native-paper@5.12.3
```
#### **npm**
```bash
npm install react-native-paper@5.12.3
```
<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

- From there is a need to install @react-native-oh-tpl/react-native-safe-area-context for handling safe area.
- If you're on a vanilla React Native project, you also need to install and link @react-native-oh-tpl/react-native-vector-icons.

1.Wrap your root component in from . If you have a vanilla React Native project, it's a good idea to add it in the component which is passed to . This will usually be in the file. If you have an Expo project, you can do this inside the exported component in the file.`PaperProvider``react-native-paper``AppRegistry.registerComponent``index.js``App.js`

```js
import { AppRegistry } from 'react-native';
import { PaperProvider } from 'react-native-paper';
import App from './src/test';
import { name as appName } from './app.json';

export default function PaperExample() {
    return (
      <PaperProvider>
        <App />
      </PaperProvider>
    );
}
AppRegistry.registerComponent(appName, () => PaperExample);
```

2.App.json file (the following is the name of the test project)
```js
{
  "name": "app_name",
  "displayName": "tester",
}
```

3.Create a new Navigation.tsx file in the components directory
```js
import React, {useEffect} from 'react';
import {
  FlatList,
  Image,
  Platform,
  StyleSheet,
  Text,
  TouchableOpacity,
  View,
} from 'react-native';

const NavigationContext = React.createContext<
  | {
      currentPageName: string;
      navigateTo: (pageName: string) => void;
      registerPageName: (pageName: string) => void;
      registeredPageNames: string[];
    }
  | undefined
>(undefined);

const PALETTE = {
  REACT_CYAN_LIGHT: 'hsl(193, 95%, 68%)',
  REACT_CYAN_DARK: 'hsl(193, 95%, 30%)',
};

export function NavigationContainer({
  initialPage = 'INDEX',
  children,
}: {
  initialPage?: string;
  children: any;
}) {
  const [currentPageName, setCurrentPageName] = React.useState(initialPage);
  const [registeredPageNames, setRegisteredPageNames] = React.useState<
    string[]
  >([]);

  return (
    <NavigationContext.Provider
      value={{
        currentPageName,
        navigateTo: setCurrentPageName,
        registerPageName: (pageName: string) => {
          setRegisteredPageNames(pageNames => {
            if (pageNames.includes(pageName)) {
              return pageNames;
            }
            return [...pageNames, pageName];
          });
        },
        registeredPageNames,
      }}>
      <View style={{width: '100%', height: '100%', flexDirection: 'column'}}>
        <Page name="INDEX" children={<IndexPage />}>
        </Page>
        {children}
      </View>
    </NavigationContext.Provider>
  );
}

export function useNavigation() {
  return React.useContext(NavigationContext)!;
}

export function Page({name, children}: {name: string; children: any}) {
  const {currentPageName, navigateTo, registerPageName} = useNavigation();

  useEffect(() => {
    if (name !== 'INDEX') {
      registerPageName(name);
    }
  }, [name]);

  return name === currentPageName ? (
    <View style={{width: '100%', height: '100%'}}>
      {name !== 'INDEX' && (
        <View style={{backgroundColor: PALETTE.REACT_CYAN_DARK}}>
          <TouchableOpacity
            onPress={() => {
              navigateTo('INDEX');
            }}>
            <Text
              style={[styles.buttonText, {color: PALETTE.REACT_CYAN_LIGHT}]}>
              {'‹ Back'}
            </Text>
          </TouchableOpacity>
        </View>
      )}
      <View style={{width: '100%', flex: 1}}>{children}</View>
    </View>
  ) : null;
}

export function IndexPage() {
  const {navigateTo, registeredPageNames} = useNavigation();

  return (
    <FlatList
      data={registeredPageNames}
      ListHeaderComponent={
        <View
          style={{
            flexDirection: 'row',
            alignItems: 'center',
            paddingHorizontal: 16,
            paddingVertical: 16,
          }}>
          <Image
            style={{width: 32, height: 32}}
            resizeMode="contain"
            source={require('../assets/images/react-native-logo.png')}
          />
          <Text
            style={{
              color: '#EEE',
              fontSize: 24,
              fontWeight: 'bold',
              padding: 16,
            }}>
            RN Tester
            {'rnohArchitecture' in Platform.constants
              ? (` (${Platform.constants.rnohArchitecture})` as string)
              : ''}
          </Text>
        </View>
      }
      renderItem={({item}) => {
        return (
          <View style={{backgroundColor: PALETTE.REACT_CYAN_DARK}}>
            <TouchableOpacity
              onPress={() => {
                navigateTo(item);
              }}>
              <Text style={styles.buttonText}>{item}</Text>
            </TouchableOpacity>
          </View>
        );
      }}
      ItemSeparatorComponent={() => (
        <View
          style={{height: StyleSheet.hairlineWidth, backgroundColor: '#666'}}
        />
      )}
    />
  );
}

const styles = StyleSheet.create({
  container: {
    width: '100%',
    height: '100%',
    backgroundColor: '#888',
  },
  buttonText: {
    width: '100%',
    fontWeight: 'bold',
    paddingHorizontal: 16,
    paddingVertical: 24,
    color: 'white',
    backgroundColor: 'black',
  },
});

```

4.After packaging PaperProvider, we need to pass the displayed components to Providers. In this section, we use the ActiveIndicator as an example to demonstrate. Create a new file named test.tsx in the src directory and put the following code into it.
```js
import * as React from 'react';
import { View, StatusBar, SafeAreaView } from 'react-native';
import { PortalProvider } from '@gorhom/portal';
import { ActivityIndicator, MD2Colors } from 'react-native-paper';
import { NavigationContainer, Page } from './components';

export default function App() {
  return (
    <View style={{backgroundColor: 'black'}}>
      <StatusBar barStyle="light-content" />
      <SafeAreaView>
        <NavigationContainer>
          <PortalProvider>
           <View id="__harmony::ready" />
            <Page name="EXAMPLE: ActivityIndicatorDemo">
              <ActivityIndicator animating={true} color={MD2Colors.red800} />
            </Page>
          </PortalProvider>
        </NavigationContainer>
      </SafeAreaView>
    </View>      
  );
}
```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-safe-area-context and @react-native-oh-tpl/react-native-vector-icons. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-safe-area-context](/en/react-native-safe-area-context.md) to add it to your project.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-vector-icons](/en/react-native-vector-icons.md) to add it to your project.

## Constraints
### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20-CAPI; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Component

View details[Paper](https://callstack.github.io/react-native-paper/docs/components/ActivityIndicator/)

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| ActivityIndicator  | Activity indicator is used to present progress of some activity in the app. It can be used as a drop-in for the ActivityIndicator shipped with React Native | component  | No | iOS/Android      | yes |
| Appbar  | A component to display action items in a bar. It can be placed at the top or bottom | component  | No | iOS/Android      | yes |
| Avatar  | Avatars can be used to represent people in a graphical way | component  | No | iOS/Android      | yes |
| Badge  | Badges are small status descriptors for UI elements | component  | No | iOS/Android      | yes |
| Banner  | Banner displays a prominent message and related actions | component  | No | iOS/Android      | yes |
| BottomNavigation  | BottomNavigation provides quick navigation between top-level views of an app with a bottom navigation bar | component  | No | iOS/Android      | yes |
| Button  | A button is component that the user can press to trigger an action | component  | No | iOS/Android      | yes |
| Card  | A card is a sheet of material that serves as an entry point to more detailed information | component  | No | iOS/Android      | yes |
| Checkbox  | A card is a sheet of material that serves as an entry point to more detailed information | component  | No | iOS/Android      | yes |
| Chip  | Chips are compact elements that can represent inputs, attributes, or actions. They can have an icon or avatar on the left, and a close button icon on the right | component  | No | iOS/Android      | yes |
| DataTable  | Data tables allow displaying sets of data | component  | No | iOS/Android      | yes |
| Dialog  | Dialogs inform users about a specific task and may contain critical information, require decisions, or involve multiple tasks | component  | No | iOS/Android      | yes |
| Divider  | A divider is a thin, lightweight separator that groups content in lists and page layouts | component  | No | iOS/Android    | yes |
| Drawer  | Collapsed component used to show an action item with an icon and optionally label in a navigation drawer | component  | No | iOS/Android    | yes |
| FAB  | A floating action button represents the primary action on a screen. It appears in front of all screen content.  | component  | No | iOS/Android    | yes |
| HelperText  | Helper text is used in conjuction with input elements to provide additional hints for the user  | component  | No | iOS/Android    | yes |
| Icon  | An icon component which renders icon from vector library  | component  | No | iOS/Android    | yes |
| IconButton  | An icon component which renders icon from vector library  | component  | No | iOS/Android    | yes |
| List  | A component used to display an expandable list item  | component  | No | iOS/Android    | yes |
| Menu  | Menus display a list of choices on temporary elevated surfaces. Their placement varies based on the element that opens them  | component  | No | iOS/Android    | yes |
| Modal  | The Modal component is a simple way to present content above an enclosing view. To render the Modal above other components, you'll need to wrap it with the Portal component  | component  | No | iOS/Android    | yes |
| Portal  | Portal allows rendering a component at a different place in the parent tree  | component  | No | iOS/Android    | yes |
| ProgressBar  | Progress bar is an indicator used to present progress of some activity in the app.  | component  | No | iOS/Android    | yes |
| RadioButton  | Radio buttons allow the selection a single option from a set.  | component  | No | iOS/Android    | yes |
| Searchbar  | Searchbar is a simple input box where users can type search queries.  | component  | No | iOS/Android    | yes |
| SegmentedButtons  | Segmented buttons can be used to select options, switch views or sort elements  | component  | No | iOS/Android    | yes |
| Snackbar  | Snackbars provide brief feedback about an operation through a message rendered at the bottom of the container in which it's wrapped  | component  | No | iOS/Android    | yes |
| Surface  | Surface is a basic container that can give depth to an element with elevation shadow  | component  | No | iOS/Android    | yes |
| Surface  | Switch is a visual toggle between two mutually exclusive states — on and off.  | component  | No | iOS/Android    | yes |
| Text  | Typography component showing styles complied with passed variant prop and supported by the type system.  | component  | No | iOS/Android    | yes |
| TextInput  | A component to allow users to input text.  | component  | No | iOS/Android    | yes |
| ToggleButton  | Toggle buttons can be used to group related options. To emphasize groups of related toggle buttons, a group should share a common container  | component  | No | iOS/Android    | yes |
| Tooltip  | Tooltips display informative text when users hover over, focus on, or tap an element  | component  | No | iOS/Android    | yes |
| TouchableRipple  | A wrapper for views that should respond to touches  | component  | No | iOS/Android    | yes |

## Properties

View details[Paper](https://callstack.github.io/react-native-paper/docs/components/ActivityIndicator#animating)

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**ActivityIndicator**：Activity indicator is used to present progress of some activity in the app. It can be used as a drop-in for the ActivityIndicator shipped with React Native
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  animating  |  Whether to show the indicator or hide it   | boolean | NO      | All      | Yes               |
| color  |  The color of the spinner   | string | NO      | All      | Yes               |
| size |  Size of the indicator   |      small \| large \| number     | NO       | All      | Yes               |
|  hidesWhenStopped  |    Whether the indicator should hide when not animating     |     boolean      | NO       | All      | Yes               |
|  theme   |  theme | ThemeProp | NO      | All      | Yes               |
|  style   |  style | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | NO      | All      | Yes               |

**Appbar**：A component to display action items in a bar. It can be placed at the top or bottom
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children   |  Content of the Appbar   | React.ReactNode | NO      | All      | Yes               |
| mode   |  Mode of the Appbar.   | small \| medium \| large \| center-aligned | NO      | All      | Yes               |
| elevated  |  Whether Appbar background should have the elevation along with primary color pigment.   |     boolean      | NO       | All      | Yes               |
|  safeAreaInsets   |   Safe area insets for the Appbar     |     { bottom?: number; top?: number; left?: number; right?: number; }      | NO       | All      | Yes               |
|  theme   |  theme | ThemeProp | NO      | All      | Yes               |
|  style   |  style | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | NO      | All      | Yes               |

**Appbar.Action**：A component used to display an action item in the appbar.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  color   |  Custom color for action icon   | string | NO      | All      | Yes               |
|  rippleColor   |  Color of the ripple effect   | ColorValue | NO      | All      | Yes               |
|  icon    |  Name of the icon to show   | IconSource | Yes      | All      | Yes               |
|  size    | Optional icon size   | number | NO      | All      | Yes               |
|  disabled    | Whether the button is disabled. A disabled button is greyed out and onPress is not called on touch.   | boolean | NO      | All      | Yes               |
|  accessibilityLabel    | Accessibility label for the button. This is read by the screen reader when the user taps the button   | string | NO      | All      | Yes               |
|  onPress    | Whether it's the leading button.   | fuction | NO      | All      | Yes               |
|  isLeading (Available in v5.x with theme version 3)    | Whether it's the leading button.   | boolean | NO      | All      | NO               |
|  style   |  Style for Appbar.Action container | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | NO      | All      | Yes               |
|  ref   |  ref | React.RefObject<View> | NO      | All      | Yes               |
|  theme   |  theme | ThemeProp | NO      | All      | Yes               |

**Appbar.BackAction**：A component used to display a back button in the appbar.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  color   |  Custom color for action icon   | string | NO      | All      | Yes               |
|  size    | Optional icon size   | number | NO      | All      | Yes               |
|  disabled    | Whether the button is disabled. A disabled button is greyed out and onPress is not called on touch.   | boolean | NO      | All      | Yes               |
|  accessibilityLabel    | Accessibility label for the button. This is read by the screen reader when the user taps the button   | string | NO      | All      | Yes               |
|  onPress    | Function to execute on press.   | fuction | NO      | All      | Yes               |
|       style        |            Style for Appbar.BackAction container             | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | NO      | All      | Yes               |
|        ref         |                             ref                              |              React.RefObject<View>               | NO      | All      | Yes               |

**Appbar.Content**：A component used to display a title and optional subtitle in an appbar

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title (required)   |  Text or component for the title.  | React.ReactNode | Yes      | All      | Yes               |
|  titleStyle    | Style for the title, if title is a string.   | StyleProp<TextStyle> | NO      | All      | Yes               |
|  titleRef    | Reference for the title.   | React.RefObject<TextRef> | NO      | All      | Yes               |
|  onPress    | Function to execute on press.   | fuction | NO      | All      | Yes               |
|  disabled    | If true, disable all interactions for this component.   | boolean | NO      | All      | Yes               |
|  color    | Custom color for the text   | string | NO      | All      | Yes               |
|  titleMaxFontSizeMultiplier    | Specifies the largest possible scale a title font can reach   | number | NO      | All      | Yes               |
|  style   |  Style for Appbar.Content container | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | NO      | All      | Yes               |
|           theme            |                            theme                            |                    ThemeProp                     | NO      | All      | Yes               |
|           testID           |                 testID to be used on tests.                 |                      string                      | NO      | All      | Yes               |

**Appbar.Header**：A component to use as a header at the top of the screen. It can contain the screen title, controls such as navigation buttons, menu button etc.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  dark  |  Whether the background color is a dark color. A dark header will render light text and vice-versa  | boolean | NO      | All      | Yes               |
|  statusBarHeight    | Extra padding to add at the top of header to account for translucent status bar   | number | NO      | All      | Yes               |
|  children (required)    | Reference for the title.   | React.ReactNode | Yes      | All      | Yes               |
|  mode     | Mode of the Appbar.   | small \| medium \| large \| center-aligned | NO      | All      | Yes               |
|  elevated      | Whether Appbar background should have the elevation along with primary color pigment   | boolean | NO      | All      | Yes               |
|  ref   |  ref | React.RefObject<View> | NO      | All      | Yes               |
|  theme   |  theme | ThemeProp | NO      | All      | Yes               |
|  testID   |  testID to be used on tests. | string | NO      | All      | Yes               |

**Avatar.Icon**：Avatars can be used to represent people in a graphical way.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)  | Icon to display for the Avatar.  | IconSource | Yes      | All      | Yes               |
|  size  | Size of the avatar.  | number | NO      | All      | Yes               |
|  color  | Custom color for the icon.  | string | NO      | All      | Yes               |
|  style  | style | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  theme   |  theme | ThemeProp | NO      | All      | Yes               |

**Avatar.Image**：Avatars can be used to represent people in a graphical way.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  source (required)  | Image to display for the Avatar. It accepts a standard React Native Image source prop Or a function that returns an Image  | ImageSourcePropType  | Yes      | All      | Yes               |
|  size  | Size of the avatar.  | number | NO      | All      | Yes               |
|  style   |  style | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | NO      | All      | Yes               |
|  onError   |  Invoked on load error. | fuction | NO      | All      | Yes               |
|  onLayout   |  Invoked on mount and on layout changes. | fuction | NO      | All      | Yes               |
|  onLoad   |  Invoked when load completes successfully. | fuction | NO      | All      | Yes               |
|  onLoadEnd   |  Invoked when load either succeeds or fails. | fuction | NO      | All      | Yes               |
|  onLoadStart   |  Invoked on load start. | fuction | NO      | All      | Yes               |
|  onProgress   |  Invoked on download progress. | fuction | NO      | All      | Yes               |
|  theme   | theme  | ThemeProp | NO      | All      | Yes               |

**Avatar.Text**：Avatars can be used to represent people in a graphical way.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  label (required)  | Initials to show as the text in the Avatar.  | string  | Yes      | All      | Yes               |
|  size  | Size of the avatar.  | number | NO      | All      | Yes               |
|  color  | Custom color for the text.  | string | NO      | All      | Yes               |
|  style  | Style for text container  | StyleProp<TextStyle> | NO      | All      | Yes               |
|  labelStyle  | Style for the title.  | StyleProp<TextStyle> | NO      | All      | Yes               |
|  maxFontSizeMultiplier  | Specifies the largest possible scale a text font can reach.  | number | NO      | All      | Yes               |
|  theme   | theme  | ThemeProp | NO      | All      | Yes               |

**Badge**：Badges are small status descriptors for UI elements
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  visible  | Whether the badge is visible  | boolean  | NO      | All      | Yes               |
|  children  | Content of the Badge  | string  \| number | NO      | All      | Yes               |
|  size  | Size of the Badge  |  number | NO      | All      | Yes               |
|  style  | Style for Badge container  | StyleProp<TextStyle> | NO      | All      | Yes               |
|  ref  | ref  | React.RefObject<typeof Animated.Text> | NO      | All      | Yes               |
|  theme   | theme  | ThemeProp | NO      | All      | Yes               |

**Banner**：Banner displays a prominent message and related actions.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  visible  | Whether the badge is visible  | boolean  | Yes      | All      | Yes               |
|  children  | Content of the Badge  |React.ReactNode | NO      | All      | Yes               |
|  icon  | Icon to display for the Banner. Can be an image.  |  IconSource | NO      | All      | Yes               |
|  actions  | Action items to shown in the banner |  Array< { label: string; } | NO      | All      | Yes               |
|  contentStyle  | Style of banner's inner content. Use this prop to apply custom width for wide layouts. |  StyleProp<ViewStyle> | NO      | All      | Yes               |
|  elevation   | Changes Banner shadow and background on iOS and Android.|   Animated.Value | NO      | All      | Yes               |
|  maxFontSizeMultiplier   | Specifies the largest possible scale a text font can reach.|   number | NO      | All      | Yes               |
|  onShowAnimationFinished   | Optional callback that will be called after the opening animation finished running normally|   Animated.EndCallback | NO      | All      | Yes               |
|  onHideAnimationFinished   | Optional callback that will be called after the closing animation finished running normally|   Animated.EndCallback | NO      | All      | Yes               |
|  style  | Style for Badge container  | StyleProp<TextStyle> | NO      | All      | Yes               |
|  ref  | ref  | React.RefObject<typeof Animated.Text> | NO      | All      | Yes               |
|  theme   | theme  | ThemeProp | NO      | All      | Yes               |

**BottomNavigation**：BottomNavigation provides quick navigation between top-level views of an app with a bottom navigation bar.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  shifting  | Whether the shifting style is used, the active tab icon shifts up to show the label and the inactive tabs won't have a label.  | boolean  | NO      | All      | Yes               |
|  labeled  | Whether to show labels in tabs. When false, only icons will be displayed.  |boolean | NO      | All      | Yes               |
|  compact  | Whether tabs should be spread across the entire width.  |  boolean | NO      | All      | Yes               |
|  navigationState (required)  | State for the bottom navigation. The state should contain the following properties|  { index: number; routes: Route[]; } | Yes      | All      | Yes               |
|  onIndexChange (required)  | Callback which is called on tab change, receives the index of the new tab as argument|  (index: number) => void | Yes      | All      | Yes               |
|  renderScene (required)  | Callback which returns a react element to render as the page for the tab |  (props: { route: Route; jumpTo: (key: string) => void; }) => React.ReactNode \| null | Yes      | All      | Yes               |
|  renderIcon  | Callback which returns a React Element to be used as tab icon. | (props: { route: Route; focused: boolean; color: string; }) => React.ReactNode \| null | NO      | All      | Yes               |
|  renderLabel  | Callback which React Element to be used as tab label. | (props: { route: Route; focused: boolean; color: string; }) => React.ReactNode \| null | NO      | All      | Yes               |
|  renderTouchable  | Callback which returns a React element to be used as the touchable for the tab item. | (props: TouchableProps<Route>) => React.ReactNode \| null | NO      | All      | Yes               |
|  getAccessibilityLabel  | Get accessibility label for the tab button. | (props: { route: Route }) => string \| undefined \| null | NO      | All      | Yes               |
|  getBadge  | Get badge for the tab, uses route.badge by default. | (props: { route: Route }) => boolean \| number \| string \| undefined \| null | NO      | All      | Yes               |
|  getColor  | Get color for the tab, uses route.color by default. | (props: { route: Route }) => string \| undefined \| number \| string \| undefined \| null | NO      | All      | Yes               |
|  getLabelText  | Get label text for the tab, uses route.title by default. Use renderLabel to replace label component. | (props: { route: Route }) => string \| undefined \| undefined \| number \| string \| undefined \| null | NO      | All      | Yes               |
|  getTestID  | Get the id to locate this tab button in tests, uses route.testID by default. | (props: { route: Route }) => string \| undefined | NO      | All      | Yes               |
|  getLazy  | Get lazy for the current screen. Uses true by default. | (props: { route: Route }) => string \| undefined | NO      | All      | Yes               |
|  onTabPress  | Function to execute on tab press. It receives the route for the pressed tab, useful for things like scroll to top. | (props: { route: Route } & TabPressEvent) => void | NO      | All      | Yes               |
|  onTabLongPress  | Function to execute on tab long press. It receives the route for the pressed tab, useful for things like custom action when longed pressed. | (props: { route: Route } & TabPressEvent) => void | NO      | All      | Yes               |
|  activeColor  | Custom color for icon and label in the active tab. | string | NO      | All      | Yes               |
|  inactiveColor  | Custom color for icon and label in the inactive tab. | string | NO      | All      | Yes               |
|  sceneAnimationEnabled  | Whether animation is enabled for scenes transitions in shifting mode. | boolean | NO      | All      | Yes               |
|  sceneAnimationEasing  | The scene animation Easing. | EasingFunction \| undefined | NO      | All      | Yes               |
|  sceneAnimationType  | The scene animation effect. Specify 'shifting' for a different effect. By default, 'opacity' will be used. | 'opacity' \| 'shifting' | NO      | All      | Yes               |
|  keyboardHidesNavigationBar  | Whether the bottom navigation bar is hidden when keyboard is shown | boolean | NO      | All      | Yes               |
|  safeAreaInsets  | Safe area insets for the tab bar | { top?: number; right?: number; bottom?: number; left?: number; } | NO      | All      | Yes               |
|  activeIndicatorStyle  | Style for the bottom navigation bar. You can pass a custom background color here | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  labelMaxFontSizeMultiplier  | Specifies the largest possible scale a label font can reach. | number | NO      | All      | Yes               |
|  style  | Style for Badge container  | StyleProp<TextStyle> | NO      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string | NO      | All      | Yes               |

**BottomNavigation.Bar**：A navigation bar which can easily be integrated with React Navigation's Bottom Tabs Navigator.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  shifting  | Whether the shifting style is used, the active tab icon shifts up to show the label and the inactive tabs won't have a label.  | boolean  | NO      | All      | Yes               |
|  labeled  | Whether to show labels in tabs. When false, only icons will be displayed.  |boolean | NO      | All      | Yes               |
|  compact  | Whether tabs should be spread across the entire width.  |  boolean | NO      | All      | Yes               |
|  navigationState (required)  | State for the bottom navigation. The state should contain the following properties|  { index: number; routes: Route[]; } | Yes      | All      | Yes               |
|  renderScene (required)  | Callback which returns a react element to render as the page for the tab |  (props: { route: Route; jumpTo: (key: string) => void; }) => React.ReactNode \| null | Yes      | All      | Yes               |
|  renderIcon  | Callback which returns a React Element to be used as tab icon. | (props: { route: Route; focused: boolean; color: string; }) => React.ReactNode \| null | NO      | All      | Yes               |
|  renderLabel  | Callback which React Element to be used as tab label. | (props: { route: Route; focused: boolean; color: string; }) => React.ReactNode \| null | NO      | All      | Yes               |
|  renderTouchable  | Callback which returns a React element to be used as the touchable for the tab item. | (props: TouchableProps<Route>) => React.ReactNode \| null | NO      | All      | Yes               |
|  getAccessibilityLabel  | Get accessibility label for the tab button. | (props: { route: Route }) => string \| undefined \| null | NO      | All      | Yes               |
|  getBadge  | Get badge for the tab, uses route.badge by default. | (props: { route: Route }) => boolean \| number \| string \| undefined \| null | NO      | All      | Yes               |
|  getColor  | Get color for the tab, uses route.color by default. | (props: { route: Route }) => string \| undefined \| number \| string \| undefined \| null | NO      | All      | Yes               |
|  getLabelText  | Get label text for the tab, uses route.title by default. Use renderLabel to replace label component. | (props: { route: Route }) => string \| undefined \| undefined \| number \| string \| undefined \| null | NO      | All      | Yes               |
|  getTestID  | Get the id to locate this tab button in tests, uses route.testID by default. | (props: { route: Route }) => string \| undefined | NO      | All      | Yes               |
|  onTabPress  | Function to execute on tab press. It receives the route for the pressed tab, useful for things like scroll to top. | (props: { route: Route } & TabPressEvent) => void | NO      | All      | Yes               |
|  onTabLongPress  | Function to execute on tab long press. It receives the route for the pressed tab, useful for things like custom action when longed pressed. | (props: { route: Route } & TabPressEvent) => void | NO      | All      | Yes               |
|  activeColor  | Custom color for icon and label in the active tab. | string | NO      | All      | Yes               |
|  inactiveColor  | Custom color for icon and label in the inactive tab. | string | NO      | All      | Yes               |
|  animationEasing  | The scene animation Easing. | EasingFunction \| undefined | NO      | All      | Yes               |
|  keyboardHidesNavigationBar  | Whether the bottom navigation bar is hidden when keyboard is shown | boolean | NO      | All      | Yes               |
|  safeAreaInsets  | Safe area insets for the tab bar | { top?: number; right?: number; bottom?: number; left?: number; } | NO      | All      | Yes               |
|  barStyle  | Style for the bottom navigation bar. You can pass a custom background color here | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | NO      | All      | Yes               |
|  labelMaxFontSizeMultiplier  | Specifies the largest possible scale a label font can reach. | number | NO      | All      | Yes               |
|  style  | Style for Badge container  | StyleProp<TextStyle> | NO      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string | NO      | All      | Yes               |

**Button**：A button is component that the user can press to trigger an action.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  mode  | Mode of the button. You can change the mode to adjust the styling to give it desired emphasis  | text \| outlined \| contained \| elevated \| contained-tonal | NO      | All      | Yes               |
|  dark  | Whether the color is a dark color. A dark button will render light text and vice-versa. Only applicable for  | boolean | NO      | All      | Yes               |
|  compact  | Use a compact look, useful for text buttons in a row.  | boolean | NO      | All      | Yes               |
|  buttonColor  | Custom button's background color. | string | NO      | All      | Yes               |
|  textColor  | Custom button's text color. | string | NO      | All      | Yes               |
|  rippleColor  | Color of the ripple effect. | ColorValue | NO      | All      | Yes               |
|  loading  | Whether to show a loading indicator. | boolean | NO      | All      | Yes               |
|  icon  | Icon to display for the Button. | IconSource | NO      | All      | Yes               |
|  disabled  | Whether the button is disabled. A disabled button is greyed out and onPress is not called on touch | boolean | NO      | All      | Yes               |
|  children (required)  | Label text of the button. | React.ReactNode | Yes      | All      | Yes               |
|  uppercase  | Make the label text uppercased. Note that this won't work if you pass React elements as children. | boolean | NO      | All      | Yes               |
|  background  | Type of background drawabale to display the feedback (Android). | PressableAndroidRippleConfig | NO      | All      | Yes               |
|  accessibilityLabel  | Accessibility label for the button. This is read by the screen reader when the user taps the button. | string | NO      | All      | Yes               |
|  accessibilityHint  | Accessibility hint for the button. This is read by the screen reader when the user taps the button. | string | NO      | All      | Yes               |
|  accessibilityRole  | Accessibility role for the button. The "button" role is set by default. | AccessibilityRole | NO      | All      | Yes               |
|  onPress  | Function to execute on press. | (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  onPressIn  | Function to execute as soon as the touchable element is pressed and invoked even before onPress. | (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  onPressOut  | Function to execute as soon as the touch is released even before onPress. | (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  onLongPress  | Function to execute on long press. | (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  delayLongPress  | The number of milliseconds a user must touch the element before executing onLongPress. | number | NO      | All      | Yes               |
|  contentStyle  | Style of button's inner content. Use this prop to apply custom height and width and to set the icon on the right with flexDirection: 'row-reverse'. | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  maxFontSizeMultiplier  | Specifies the largest possible scale a text font can reach. | number | NO      | All      | Yes               |
|  style  | Style for Badge Button | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | NO      | All      | Yes               |
|  labelStyle  | Style for the button text. | StyleProp<TextStyle> | NO      | All      | Yes               |
|  theme  | theme | ThemeProp | NO      | All      | Yes               |
|  touchableRef  | Reference for the touchable | React.RefObject<View> | NO      | All      | Yes               |
|  testID  | string | testID to be used on tests. | NO      | All      | Yes               |

**Card**：A card is a sheet of material that serves as an entry point to more detailed information.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  mode  | Mode of the Card.  |  outlined \| contained \| elevated | NO      | All      | Yes               |
|  children (required)  | Content of the Card | React.ReactNode | Yes      | All      | Yes               |
|  onLongPress  | Function to execute on long press. | () => void | NO      | All      | Yes               |
|  onPress  | Function to execute on press | (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  onPressIn  | Function to execute as soon as the touchable element is pressed and invoked even before onPress. | (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  onPressOut  | Function to execute as soon as the touch is released even before onPress. | (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  delayLongPress  | The number of milliseconds a user must touch the element before executing onLongPress. | number | NO      | All      | Yes               |
|  disabled  | TIf true, disable all interactions for this component. | boolean | NO      | All      | Yes               |
|  elevation  | Changes Card shadow and background on iOS and Android. | Animated.Value | NO      | All      | Yes               |
|  contentStyle  | Style of card's inner content. | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  style  | style | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  theme  | theme | ThemeProp | NO      | All      | Yes               |
|  testID  | Pass down testID from card props to touchable | string | NO      | All      | Yes               |
|  accessible  | Pass down accessible from card props to touchable | boolean | NO      | All      | Yes               |

**Card.Actions**：A component to show a list of actions inside a Card.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Items inside the CardActions. |  React.ReactNode | Yes      | All      | Yes               |
|  style  | style |  StyleProp<ViewStyle> | NO      | All      | Yes               |
|  theme  | theme |  ThemeProp | NO      | All      | Yes               |

**Card.Content**：A component to show content inside a Card.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Items inside the Card.Content. |  React.ReactNode | Yes      | All      | Yes               |
|  style  | style |  StyleProp<ViewStyle> | NO      | All      | Yes               |

**Card.Cover**：A component to show a cover image inside a Card.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  Image props  | Extends: ...Image props |  props | NO      | All      | Yes               |
|  style  | style |  StyleProp<ViewStyle> | NO      | All      | Yes               |
|  theme  | theme |  ThemeProp | NO      | All      | Yes               |

**Card.Title**：A component to show a title, subtitle and an avatar inside a Card.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title (required)  | Text for the title. Note that this will only accept a string or <Text>-based node.|  React.ReactNode | Yes      | All      | Yes               |
|  titleStyle  | StyleProp<TextStyle> |  Style for the title. | NO      | All      | Yes               |
|  titleNumberOfLines  | Number of lines for the title. |  number | NO      | All      | Yes               |
|  titleVariant(Available in v5.x with theme version 3)   | Title text variant defines appropriate text styles for type role and its size. Available variants: |  unknown | NO      | All      | Yes               |
|  subtitle   | Text for the subtitle. Note that this will only accept a string or <Text>-based node. |  React.ReactNode | NO      | All      | Yes               |
|  subtitleStyle   | Style for the subtitle. |  StyleProp<TextStyle> | NO      | All      | Yes               |
|  subtitleNumberOfLines   | Number of lines for the subtitle. |  number | NO      | All      | Yes               |
|  subtitleVariant (Available in v5.x with theme version 3)   | Subtitle text variant defines appropriate text styles for type role and its size. Available variants |  unknown | NO      | All      | Yes               |
|  left   | Callback which returns a React element to display on the left side. |  (props: { size: number }) => React.ReactNode | NO      | All      | Yes               |
|  leftStyle   | Style for the left element wrapper. |  StyleProp<ViewStyle> | NO      | All      | Yes               |
|  right   | Callback which returns a React element to display on the right side. |  (props: { size: number }) => React.ReactNode | NO      | All      | Yes               |
|  rightStyle   |Style for the right element wrapper. |  StyleProp<ViewStyle> | NO      | All      | Yes               |
|  titleMaxFontSizeMultiplier   |Specifies the largest possible scale a title font can reach.|  number | NO      | All      | Yes               |
|  subtitleMaxFontSizeMultiplier   |Specifies the largest possible scale a subtitle font can reach.|  number | NO      | All      | Yes               |
|  style   |style|  StyleProp<ViewStyle> | NO      | All      | Yes               |
|  theme   |theme|  ThemeProp | NO      | All      | Yes               |

**Checkbox**：Checkboxes allow the selection of multiple options from a set.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  status (required)  | Status of checkbox.  |  checked \| unchecked \| indeterminate | Yes      | All      | Yes               |
|  disabled  | Whether checkbox is disabled.  |  boolean | NO      | All      | Yes               |
|  onPress  | Function to execute on press.  |  (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  uncheckedColor  | Custom color for unchecked checkbox.  |  string | NO      | All      | Yes               |
|  color  | Custom color for checkbox.  |  string | NO      | All      | Yes               |
|  theme  | theme  |  ThemeProp | NO      | All      | Yes               |
|  testID  | theme  |  string | NO      | All      | Yes               |

**Checkbox.Android**：Checkboxes allow the selection of multiple options from a set. This component follows platform guidelines for iOS, but can be used on any platform.

|       Name        |             Description              |       TypeTouchableRipple props       | Required | Platform | HarmonyOS Support |
| :---------------: | :----------------------------------: | :-----------------------------------: | -------- | -------- | ----------------- |
|  TouchableRipple  |              Touchable               |         TouchableRipple props         | NO       | All      | Yes               |
| status (required) |         Status of checkbox.          | checked \| unchecked \| indeterminate | Yes      | All      | Yes               |
|     disabled      |    Whether checkbox is disabled.     |                boolean                | NO       | All      | Yes               |
|      onPress      |    Function to execute on press.     |  (e: GestureResponderEvent) => void   | NO       | All      | Yes               |
|  uncheckedColor   | Custom color for unchecked checkbox. |                string                 | NO       | All      | Yes               |
|       color       |      Custom color for checkbox.      |                string                 | NO       | All      | Yes               |
|       theme       |                theme                 |               ThemeProp               | NO       | All      | Yes               |
|      testID       |                theme                 |                string                 | NO       | All      | Yes               |

**Checkbox.IOS**：Checkboxes allow the selection of multiple options from a set. This component follows platform guidelines for iOS, but can be used on any platform.

|       Name        |          Description          |                 Type                  | Required | Platform | HarmonyOS Support |
| :---------------: | :---------------------------: | :-----------------------------------: | -------- | -------- | ----------------- |
|  TouchableRipple  |           Touchable           |         TouchableRipple props         | NO       | All      | Yes               |
| status (required) |      Status of checkbox.      | checked \| unchecked \| indeterminate | Yes      | All      | Yes               |
|     disabled      | Whether checkbox is disabled. |                boolean                | NO       | All      | Yes               |
|      onPress      | Function to execute on press. |  (e: GestureResponderEvent) => void   | NO       | All      | Yes               |
|       color       |  Custom color for checkbox.   |                string                 | NO       | All      | Yes               |
|       theme       |             theme             |               ThemeProp               | NO       | All      | Yes               |
|      testID       |             theme             |                string                 | NO       | All      | Yes               |

**Checkbox.Item**：Checkbox.Item allows you to press the whole row (item) instead of only the Checkbox.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  status (required)  | Status of checkbox.  |  checked \| unchecked \| indeterminate | Yes      | All      | Yes               |
|  disabled  | Whether checkbox is disabled.  |  boolean | NO      | All      | Yes               |
|  label (required)  | Label to be displayed on the item. |  string | Yes      | All      | Yes               |
|  onPress  | Function to execute on press. |  fuction | NO      | All      | Yes               |
|  onLongPress  | Function to execute on long press. |  fuction | NO      | All      | Yes               |
|  background  | Type of background drawabale to display the feedback (Android). https://reactnative.dev/docs/pressable#rippleconfig |  PressableAndroidRippleConfig | NO      | All      | Yes               |
|  accessibilityLabel  | Accessibility label for the touchable. This is read by the screen reader when the user taps the touchable. |  string | NO      | All      | Yes               |
|  uncheckedColor  | Custom color for unchecked checkbox. |  string | NO      | All      | Yes               |
|  color  | Custom color for checkbox. |  string | NO      | All      | Yes               |
|  rippleColor  | Color of the ripple effect. |  ColorValue | NO      | All      | Yes               |
|  style  | Additional styles for container View. |  StyleProp<ViewStyle> | NO      | All      | Yes               |
|  labelMaxFontSizeMultiplier  | Specifies the largest possible scale a label font can reach. |  number | NO      | All      | Yes               |
|  labelStyle  | Style that is passed to Label element. |  StyleProp<TextStyle> | NO      | All      | Yes               |
|  labelVariant( Available in v5.x with theme version 3)   | Label text variant defines appropriate text styles for type role and its size. Available variants. |  unknown | NO      | All      | Yes               |
|  theme   | theme |  ThemeProp | NO      | All      | Yes               |
|  testID   | string |  ThemeProp | NO      | All      | Yes               |
|  position   | Checkbox control position. |  leading \| trailing | NO      | All      | Yes               |
|  mode   | Whether <Checkbox.Android /> or <Checkbox.IOS /> should be used. Left undefined <Checkbox /> will be used. |  android \| ios | NO      | All      | Yes               |

**Chip**：Chips are compact elements that can represent inputs, attributes, or actions

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  mode  | Mode of the chip.  |  flat \| outlined  | NO      | All      | Yes               |
|  children (required)  | Text content of the Chip.  |  React.ReactNode | Yes      | All      | Yes               |
|  icon  | Icon to display for the Chip. Both icon and avatar cannot be specified.  |  IconSource | NO      | All      | Yes               |
|  avatar  | Avatar to display for the Chip. Both icon and avatar cannot be specified.  |  React.ReactNode | NO      | All      | Yes               |
|  closeIcon  | Icon to display as the close button for the Chip. The icon appears only when the onClose prop is specified.  |  IconSource | NO      | All      | Yes               |
|  selected  | Whether chip is selected.  |  boolean | NO      | All      | Yes               |
|  selectedColor  | Whether to style the chip color as selected.  |  string | NO      | All      | Yes               |
|  showSelectedOverlay   | Whether to display overlay on selected chip  |  boolean | NO      | All      | Yes               |
|  showSelectedCheck   | Whether to display default check icon on selected chip.  |  boolean | NO      | All      | Yes               |
|  rippleColor   | Color of the ripple effect.  |  ColorValue | NO      | All      | Yes               |
|  disabled   | Whether the chip is disabled.  |  boolean | NO      | All      | Yes               |
|  background   | Type of background drawabale to display the feedback (Android).  |  PressableAndroidRippleConfig | NO      | Android      |No               |
|  accessibilityLabel   | Accessibility label for the chip. This is read by the screen reader when the user taps the chip.  |  string | NO      | All      | Yes               |
|  closeIconAccessibilityLabel   | Accessibility label for the close icon. This is read by the screen reader when the user taps the close icon.  |  string | NO      | All      | Yes               |
|  onPress   | Function to execute on press.  |  (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  onLongPress   | Function to execute on long press.  |   () => void | NO      | All      | Yes               |
|  onPressIn   | Function to execute as soon as the touchable element is pressed and invoked even before onPress.  |   (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  onPressOut   | Function to execute as soon as the touch is released even before onPress.  |   (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  onClose   | Function to execute on close button press. The close button appears only when this prop is specified.  |   () => void | NO      | All      | Yes               |
|  delayLongPress   | The number of milliseconds a user must touch the element before executing onLongPress.  |   number | NO      | All      | Yes               |
|  compact    | Sets smaller horizontal paddings 12dp around label, when there is only label.  |   boolean | NO      | All      | Yes               |
|  elevated     | Whether chip should have the elevation.  |   boolean | NO      | All      | Yes               |
|  textStyle     | Style of chip's text  |   StyleProp<TextStyle> | NO      | All      | Yes               |
|  style     | style  |   Animated.WithAnimatedValue<StyleProp<ViewStyle>> | NO      | All      | Yes |
|  theme     | theme  |   ThemeProp | NO      | All      | Yes               |
|  testID     | Pass down testID from chip props to touchable for Detox tests.  |   string | NO      | All      | Yes               |
|  ellipsizeMode     | Ellipsize Mode for the children text  |   EllipsizeProp | NO      | All      | Yes               |
|  maxFontSizeMultiplier     | Specifies the largest possible scale a text font can reach.  |   number | NO      | All      | Yes               |
|  accessibilityRole     | Default value: 'button'  |  string | NO      | All      | Yes               |

**DataTable**：Data tables allow displaying sets of data.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Content of the DataTable  |  React.ReactNode  | Yes      | All      | Yes               |
|  style     | style  |    StyleProp<ViewStyle> | NO      | All      | Yes |

**DataTable.Cell**：A component to show a single cell inside of a table.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Content of the DataTableCell.  |  React.ReactNode  | Yes      | All      | Yes               |
|  numeric  | Align the text to the right. Generally monetary or number fields are aligned to right.  |  boolean  | NO      | All      | Yes               |
|  onPress  | Function to execute on press.  |  (e: GestureResponderEvent) => void  | NO      | All      | Yes               |
|  style     | Text content style of the DataTableCell.  |    StyleProp<ViewStyle> | NO      | All      | Yes |
|  textStyle  | Text content style of the DataTableCell.  |   StyleProp<TextStyle>  | NO      | All      | Yes               |
|  maxFontSizeMultiplier  | Specifies the largest possible scale a text font can reach. |   number  | NO      | All      | Yes               |
|  testID     | testID to be used on tests.  | string | NO      | All      | Yes |

**DataTable.Header**：A component to display title in table header.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Content of the DataTableHeader.  |  React.ReactNode  | Yes      | All      | Yes               |
|  style     | Text content style of the DataTable.Header.  |    StyleProp<ViewStyle> | NO      | All      | Yes |
|  theme     | theme  | ThemeProp | NO      | All      | Yes |

**DataTable.Pagination**：A component to show pagination for data table.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- |----------|-------------------|
|  page (required)  | The currently visible page (starting with 0).  | number  | Yes      | All      | Yes               |
|  numberOfPages (required)  | The total number of pages.  | number  | Yes      | All      | Yes               |
|  onPageChange (required)  | Function to execute on page change. | (page: number) => void  | Yes      | All      | Yes               |
|  showFastPaginationControls  | Whether to show fast forward and fast rewind buttons in pagination. False by default. | boolean  | NO      | All      | Yes               |
|  paginationControlRippleColor  | Color of the pagination control ripple effect. | ColorValue  | NO      | Android  | NO                |
|  theme     | theme  | ThemeProp | NO      | All      | Yes               |
|  numberOfItemsPerPage  | The current number of rows per page. | number  | NO      | All      | Yes               |
|  numberOfItemsPerPageList  | Options for a number of rows per page to choose from. | Array<number>  | NO      | All      | Yes               |
|  onItemsPerPageChange  | The function to set the number of rows per page. | (numberOfItemsPerPage: number) => void  | NO      | All      | Yes               |
|  dropdownItemRippleColor  | Color of the dropdown item ripple effect. | ColorValue  | NO      | All      | Yes               |
|  selectPageDropdownRippleColor  | Color of the select page dropdown ripple effect. | ColorValue  | NO      | All      | Yes               |
|  selectPageDropdownLabel  | Label text for select page dropdown to display. | React.ReactNode  | NO      | All      | Yes               |
|  selectPageDropdownAccessibilityLabel  | AccessibilityLabel for selectPageDropdownLabel | string  | NO      | All      | Yes               |
|  label  | Label text to display which indicates current pagination. | React.ReactNode  | NO      | All      | Yes               |
|  accessibilityLabel  | AccessibilityLabel for label. | string  | NO      | All      | Yes               |
|  style     | Text content style of the DataTable.Pagination.  |    StyleProp<ViewStyle> | NO      | All      | Yes               |

**DataTable.Row**：A component to show a single row inside of a table.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- |----------| ----------------- |
|  TouchableRipple | Extends: ...TouchableRipple props  | props  | NO      | All      | Yes               |
|  children (required)  | Content of the DataTableRow.  | React.ReactNode  | Yes      | All      | Yes               |
|  onPress  | Function to execute on press.  | (e: GestureResponderEvent) => void  | NO      | All      | Yes               |
|  style     | Text content style of the DataTable.Pagination.  |    StyleProp<ViewStyle> | NO      | All      | Yes |
|  theme     | theme  |  ThemeProp | NO      | All      | Yes |
|  pointerEvents     | pointerEvents passed to the View container, which is wrapping children within TouchableRipple.  |  ViewProps['pointerEvents'] | NO      | Android  | No |

**DataTable.Title**：A component to display title in table header.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Text content of the DataTableTitle.  | React.ReactNode  | Yes      | All      | Yes               |
|  numeric  | Align the text to the right. Generally monetary or number fields are aligned to right.  | boolean  | NO      | All      | Yes               |
|  sortDirection  | Direction of sorting. An arrow indicating the direction is displayed when this is given.  | boolean  | NO      | All      | Yes               |
|  numberOfLines  | The number of lines to show.  | number  | NO      | All      | Yes               |
|  onPress  | Function to execute on press.  | (e: GestureResponderEvent) => void  | NO      | All      | Yes               |
|  style  | Text content style of the DataTableTitle.  | StyleProp<TextStyle>  | NO      | All      | Yes               |
|  textStyle  | Text content style of the DataTableTitle.  | StyleProp<TextStyle>  | NO      | All      | Yes               |
|  maxFontSizeMultiplier  | Specifies the largest possible scale a text font can reach.  | maxFontSizeMultiplier  | NO      | All      | Yes               |
|  theme  |theme  | ThemeProp  | NO      | All      | Yes               |

**Dialog**：Dialogs inform users about a specific task and may contain critical information, require decisions, or involve multiple tasks

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  dismissable  | Determines whether clicking outside the dialog dismiss it.  | boolean  | NO      | All      | Yes               |
|  dismissableBackButton  | Determines whether clicking Android hardware back button dismiss dialog.  | boolean  | NO      | All      | Yes               |
|  onDismiss  | Callback that is called when the user dismisses the dialog.  | () => void  | NO      | All      | Yes               |
|  visible  | Determines Whether the dialog is visible.  | boolean  | NO      | All      | Yes               |
|  children (required)  | Content of the Dialog  | React.ReactNode  | Yes      | All      | Yes               |
|  style  | Text content style of the Dialog.  | StyleProp<TextStyle>  | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |
|  testID  | testID to be used on tests.  | string  | NO      | All      | Yes               |

**Dialog.Actions**：A component to show a list of actions in a Dialog.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Content of the DialogActions.  | React.ReactNode  | Yes      | All      | Yes               |
|  style  | Text content style of the Dialog.Actions.  | StyleProp<TextStyle>  | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |

**Dialog.Content**：A component to show content in a Dialog.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Content of the DialogContent.  | React.ReactNode  | Yes      | All      | Yes               |
|  style  | Text content style of the Dialog.Content.  | StyleProp<TextStyle>  | NO      | All      | Yes               |

**Dialog.Icon**：@supported Available in v5.x with theme version 3 A component to show an icon in a Dialog.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  color  | Custom color for action icon.  | IconSource  | NO      | All      | Yes               |
|  icon (required)  | Name of the icon to show. | IconSource  | Yes      | All      | Yes               |
|  size  | Optional icon size.  | number  | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |

**Dialog.ScrollArea**：A component to show a scrollable content in a Dialog.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Content of the DialogScrollArea.  | React.ReactNode  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |

**Dialog.Title**：A component to show a title in a Dialog.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Title text for the DialogTitle.  | React.ReactNode  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |

**Divider**：A divider is a thin, lightweight separator that groups content in lists and page layouts.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  leftInset   | Whether divider has a left inset.  | boolean  | NO      | All      | Yes               |
|  horizontalInset    |Whether divider has a horizontal inset on both sides.  | boolean  | NO      | All      | Yes               |
|  bold     | Whether divider should be bolded.  | boolean  | NO      | All      | Yes               |
|  style  | Text content style of the Divider.  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |

**Drawer.CollapsedItem**：Collapsed component used to show an action item with an icon and optionally label in a navigation drawer.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  label   | The label text of the item.  | string  | NO      | All      | Yes               |
|  badge   | Badge to show on the icon, can be true to show a dot, string or number to show text.  | string \| number \| boolean  | NO      | All      | Yes               |
|  disabled   | Whether the item is disabled.  | boolean  | NO      | All      | Yes               |
|  focusedIcon    | Icon to use as the focused destination icon, can be a string, an image source or a react component  | IconSource  | NO      | All      | Yes               |
|  unfocusedIcon     | Icon to use as the unfocused destination icon, can be a string, an image source or a react component  | IconSource  | NO      | All      | Yes               |
|  active     | Whether to highlight the drawer item as active.  | boolean  | NO      | All      | Yes               |
|  onPress     | Function to execute on press.  |  (e: GestureResponderEvent) => void  | NO      | All      | Yes               |
|  labelMaxFontSizeMultiplier     | Specifies the largest possible scale a label font can reach.  |  number  | NO      | All      | Yes               |
|  accessibilityLabel     | Accessibility label for the button. This is read by the screen reader when the user taps the button.  |  string  | NO      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string  | NO      | All      | Yes               |

**Drawer.Item**：A component used to show an action item with an icon and a label in a navigation drawer.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  label   | The label text of the item.  | string  | NO      | All      | Yes               |
|  icon   | Icon to display for the DrawerItem.  | IconSource  | NO      | All      | Yes               |
|  active   | Whether to highlight the drawer item as active.  | boolean  | NO      | All      | Yes               |
|  disabled   | Whether the item is disabled.  | boolean  | NO      | All      | Yes               |
|  onPress   | Function to execute on press.  | (e: GestureResponderEvent) => void  | NO      | All      | Yes               |
|  background   | Type of background drawabale to display the feedback (Android).  | PressableAndroidRippleConfig  | NO      | All      | Yes               |
|  accessibilityLabel   | Accessibility label for the button. This is read by the screen reader when the user taps the button.  | string  | NO      | All      | Yes               |
|  right   | Callback which returns a React element to display on the right side. For instance a Badge.  |  (props: { color: string }) => React.ReactNode  | NO      | All      | Yes               |
|  labelMaxFontSizeMultiplier   | Specifies the largest possible scale a label font can reach.  |  number  | NO      | All      | Yes               |
|  rippleColor   | Color of the ripple effect.  |  ColorValue  | NO      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |

**Drawer.Section**：A component to group content inside a navigation drawer.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title   | Title to show as the header for the section.  | string  | NO      | All      | Yes               |
|  children (required)   | Content of the Drawer.Section.  | React.ReactNode  | Yes      | All      | Yes               |
|  showDivider  | Whether to show Divider at the end of the section. True by default.  | boolean  | NO      | All      | Yes               |
|  titleMaxFontSizeMultiplier  | Specifies the largest possible scale a title font can reach. True by default.  | number  | NO      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |

**FAB**：A floating action button represents the primary action on a screen. It appears in front of all screen content.

|            Name            |                         Description                          |                       Type                       | Required | Platform | HarmonyOS Support |
| :------------------------: | :----------------------------------------------------------: | :----------------------------------------------: | -------- | -------- | ----------------- |
|      icon (required)       |                 Icon to display for the FAB.                 |                    IconSource                    | Yes      | All      | Yes               |
|      label (required)      |                   Label for extended FAB.                    |                      string                      | Yes      | All      | Yes               |
|         uppercase          |               Make the label text uppercased.                |                     boolean                      | NO      | All      | Yes               |
|         background         | Type of background drawabale to display the feedback (Android). |           PressableAndroidRippleConfig           | NO      | All      | Yes               |
|     accessibilityLabel     | Accessibility label for the FAB. This is read by the screen reader when the user taps the FAB. |                      string                      | NO      | All      | Yes               |
|     accessibilityState     | Accessibility state for the FAB. This is read by the screen reader when the user taps the FAB. |                AccessibilityState                | NO      | All      | Yes               |
|          animated          |             Whether an icon change is animated.              |                     boolean                      | NO      | All      | Yes               |
|           color            |       Custom color for the icon and label of the FAB.        |                      string                      | NO      | All      | Yes               |
|        rippleColor         |                 Color of the ripple effect.                  |                    ColorValue                    | NO      | All      | Yes               |
|          disabled          | Whether FAB is disabled. A disabled button is greyed out and onPress is not called on touch. |                     boolean                      | NO      | All      | Yes               |
|          visible           |              Whether FAB is currently visible.               |                     boolean                      | NO      | All      | Yes               |
|          loading           |             Whether to show a loading indicator.             |                     boolean                      | NO      | All      | Yes               |
|          onPress           |                Function to execute on press.                 |        (e: GestureResponderEvent) => void        | NO      | All      | Yes               |
|        onLongPress         |              Function to execute on long press.              |        (e: GestureResponderEvent) => void        | NO      | All      | Yes               |
|       delayLongPress       | The number of milliseconds a user must touch the element before executing onLongPress |                      number                      | NO      | All      | Yes               |
|            size            |                  Default value: `'medium'`                   |          'small' \| 'medium' \| 'large'          | NO      | All      | Yes               |
|            mode            | Mode of the `FAB`. You can change the mode to adjust the the shadow: |               'flat' \| 'elevated'               | NO      | All      | Yes               |
|          variant           | Color mappings variant for combinations of container and icon colors. | 'primary'\|'secondary'  \|'tertiary' \|'surface' | NO      | All      | Yes               |
| labelMaxFontSizeMultiplier | Specifies the largest possible scale a label font can reach. |                      number                      | NO      | All      | Yes               |
|           style            |                            style                             |               StyleProp<ViewStyle>               | NO      | All      | Yes               |
|           theme            |                            theme                             |                    ThemeProp                     | NO      | All      | Yes               |
|           testID           |               TestID used for testing purposes               |                      string                      | NO      | All      | Yes               |
|            ref             |                             ref                              |              React.RefObject<View>               | NO      | All      | Yes               |

**AnimatedFAB**：An animated, extending horizontally floating action button represents the primary action in an application.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)   | Icon to display for the FAB.  | IconSource  | Yes      | All      | Yes               |
|  label (required)   | Label for extended FAB.  | string  | Yes      | All      | Yes               |
|  uppercase   | Make the label text uppercased.  | boolean  | NO      | All      | Yes               |
|  background   | Type of background drawabale to display the feedback (Android).  | PressableAndroidRippleConfig  | NO      | All      | Yes               |
|  accessibilityLabel   | Accessibility label for the FAB. This is read by the screen reader when the user taps the FAB.  | string  | NO      | All      | Yes               |
|  accessibilityState   | Accessibility state for the FAB. This is read by the screen reader when the user taps the FAB.  | AccessibilityState  | NO      | All      | Yes               |
|  color   | Custom color for the icon and label of the FAB.  | string  | NO      | All      | Yes               |
|  rippleColor   | Color of the ripple effect.  | ColorValue  | NO      | All      | Yes               |
|  disabled   | Whether FAB is disabled. A disabled button is greyed out and onPress is not called on touch.  | boolean  | NO      | All      | Yes               |
|  visible   | Whether FAB is currently visible.  | boolean  | NO      | All      | Yes               |
|  onPress   | Function to execute on press.  | (e: GestureResponderEvent) => void  | NO      | All      | Yes               |
|  onLongPress   | Function to execute on long press.  | (e: GestureResponderEvent) => void  | NO      | All      | Yes               |
|  delayLongPress   | The number of milliseconds a user must touch the element before executing onLongPress  | number  | NO      | All      | Yes               |
|  iconMode   | Whether icon should be translated to the end of extended FAB or be static and stay in the same place. The default value is dynamic.  | static\| dynamic  | NO      | All      | Yes               |
|  animateFrom   | Indicates from which direction animation should be performed. The default value is right.  | left\| right  | NO      | All      | Yes               |
|  extended   | Whether FAB should start animation to extend.  | boolean  | NO      | All      | Yes               |
|  labelMaxFontSizeMultiplier   | Specifies the largest possible scale a label font can reach.  | number  | NO      | All      | Yes               |
|  variant    | Color mappings variant for combinations of container and icon colors.  | primary\| secondary \| tertiary \| surface | NO      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string  | NO      | All      | Yes               |

**FAB.Group**：A component to display a stack of FABs with related actions in a speed dial.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)   | Icon to display for the FAB.  | IconSource  | Yes      | All      | Yes               |
|  accessibilityLabel   | Accessibility label for the FAB. This is read by the screen reader when the user taps the FAB.  | string  | NO      | All      | Yes               |
|  color   | Custom color for the FAB  | string  | NO      | All      | Yes               |
|  backdropColor   | Custom backdrop color for opened speed dial background.  | string  | NO      | All      | Yes               |
|  rippleColor   | Color of the ripple effect.  | ColorValue  | NO      | All      | Yes               |
|  onPress   | Function to execute on pressing the FAB.  | (e: GestureResponderEvent) => void  | NO      | All      | Yes               |
|  onLongPress   | Function to execute on long pressing the FAB.  | (e: GestureResponderEvent) => void  | NO      | All      | Yes               |
|  toggleStackOnLongPress   | Makes actions stack appear on long press instead of on press.  | boolean  | NO      | All      | Yes               |
|  delayLongPress   | Changes the delay for long press reaction.  | number  | NO      | All      | Yes               |
|  enableLongPressWhenStackOpened   | Allows for onLongPress when stack is opened.  | boolean  | NO      | All      | Yes               |
|  open (required)   | Whether the speed dial is open.  | boolean  | Yes      | All      | Yes               |
|  onStateChange (required)   | Callback which is called on opening and closing the speed dial. The open state needs to be updated when it's called, otherwise the change is dropped.  | (state: { open: boolean }) => void  | Yes      | All      | Yes               |
|  visible (required)   | Whether FAB is currently visible.  | boolean  | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string  | NO      | All      | Yes               |

**HelperText**：Helper text is used in conjuction with input elements to provide additional hints for the user.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  type   | Type of the helper text.  | error\| info | NO      | All      | Yes               |
|  children (required)   | Text content of the HelperText.  | React.ReactNode | Yes      | All      | Yes               |
|  visible   | Whether to display the helper text.  | boolean | NO      | All      | Yes               |
|  padding   | Whether to apply padding to the helper text.  | none\| normal | NO      | All      | Yes               |
|  disabled   | Whether the text input tied with helper text is disabled.  | boolean | NO      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string  | NO      | All      | Yes               |

**Icon**：An icon component which renders icon from vector library.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  size    | Size of icon.  | number | NO      | All      | Yes               |
|  allowFontScaling    | allowFontScaling  | boolean | NO      | All      | No               |
|  source (required)    | Icon to display.  | any | Yes      | All      | Yes               |
|  color    | Color of the icon.  | any | NO      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string  | NO      | All      | Yes               |

**IconButton**：An icon button is a button which displays only an icon without a label.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)    | Icon to display.  | IconSource | Yes      | All      | Yes               |
|  mode     | Mode of the icon button. By default there is no specified mode - only pressable icon will be rendered.  | outlined \| contained \| contained-tonal  | NO      | All      | Yes               |
|  iconColor      | Color of the icon.  | string   | NO      | All      | Yes               |
|  containerColor      | Background color of the icon container.  | string   | NO      | All      | Yes               |
|  rippleColor      | Color of the ripple effect.  | ColorValue   | NO      | All      | Yes               |
|  selected       | Whether icon button is selected. A selected button receives alternative combination of icon and container colors.  | boolean   | NO      | All      | Yes               |
|  size       | Size of the icon.  | number   | NO      | All      | Yes               |
|  disabled       | Whether the button is disabled. A disabled button is greyed out and onPress is not called on touch.  | boolean   | NO      | All      | Yes               |
|  animated       | Whether an icon change is animated.  | boolean   | NO      | All      | Yes               |
|  accessibilityLabel       | Accessibility label for the button. This is read by the screen reader when the user taps the button.  | string   | NO      | All      | Yes               |
|  onPress       | Function to execute on press. | (e: GestureResponderEvent) => void  | NO      | All      | Yes               |
|  ref  | ref  | React.RefObject<View>  | NO      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string  | NO      | All      | Yes               |
|  loading       | Whether to show a loading indicator. | boolean  | NO      | All      | Yes               |

**List.Accordion**：A component used to display an expandable list item.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title (required)    | Title text for the list accordion.  | React.ReactNode | Yes      | All      | Yes               |
|  description    | Description text for the list accordion.  | React.ReactNode | NO      | All      | Yes               |
|  left    | Callback which returns a React element to display on the left side.  | (props: { color: string; style: Style }) => React.ReactNode | NO      | All      | Yes               |
|  right    | Callback which returns a React element to display on the right side.  | (props: { isExpanded: boolean }) => React.ReactNode | NO      | All      | Yes               |
|  expanded    | Whether the accordion is expanded If this prop is provided, the accordion will behave as a "controlled component".  | boolean | NO      | All      | Yes               |
|  onPress    | Function to execute on press.  | (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  onLongPress    | Function to execute on long press.  | (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  delayLongPress    | The number of milliseconds a user must touch the element before executing onLongPress.  | number | NO      | All      | Yes               |
|  children (required)    | Content of the section.  | React.ReactNode | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |
|  background    | Type of background drawabale to display the feedback (Android). | PressableAndroidRippleConfig | NO      | All      | Yes               |
|  style    | Style that is passed to the wrapping TouchableRipple element. | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  titleStyle    | Style that is passed to Title element. | StyleProp<TextStyle> | NO      | All      | Yes               |
|  descriptionStyle    | Style that is passed to Description element. | StyleProp<TextStyle> | NO      | All      | Yes               |
|  rippleColor    | Color of the ripple effect. | ColorValue | NO      | All      | Yes               |
|  titleNumberOfLines    | Truncate Title text such that the total number of lines does not exceed this number. | number | NO      | All      | Yes               |
|  descriptionNumberOfLines    | Truncate Description text such that the total number of lines does not exceed this number. | number | NO      | All      | Yes               |
|  titleMaxFontSizeMultiplier    | Specifies the largest possible scale a description font can reach. | number | NO      | All      | Yes               |
|  id    | Id is used for distinguishing specific accordion when using List. | string \| number | NO      | All      | Yes               |
|  testID    | TestID used for testing purposes | string | NO      | All      | Yes               |
|  accessibilityLabel    | Accessibility label for the TouchableRipple. This is read by the screen reader when the user taps the touchable. | string | NO      | All      | Yes               |
|  pointerEvents    | pointerEvents passed to the View container | ViewProps['pointerEvents'] | NO      | Android      | NO               |

**List.AccordionGroup**：List.AccordionGroup allows to control a group of List Accordions.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  onAccordionPress    | Function to execute on selection change. | (expandedId: string \| number) => void | NO      | All      | Yes               |
|  expandedId    | Id of the currently expanded list accordion | string \| number | NO      | All      | Yes               |
|  children (required)    | React elements containing list accordions | React.ReactNode | Yes      | All      | Yes               |

**List.Icon**：List.AccordionGroup allows to control a group of List Accordions.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)    | Icon to show. | IconSource | Yes      | All      | Yes               |
|  color    | Color for the icon. | string | NO      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |

**ListItem**：A component to show tiles inside a List.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title (required)    | Title text for the list item. |  React.ReactNode | Yes      | All      | Yes               |
|  description    | Description text for the list item or callback which returns a React element to display the description. | React.ReactNode | NO      | All      | Yes               |
|  left    | Callback which returns a React element to display on the left side. | (props: { color: string; style: Style }) => React.ReactNode | NO      | All      | Yes               |
|  right    | Callback which returns a React element to display on the right side. | (props: { color: string; style?: Style }) => React.ReactNode | NO      | All      | Yes               |
|  onPress    | Function to execute on press. |  (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |
|  style    | Style that is passed to the wrapping TouchableRipple element. |  StyleProp<ViewStyle> | NO      | All      | Yes               |
|  contentStyle    | Style that is passed to the container wrapping title and descripton. |   StyleProp<ViewStyle> | NO      | All      | Yes               |
|  titleStyle    | Style that is passed to Title element. |   StyleProp<TextStyle> | NO      | All      | Yes               |
|  descriptionStyle    | Style that is passed to Description element. |   StyleProp<TextStyle> | NO      | All      | Yes               |
|  titleNumberOfLines    | Truncate Title text such that the total number of lines does not exceed this number. |   number | NO      | All      | Yes               |
|  descriptionNumberOfLines    | Truncate Description text such that the total number of lines does not exceed this number. |   number | NO      | All      | Yes               |
|  titleEllipsizeMode    | Ellipsize Mode for the Title. One of 'head', 'middle', 'tail', 'clip'. |   EllipsizeProp | NO      | All      | Yes               |
|  titleMaxFontSizeMultiplier    | Specifies the largest possible scale a title font can reach. |   number | NO      | All      | Yes               |
|  descriptionMaxFontSizeMultiplier    | Specifies the largest possible scale a description font can reach. |   number | NO      | All      | Yes               |
|  descriptionEllipsizeMode    | Ellipsize Mode for the Description. One of 'head', 'middle', 'tail', 'clip'. |   'head' 'middle' 'tail' 'clip' | NO      | All      | Yes               |
|  testID    | TestID used for testing purposes |   string | NO      | All      | Yes               |

**List.Section**：A component used to group list items.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title    | Title text for the section. |  string | NO      | All      | Yes               |
|  children (required)    | Content of the section. |  React.ReactNode | Yes      | All      | Yes               |
|  titleStyle    | Style that is passed to Title element. |  StyleProp<TextStyle> | NO      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |

**List.Subheader**：A component used to display a header in lists.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |
|  style    | Style that is passed to Text element. |  StyleProp<TextStyle> | NO      | All      | Yes               |
|  maxFontSizeMultiplier    | Specifies the largest possible scale a text font can reach. |  number | NO      | All      | Yes               |

**Menu**：Menus display a list of choices on temporary elevated surfaces.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  visible (required)    | Whether the Menu is currently visible. |  boolean | Yes      | All      | Yes               |
|  anchor (required)    | The anchor to open the menu from. In most cases, it will be a button that opens the menu. |  React.ReactNode \| { x: number; y: number } | Yes      | All      | Yes               |
|  anchorPosition    | Whether the menu should open at the top of the anchor or at its bottom. | top \| bottom | NO      | All      | Yes               |
|  statusBarHeight    | Extra margin to add at the top of the menu to account for translucent status bar on Android. If you are using Expo, we assume translucent status bar and set a height for status bar automatically. | number | NO      | Android      | Yes               |
|  onDismiss    | Callback called when Menu is dismissed.  |  fuction | NO      | All      | Yes               |
|  overlayAccessibilityLabel    | Accessibility label for the overlay. This is read by the screen reader when the user taps outside the menu.  |  string | NO      | All      | Yes               |
|  children (required)    | Content of the Menu  |  React.ReactNode | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  contentStyle    | Style of menu's inner content.  |  Animated.WithAnimatedValue<StyleProp<ViewStyle>> | NO      | All      | Yes               |
|  theme   | theme   | InternalTheme  | NO      | All      | Yes               |
|  keyboardShouldPersistTaps    | Inner ScrollView prop  | crollViewProps['keyboardShouldPersistTaps'] | NO      | All      | Yes               |
|  testID  | testID to be used on tests.  | string  | NO      | All      | Yes               |

**Menu.Item**：A component to show a single list item inside a Menu.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title (required)    | Title text for the MenuItem. |  React.ReactNode | Yes      | All      | Yes               |
|  leadingIcon    | Leading icon to display for the MenuItem. |  IconSource | NO      | All      | Yes               |
|  trailingIcon(Available in v5.x with theme version 3)    | Trailing icon to display for the MenuItem. |  IconSource | NO      | All      | Yes               |
|  disabled    | Whether the 'item' is disabled. A disabled 'item' is greyed out and onPress is not called on touch. |  boolean | NO      | All      | Yes               |
|  dense (Available in v5.x with theme version 3)    | Sets min height with densed layout. |  boolean | NO      | All      | Yes               |
|  background    | Type of background drawabale to display the feedback (Android). |  PressableAndroidRippleConfig | NO      | All      | Yes               |
|  onPress    | Function to execute on press. |  (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  titleMaxFontSizeMultiplier    | Specifies the largest possible scale a title font can reach. |  number | NO      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  contentStyle  | contentStyle  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  titleStyle  | titleStyle  | StyleProp<ViewStyle>  | NO      | All      | Yes               |
|  rippleColor  | titleStyle  | ColorValue  | NO      | All      | Yes               |
|  theme   | Color of the ripple effect.   | InternalTheme  | NO      | All      | Yes               |
|  testID    | TestID used for testing purposes|  string | NO      | All      | Yes               |
|  accessibilityLabel    | Accessibility label for the Touchable. |  string | NO      | All      | Yes               |
|  accessibilityState    | Accessibility state for the Touchable.  |  accessibilityState | NO      | All      | Yes               |

**Modal**：The Modal component is a simple way to present content above an enclosing view. 
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  dismissable    | Determines whether clicking outside the modal dismiss it. |  boolean | NO      | All      | Yes               |
|  dismissableBackButton    | Determines whether clicking Android hardware back button dismiss dialog. |  boolean | NO      | All      | Yes               |
|  onDismiss    | Callback that is called when the user dismisses the modal.|  () => void | NO      | All      | Yes               |
|  overlayAccessibilityLabel    | Callback that is called when the user dismisses the modal.|  () => void | NO      | All      | Yes               |
|  visible    | Determines Whether the modal is visible. |  boolean | NO      | All      | Yes               |
|  children (required)    | Content of the Modal. |  React.ReactNode | Yes      | All      | Yes               |
|  contentContainerStyle    | Style for the content of the modal |  Animated.WithAnimatedValue<StyleProp<ViewStyle>> | NO      | All      | Yes               |
|  theme  | theme  | ThemeProp  | NO      | All      | Yes               |
|  style    | Style for the wrapper of the modal. Use this prop to change the default wrapper style or to override safe area insets with marginTop and marginBottom. |  StyleProp<TextStyle> | NO      | All      | Yes |
|  testID    | testID to be used on tests. |  string | NO      | All      | Yes               |

**Portal**：Portal allows rendering a component at a different place in the parent tree.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)    | Content of the Portal. |  React.ReactNode | Yes      | All      | Yes               |
|  theme (required)    | theme |  InternalTheme | Yes      | All      | Yes               |

**Portal.Host**：Portal host renders all of its children Portal elements. 
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)    | Content of the Portal. |  React.ReactNode | Yes      | All      | Yes               |

**ProgressBar**：Progress bar is an indicator used to present progress of some activity in the app.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  animatedValue    |Animated value (between 0 and 1). This tells the progress bar to rely on this value to animate it. Note: It should not be used in parallel with the progress prop. |  number | NO      | All      | Yes               |
|  progress    | Progress value (between 0 and 1). Note: It should not be used in parallel with the animatedValue prop. |  number | NO      | All      | Yes               |
|  color    | Color of the progress bar. The background color will be calculated based on this but you can change it by passing backgroundColor to style prop. |  string | NO      | All      | Yes               |
|  indeterminate    | If the progress bar will show indeterminate progress. |  boolean | NO      | All      | Yes               |
|  visible    | Whether to show the ProgressBar (true, the default) or hide it (false). |  boolean | NO      | All      | Yes               |
|  fillStyle    | Style of filled part of the ProgresBar. |  Animated.WithAnimatedValue<StyleProp<ViewStyle>> | NO      | All      | Yes               |
|  style    | style |  StyleProp<ViewStyle> | NO      | All      | Yes               |
|  theme    | theme |  ThemeProp | NO      | All      | Yes               |
|  testID    | testID to be used on tests. |  string | NO      | All      | Yes               |

**RadioButton**：Radio buttons allow the selection a single option from a set.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  value (required)    | Value of the radio button |  string | Yes      | All      | Yes               |
|  status    | Status of radio button. |  checked \| unchecked | NO      | All      | Yes               |
|  disabled    | Whether radio is disabled. |  boolean | NO      | All      | Yes               |
|  onPress    | Function to execute on press. |  (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  uncheckedColor    | Custom color for unchecked radio. |  string | NO      | All      | Yes               |
|  color    | Custom color for radio. |  string | NO      | All      | Yes               |
|  theme    | theme |  ThemeProp | NO      | All      | Yes               |
|  testID    | testID to be used on tests. |  string | NO      | All      | Yes               |

**RadioButton.Group**：Radio button group allows to control a group of radio buttons.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  onValueChange (required)    | Function to execute on selection change. |  fuction | Yes      | All      | Yes               |
|  value (required)    | Value of the currently selected radio button. |  string | Yes      | All      | Yes               |
|  children (required) | React elements containing radio buttons.|  string | Yes      | All      | Yes               |

**RadioButton.Item**：RadioButton.Item allows you to press the whole row (item) instead of only the RadioButton.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  value (required)    | Value of the radio button. |  string | Yes      | All      | Yes               |
|  label (required)    | Label to be displayed on the item. |  string | Yes      | All      | Yes  |
|  disabled    | Whether radio is disabled. |  boolean | NO      | All      | Yes               |
|  background    | Type of background drawabale to display the feedback (Android). https://reactnative.dev/docs/pressable#rippleconfig |  PressableAndroidRippleConfig | NO      | All      | Yes               |
|  onPress    | Function to execute on press. |  Function | NO      | All      | Yes               |
|  onLongPress    | Function to execute on long press. |  Function | NO      | All      | Yes               |
|  accessibilityLabel    | Accessibility label for the touchable. This is read by the screen reader when the user taps the touchable. |  Function | NO      | All      | Yes               |
|  uncheckedColor    | Custom color for unchecked radio. |  string | NO      | All      | Yes               |
|  color    | Custom color for radio. |  string | NO      | All      | Yes               |
|  rippleColor    | Color of the ripple effect. |  ColorValue | NO      | All      | Yes               |
|  status    | Status of radio button. |  checked \| unchecked | NO      | All      | Yes               |
|  style    | Additional styles for container View. |  StyleProp<ViewStyle> | NO      | All      | Yes               |
|  labelStyle    | Style that is passed to Label element. |  StyleProp<TextStyle> | NO      | All      | Yes               |
|  labelVariant(Available in v5.x with theme version 3)   | Label text variant defines appropriate text styles for type role and its size. Available variants: |  unknown | NO      | All      | Yes               |
|  labelMaxFontSizeMultiplier  | Specifies the largest possible scale a label font can reach. |  number | NO      | All      | Yes               |
|  theme  | theme |  ThemeProp | NO      | All      | Yes               |
|  testID  | testID to be used on tests. |  string | NO      | All      | Yes               |
|  mode  | Whether <RadioButton.Android /> or <RadioButton.IOS /> should be used. Left undefined <RadioButton /> will be used. |  android \| ios | NO      | All      | Yes               |
|  position  | Radio button control position. |  leading \| trailing | NO      | All      | Yes               |

**Searchbar**：Searchbar is a simple input box where users can type search queries.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  placeholder    | Hint text shown when the input is empty. |  string | NO      | All      | Yes               |
|  value (required)    | The value of the text input. |  string | Yes      | All      | Yes               |
|  onChangeText    | Callback that is called when the text input's text changes. |  (query: string) => void | NO      | All      | Yes               |
|  mode(Available in v5.x with theme version 3)    | Search layout mode, the default value is "bar". |  bar \| view | NO      | All      | Yes               |
|  icon    | Icon name for the left icon button (see onIconPress). |  (query: string) => void | NO      | All      | Yes               |
|  onChangeText    | Callback that is called when the text input's text changes. |  IconSource | NO      | All      | Yes               |
|  iconColor    | Custom color for icon, default will be derived from theme |  string | NO      | All      | Yes               |
|  rippleColor    | Color of the ripple effect. |  ColorValue | NO      | All      | Yes               |
|  onIconPress    | Callback to execute if we want the left icon to act as button. |  (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  onClearIconPress    | Callback to execute if we want to add custom behaviour to close icon button. |  (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  searchAccessibilityLabel    | Accessibility label for the button. This is read by the screen reader when the user taps the button. |  string | NO      | All      | Yes               |
|  clearIcon    | Custom icon for clear button, default will be icon close. |  IconSource | NO      | All      | Yes               |
|  clearAccessibilityLabel    | Accessibility label for the button. This is read by the screen reader when the user taps the button. |  string | NO      | All      | Yes               |
|  traileringIcon    | Icon name for the right trailering icon button.  |  IconSource | NO      | All      | Yes               |
|  traileringIconColor    | Custom color for the right trailering icon, default will be derived from theme  |  string | NO      | All      | Yes               |
|  traileringRippleColor    | Color of the trailering icon ripple effect.  |  ColorValue | NO      | All      | Yes               |
|  onTraileringIconPress    | Callback to execute on the right trailering icon button press.  |  (e: GestureResponderEvent) => void | NO      | All      | Yes               |
|  traileringIconAccessibilityLabel    | Accessibility label for the right trailering icon button. This is read by the screen reader when the user taps the button.  |  string | NO      | All      | Yes               |
|  right     | Callback which returns a React element to display on the right side. Works only when mode is set to "bar".  |   (props: { color: string; style: Style; testID: string; }) => React.ReactNode | NO      | All      | Yes               |
|  showDivider    | Whether to show Divider at the bottom of the search. Works only when mode is set to "view". True by default. |  boolean | NO      | All      | Yes               |
|  elevation     | Changes Searchbar shadow and background on iOS and Android. |  Animated.Value | NO      | All      | Yes               |
|  inputStyle    | Set style of the TextInput component inside the searchbar | StyleProp<TextStyle> | NO      | All      | Yes               |
|  style    | style | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | NO      | All      | Yes               |
|  loading    | Custom flag for replacing clear button with activity indicator. | Boolean | NO      | All      | Yes               |
|  testID    | TestID used for testing purposes | string | NO      | All      | Yes               |
|  theme    | theme | string | NO      | All      | Yes               |

**SegmentedButtons**：Segmented buttons can be used to select options, switch views or sort elements.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  buttons (required)    | Buttons to display as options in toggle button. Button should contain the following properties: |  { value: string; icon?: IconSource; disabled?: boolean; accessibilityLabel?: string; checkedColor?: string; uncheckedColor?: string; onPress?: (event: GestureResponderEvent) => void; label?: string; showSelectedCheck?: boolean; style?: StyleProp<ViewStyle>; labelStyle?: StyleProp<TextStyle>; testID?: string; }[] | Yes      | All      | Yes               |
|  density    | Density is applied to the height, to allow usage in denser UIs |  regular | NO      | All      | Yes               |
|  style    | style | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  theme    | theme | string | NO      | All      | Yes               |

**Snackbar**：Snackbars provide brief feedback about an operation through a message rendered at the bottom of the container in which it's wrapped.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  visible (required)    | Whether the Snackbar is currently visible. |  boolean | Yes      | All      | Yes               |
|  action    | Label and press callback for the action button. It should contain the following properties: |  $RemoveChildren<typeof Button> & { label: string; } | NO      | All      | Yes               |
|  icon    | Icon to display when onIconPress is defined. Default will be close icon. | IconSource | NO      | All      | Yes               |
|  rippleColor    | Color of the ripple effect. | ColorValue | NO      | All      | Yes               |
|  onIconPress    | Function to execute on icon button press. The icon button appears only when this prop is specified. | () => void | NO      | All      | Yes               |
|  iconAccessibilityLabel    | Accessibility label for the icon button. This is read by the screen reader when the user taps the button. | string | NO      | All      | Yes               |
|  duration    | The duration for which the Snackbar is shown. | number | NO      | All      | Yes               |
|  onDismiss (required)    | Callback called when Snackbar is dismissed. The visible prop needs to be updated when this is called. | () => void | Yes      | All      | Yes               |
|  children (required)    | Text content of the Snackbar. | React.ReactNode | Yes      | All      | Yes               |
|  maxFontSizeMultiplier    | Specifies the largest possible scale a text font can reach. | number | NO      | All      | Yes               |
|  wrapperStyle    | Style for the wrapper of the snackbar | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  style    | style | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  theme    | theme | string | NO      | All      | Yes               |
|  ref    | ref | React.RefObject<View> | NO      | All      | Yes               |
|  testID    | string | TestID used for testing purposes | NO      | All      | Yes               |

**Surface**：Surface is a basic container that can give depth to an element with elevation shadow. 
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)    | Content of the Surface. |  React.ReactNode | Yes      | All      | Yes               |
|  elevation    | Changes shadows and background on iOS and Android. Used to create UI hierarchy between components. |  Animated.Value | NO      | All      | Yes               |
|  mode    | Mode of the Surface. |  flat \| elevated | NO      | All      | Yes               |
|  theme    | theme | string | NO      | All      | Yes               |
|  ref    | ref | React.RefObject<View> | NO      | All      | Yes               |
|  testID    | string | TestID used for testing purposes | NO      | All      | Yes               |

**Switch**：Switch is a visual toggle between two mutually exclusive states — on and off.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  disabled    | Disable toggling the switch. |  React.ReactNode | NO      | All      | Yes               |
|  value    | Value of the switch, true means 'on', false means 'off'. |  boolean | NO      | All      | Yes               |
|  color    | Custom color for switch. |  string | NO      | All      | Yes               |
|  onValueChange    | Callback called with the new value when it changes. |  Function | NO      | All      | Yes               |
|  style    | style | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  theme    | theme | string | NO      | All      | Yes               |

**Text**：Typography component showing styles complied with passed variant prop and supported by the type system.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  Text props    |  Extends: ...Text props |  props | NO      | All      | Yes               |
|  variant    | Variant defines appropriate text styles for type role and its size. Available variants: |  VariantProp<T> | NO      | All      | Yes               |
|  children (required)    |  Content of the Text. |  React.ReactNode | Yes      | All      | Yes               |
|  style    | style | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  theme    | theme | string | NO      | All      | Yes               |

**TextInput**：A component to allow users to input text.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  mode    | Mode of the TextInput. |  flat \| outlined | NO      | All      | Yes      |
|  left    | left | React.ReactNode | NO      | All      | Yes      |
|  right    | right | React.ReactNode | NO      | All      | Yes      |
|  disabled    | If true, user won't be able to interact with the component. |  boolean | NO      | All      |  Yes      |
|  label    | The text or component to use for the floating label. |  TextInputLabelProp | NO      | All      |  Yes      |
|  placeholder    | Placeholder for the input. |  string | NO      | All      |  Yes      |
|  error    | Whether to style the TextInput with error style. |  boolean | NO      | All      |  Yes      |
|  onChangeText    | Callback that is called when the text input's text changes. Changed text is passed as an argument to the callback handler. |  Function | NO      | All      |  Yes      |
|  selectionColor    | Selection color of the input. On iOS, it sets both the selection color and cursor color. On Android, it sets only the selection color. |  string | NO      | All      |  Yes      |
|  underlineColor    | Inactive underline color of the input. |  string | NO      | All      |  Yes      |
|  activeUnderlineColor    | Active underline color of the input. |  string | NO      | All      |  Yes      |
|  outlineColor    | Active outline color of the input. |  string | NO      | All      | Yes |
|  activeOutlineColor    | Active outline color of the input. |  string | NO      | All      |  Yes      |
|  textColor    | Color of the text in the input. |  string | NO      | All      |  Yes      |
|  dense    | Sets min height with densed layout.  |  boolean | NO      | All      |  Yes      |
|  multiline    | Whether the input can have multiple lines.  |  boolean | NO      | All      |  Yes      |
|  numberOfLines    | The number of lines to show in the input (Android only).  |  number | NO    | Android |  No  |
|  onFocus    | Callback that is called when the text input is focused.  |   (args: any) => void | NO      | All      |  Yes      |
|  onBlur    | Callback that is called when the text input is blurred.  |   (args: any) => void | NO      | All      |  Yes      |
|  render    | Callback to render a custom input component such as react-native-text-input-mask instead of the default TextInput component from react-native.  |   (props: RenderProps) => React.ReactNode | NO      | All      |  Yes      |
|  value    | Value of the text input.  | string | NO      | All      |  Yes      |
|  style    | Pass fontSize prop to modify the font size inside TextInput  |  StyleProp<TextStyle> | NO      | All      |  Yes      |
|  theme    | theme  |  ThemeProp | NO      | All      |  Yes      |
|  testID    | testID to be used on tests.  |  string | NO      | All      |  Yes      |
|  contentStyle    | Pass custom style directly to the input itself. Overrides input style Example: paddingLeft, backgroundColor  |  StyleProp<TextStyle> | NO      | All      |  Yes      |
|  outlineStyle    | Pass style to override the default style of outlined wrapper. Overrides style when mode is set to outlined Example: borderRadius, borderColor  | StyleProp<ViewStyle> | NO      | All      |  Yes      |
|  underlineStyle    | Pass style to override the default style of underlined wrapper. Overrides style when mode is set to flat Example: borderRadius, borderColor  | StyleProp<ViewStyle> | NO      | All      |  Yes      |
|  editable    | editable  | boolean | NO      | All      |  Yes      |

**TextInput.Affix**：A component to allow users to input text.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  text (required)    | Text to show. |  string | Yes      | All      |  Yes      |
|  accessibilityLabel    | Accessibility label for the affix. This is read by the screen reader when the user taps the affix. |  string | NO      | All      | Yes      |
|  textStyle    | Style that is passed to the Text element. |  StyleProp<TextStyle> | NO      | All      |  Yes      |
|  theme    | theme | string | NO      | All      | Yes               |

**TextInput.Icon**：A component to render a leading / trailing icon in the TextInput
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)    | Icon to show. |   IconSource | Yes      | All      |  Yes      |
|  onPress   | Function to execute on press. |  (e: GestureResponderEvent) => void | NO      | All      |  Yes      |
|  forceTextInputFocus    | Whether the TextInput will focus after onPress. |  boolean | NO      | All      |  Yes      |
|  color    | Color of the icon or a function receiving a boolean indicating whether the TextInput is focused and returning the color. | (isTextInputFocused: boolean) => string  | NO      | All      | Yes               |
|  rippleColor    | Color of the ripple effect. | ColorValue | NO      | All      | Yes               |
|  style    | style | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  theme    | theme | string | NO      | All      | Yes               |

**ToggleButton**：Toggle buttons can be used to group related options. 
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)    | Icon to display for the ToggleButton. |   IconSource | Yes      | All      |  Yes      |
|  size    | Size of the icon. |   number | NO      | All      |  Yes      |
|  iconColor    | Custom text color for button. |   string | NO      | All      |  Yes      |
|  rippleColor    | Color of the ripple effect. |   string | NO      | All      |  Yes      |
|  disabled    | Whether the button is disabled. |   boolean | NO      | All      |  Yes      |
|  accessibilityLabel    | Accessibility label for the ToggleButton. This is read by the screen reader when the user taps the button. |   string | NO      | All      |  Yes      |
|  onPress    | Function to execute on press. |  fuction  | NO      | All      |  Yes      |
|  value    | Value of button. |   string | NO      | All      |  Yes      |
|  status    | Status of button. |   checked \| unchecked | NO      | All      |  Yes      |
|  style    | style | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  theme    | theme | string | NO      | All      | Yes               |
|  ref    | ref | React.RefObject<View> | NO      | All      | Yes               |
|  testID    | string | testID to be used on tests. | NO      | All      | Yes               |

**ToggleButton.Group**：Toggle group allows to control a group of toggle buttons. 
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  onValueChange (required)    | Function to execute on selection change. |   (value: Value) => void | Yes      | All      |  Yes      |
|  value (required)    | Value of the currently selected toggle button. |   Value \| null | Yes      | All      |  Yes      |
|  children (required)    | React elements containing toggle buttons. |   React.ReactNode | Yes      | All      |  Yes      |

**ToggleButton.Row**：Toggle button row renders a group of toggle buttons in a row.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  onValueChange (required)    | Function to execute on selection change. |   (value: Value) => void | Yes      | All      |  Yes      |
|  value (required)    | Value of the currently selected toggle button. |   string | Yes      | All      |  Yes      |
|  children (required)    | React elements containing toggle buttons. |   React.ReactNode | Yes      | All      |  Yes      |
|  style    | style | StyleProp<ViewStyle> | NO      | All      | Yes               |

**Tooltip**：Tooltips display informative text when users hover over, focus on, or tap an element.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)   | Tooltip reference element. Needs to be able to hold a ref. |   React.ReactElement | Yes      | All      |  Yes      |
|  enterTouchDelay   | The number of milliseconds a user must touch the element before showing the tooltip. |   number | NO      | All      |  Yes      |
|  leaveTouchDelay   | The number of milliseconds after the user stops touching an element before hiding the tooltip. |   number | NO      | All      |  Yes      |
|  title (required)   | Tooltip title |   string | Yes      | All      |  Yes      |
|  titleMaxFontSizeMultiplier   | Specifies the largest possible scale a title font can reach. |   number | NO      | All      |  Yes      |
|  theme    | theme | string | NO      | All      | Yes               |

**TouchableRipple**：A wrapper for views that should respond to touches. 
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  borderless   | Whether to render the ripple outside the view bounds. |   boolean | No     | Android |  No    |
|  background   | Type of background drawabale to display the feedback. |   Object | NO      | All      |  Yes      |
|  centered   | Whether to start the ripple at the center (Web). |   boolean | No    | Web   |  No    |
|  disabled   | Whether to prevent interaction with the touchable. |   boolean | NO      | All      |  Yes      |
|  onPress   | Function to execute on press. If not set, will cause the touchable to be disabled. |   (e: GestureResponderEvent) => void | NO      | All      |  Yes      |
|  onLongPress   | Function to execute on long press. |   (e: GestureResponderEvent) => void | NO      | All      |  Yes      |
|  onPressIn   | Function to execute immediately when a touch is engaged, before onPressOut and onPress. |   (e: GestureResponderEvent) => void | NO      | All      |  Yes      |
|  onPressOut   | Function to execute when a touch is released. |   (e: GestureResponderEvent) => void | NO      | All      |  Yes      |
|  rippleColor   | Color of the ripple effect. |   ColorValue | NO      | All      |  Yes      |
|  underlayColor   | Color of the underlay for the highlight effect. |   string | NO      | All      |  Yes      |
|  children (required)   | Content of the TouchableRipple. |   ((state: PressableStateCallbackType) => React.ReactNode) \| React.ReactNode | Yes      | All      |  Yes      |
|  style    | style | StyleProp<ViewStyle> | NO      | All      | Yes               |
|  theme    | theme | string | NO      | All      | Yes               |

## Known Issues

## Others
- The allowFontScaling property on the Icon component does not take effect. Upon reviewing the source code, this property is not passed to the internal icon component. [Source code location](https://github.com/callstack/react-native-paper/blob/v5.12.3/src/components/Icon.tsx#L153) 
- The mode property in the Menu component is a new addition in version[5.12.4 Version added](https://github.com/callstack/react-native-paper/releases/tag/v5.12.4),and the current version is 5.12.3.
- The statusBarHeight property in the Menu component has no effect, as this property is exclusive to the Android platform. [Source code location](https://github.com/callstack/react-native-paper/blob/v5.12.3/src/components/Menu/Menu.tsx#L447)
- The ripple effect produced by the DataTableRow component using TouchableRipple works on Android but not on iOS.
- The DataTableRow component currently has no effect when using pointerEvents on HarmonyOS RN.
- The safeAreaInset top property in BottomNavigation has no effect because it is not used in the source code. [Source code location](https://github.com/callstack/react-native-paper/blob/v5.12.3/src/components/BottomNavigation/BottomNavigationBar.tsx#L580) 
- The keyboardHidesNavigationBar property in the BottomNavigation.Bar component is passed from the parent component BottomNavigation and should not be used standalone.
- The accessibilityState property is not supported in HarmonyOS RN (5.0.0.700).
- The DataTable component uses the HarmonyOS RN Text component underneath, and currently, the Text component does not support the accessibilityLabel property. Therefore, the accessibility read-out functionality of DataTable on HarmonyOS RN differs from other platforms.


## License

This project is licensed under [The MIT License (MIT)](https://github.com/callstack/react-native-paper/blob/main/LICENSE.md) .
