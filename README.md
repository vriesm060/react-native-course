# React Native Course
Following a React Native course from Udemy

## Apps
* [TODO App](https://github.com/vriesm060/todo-app)
* [News App](https://github.com/vriesm060/news-app)

## Differences between Expo CLI and React Native CLI

| Expo CLI                                         | React Native CLI                                                 |
| ------------------------------------------------ | ---------------------------------------------------------------- |
| Managed workflow                                 | Manually install and configure some dependencies                 |
| Same installation steps on Mac, Windows or Linux | The instructions are different depending on the operating system |
| Limited to the Expo ecosystem                    | Full flexibility                                                 |

You can switch between the two at any time.

## Setup

`expo init my-app-name`

Android Emulator for both Mac and Windows.
iOS Simulator only for Mac.

In React Native you style your components using JS.
You therefore use camelCase instead of hyphens.

## Features

### State
You use state to store values that can change in a component.

### React Hooks
For functional components.

`const [todoItem, setTodoItem] = useState('');`

Declare a state with a variable (todoItem) and a function (setTodoItem) that takes a default value ('').

### Spread operator
Generates a copy of the existing variable.

`...todoList`

## Styling in React Native

Styling is done using flexbox.
A big difference from the web is the axis working with flexbox. The main axis in React Native is the y-axis, and the cross axis is the x-axis. Opposite of the web.

So, in React Native, applying `justifyContent: center` means the flex items will be centered vertically, along the main (y) axis, as opposed to the web.

### Platform specific styles
`backgroundColor: Platform.OS === 'ios' ? '#72bcd4' : '#fff',`

### Images in React Native
`<Image source={require('../../assets/news.jpeg')} />`
Using require. Locally.
From the web:
`source={{uri: 'https://www.conchovalleyhomepage.com/wp-content/uploads/sites/83/2020/05/BREAKING-NEWS-GENERIC-1.jpg?w=1920&h=1080&crop=1'}}`

### Fonts in React Native
Install expo-font and import it as follows: `import * as Font from 'expo-font';`.

Loading the local fonts you want to use using the following function:
```
const loadFonts = () => {
  return Font.loadAsync({
    'Bree Serif': require('./assets/fonts/breeserif_regular.otf'),
  });
}
```

Since loading the fonts is an async function, the app has to wait untill the fonts are done loading before we show the components.
To do this, we make use of a splashscreen component from Expo and remove this component when the loading is done.

```
const [fontLoaded, setFontLoaded] = useState(false);

if (!fontLoaded) {
  return (
    <AppLoading
      startAsync={loadFonts}
      onFinish={() => setFontLoaded(true)}
    />
  );
}
```

### Icons in React Native
Import icons from expo library: `import { MaterialIcons } from '@expo/vector-icons';`.