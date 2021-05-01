# React Native Course
Following a React Native course from Udemy

## Apps
* [TODO App](https://github.com/vriesm060/todo-app)
* [News App](https://github.com/vriesm060/news-app)
* [Home Listing App](https://github.com/vriesm060/home-listing-app)

## Differences between Expo CLI and React Native CLI

| Expo CLI                                         | React Native CLI                                                 |
| ------------------------------------------------ | ---------------------------------------------------------------- |
| Managed workflow                                 | Manually install and configure some dependencies                 |
| Same installation steps on Mac, Windows or Linux | The instructions are different depending on the operating system |
| Limited to the Expo ecosystem                    | Full flexibility                                                 |

You can switch between the two at any time.

---

## Setup

`expo init my-app-name`

Android Emulator for both Mac and Windows.
iOS Simulator only for Mac.

In React Native you style your components using JS.
You therefore use camelCase instead of hyphens.

---

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

---

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

---

## Navigation in React Native
Use React Navigation package.

Three types of navigation:

* **Stack navigation**
  Move from one page to the other by stacking screens ontop of each other.
* **Tabs navigation**
  Move to different screens as tabs.
* **Drawer navigation**
  Create a hamburger menu with drawers.

### Stack Navigator
```
const Stack = createStackNavigator();

function AppNavigator() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

Create a stack navigator tree using createStackNavigator function.

`<Stack.Screen name="NewsList" component={NewsListScreen} />`

Setup a screen as part of a stack navigator.
Name is relevant for moving between one screen to another.

Using React Navigation will give screens a navigation prop, which has methods like goBack and navigate.

Navigate will automatically give a back button.

**Moving between screens like this:**
`props.navigation.navigate('NewsDetails')`

### Tabs navigation

```
<Tabs.Navigator>
  <Tabs.Screen name="Home" component={HomeNavigator} />
  <Tabs.Screen name="Favorites" component={FavoritesNavigator} />
</Tabs.Navigator>
```

You can use tab navigation to navigate between different stacks, which can contain screens.

### Drawer navigation

```
<Drawer.Navigator>
  <Drawer.Screen name="News" component={TabsNavigator} />
  <Drawer.Screen name="About" component={AboutScreen} />
</Drawer.Navigator>
```

Creates a drawer coming in by default from the left of the screen when dragging from left to right.

**Add a hamburger menu:**

Import useNavigation component which will give access to the navigation props.
This way we can create a hamburger menu to open up the drawer.

```
const HeaderLeft = () => {
  const navigation = useNavigation();

  return (
    <MaterialIcons name="menu" size={24} onPress={() => navigation.openDrawer()} />
  );
}
```

---

## State management with Redux

Redux makes it easy to manage the state (data) of an application. With Redux, the state is kept in a central **store**, accessibe to every component that needs to use it.

**Flow:**
A component can trigger an event. This event can be dispatched to a reducer, which updates the state in the central Redux store. From there the updated states are passed back to the connected components.

* Action folder
* Reducer folder

Make use of combineReducers to combine all the reducers in the store.

```
const rootReducer = combineReducers({
  news: newsReducer,
});
```

Create the store using `createStore(rootReducer, middleware)`.

Use the store as a `<Provider></Provider>` component, wrapper the App.

### Setting up reducers

Reducers are JS functions that take two parameters: state and actions.

```
const initialState = {
  articles: [],
  favorites: [],
}

export default function (state = initialState, action) {
  return state;
}
```

### Redux Actions
Redux Actions are JS objects with **type** and **payload**. The **type** property describes how the state should change. The **payload** property discribes what should change and can be omitted if you don't have new data to save in the store.

You use identifiers to describe the actions that will happen, like so:
`export const FETCH_ARTICLES = 'FETCH_ARTICLES';`

**Action:**
```
export const fetchArticles = () => {
  return {
    type: FETCH_ARTICLES,
    payload: {
      id: 1,
      title: 'Sport news',
      description: 'Sport news is on'
    }
  };
}
```

You can make HTTP requests and fetch other type of data in the actions part of Redux, so you can use it in the state.

### Use Redux in components
Using `useSelector` we can select data from the state.
With useDispatch we can dispatch actions to the reducer.

Dispatch an action:
```
const dispatch = useDispatch();

useEffect(() => {
  dispatch(newsAction.fetchArticles());
}, [dispatch]);
```

And use the data from the store:
`const articles = useSelector(state => state.news.articles);`

---

## Building web server using express and MongoDB

### Setup MongoDB with schema

**Schema:**
```
const mongoose = require('mongoose');

const HouseSchema = new mongoose.Schema({
  title:        { type: String, required: true },
  address:      { type: String, required: true },
  homeType:     { type: String },
  description:  { type: String },
  price:        { type: Number, required: true },
  image:        { type: String },
  yearBuilt:    { type: Number },
});

module.exports = mongoose.model('House', HouseSchema);
```

**Routing:**
```
const express = require('express');
const House = require('../models/House');

const router = express.Router();

router.post('/', (req, res) => {
  const house = new House({
    title: req.body.title,
    address: req.body.address,
    homeType: req.body.homeType,
    description: req.body.description,
    price: req.body.price,
    image: req.body.image,
    yearBuilt: req.body.yearBuilt,
  });

  house.save()
    .then(result => {
      res.send({
        message: 'House data created successfully',
        data: result
      });
    })
    .catch(err => console.log(err));
});

module.exports = router;
```