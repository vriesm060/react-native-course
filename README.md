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

**Validation:**
```
router.post('/', [
  check('title')
    .isLength({ min: 3, max: 50 })
    .withMessage('Title should be between 3 and 50 characters.');
], (req, res) => {
  const errors = validationResult(req);
  if (!errors.isEmpty()) return res.status(422).send({ errors: errors.array() });

  ...
});
```

---

## Combining React Native frontend with Node JS Backend

I setup a React Native app for the home listing App using the React Native features I've learned in previous sections. Setting it up with a stack and tab navigation.

### Connect React Native to the server

Fetch the data from the server in an action and pass this data through the reducer to the components that will take it in.

```
export const fetchHouses = () => {
  return async dispatch => {

    const result = await fetch('http://localhost:3000/api/houses');
    const resultData = await result.json();

    dispatch({
      type: FETCH_HOUSES,
      payload: resultData,
    });
  }
}
```

### Add a form to post data to the server

React Native form is build using Formik.

```
<Formik
  initialValues={{
    title: '',
    image: '',
    homeType: '',
    price: '',
    yearBuilt: '',
    address: '',
    description: '',
  }}
  validationSchema={formSchema}
  onSubmit={(values) => {
    dispatch(houseAction.createHome(values))
      .then(() => {
        Alert.alert('Created successfully');
      })
      .catch(() => {
        Alert.alert('An error occurred. Please try again.');
      });
  }}
>
  {(props) => (
    <View style={styles.form}>
      <View style={styles.formGroup}>
        <Text style={styles.label}>Title</Text>
        <TextInput
          style={styles.input}
          onChangeText={props.handleChange('title')}
          onBlur={props.handleBlur('title')}
          value={props.values.title}
        />
        <Text style={styles.error}>{ props.touched.title && props.errors.title }</Text>
      </View>

      ...

      <View style={styles.buttonContainer}>
        <Button
          title="Add Home"
          onPress={props.handleSubmit}
        />
      </View>
    </View>
  )}
</Formik>
```

### Add validation to form in react native

We use Yup to validate the React Native form.

Define a schema for the validation.
```
const formSchema = yup.object({
  title: yup.string().required().min(3).max(50),
  price: yup.number().required(),
  yearBuilt: yup.number().required(),
  image: yup.string().required(),
  address: yup.string().required(),
  description: yup.string().required(),
});
```

### Add post request to the server

Post the form data to the server using fetch. We do this in the action.

```
export const createHome = ({ title, image, homeType, price, yearBuilt, address, description }) => {
  return async dispatch => {
    const response = await fetch('http://localhost:3000/api/houses', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        title,
        image,
        homeType,
        price,
        yearBuilt,
        address,
        description,
      })
    });

    const responseData = await response.json();

    dispatch({
      type: CREATE_HOUSES,
      payload: responseData,
    });
  }
}
```

This action is passed through the reducer and back to the components.

---

## Authentication system

### The setup
A client (App) sends a request with authentication to the server. In response it gets a token. This token is stored on the client side and gets send to the server on subsequent requests whenever the client wants to make a request to the server. 

This is the authentication system we will build.

### Building the user register request
```
router.post('/register', async (req, res) => {
  const user = new User({
    fullName: req.body.fullName,
    email: req.body.email,
    password: req.body.password,
  });

  try {
    const savedUser = await user.save();
    res.send(savedUser);
  } catch (err) {
    res.status(400).send(err);
  }
});
```

We add validation and secure the password in the database by hashing it.
For the hashing we use the bcryptjs package.

**Hashing password:**
```
// Hash the password:
const salt = await bcrypt.genSalt();
const hashPassword = await bcrypt.hash(req.body.password, salt);
```

**Check if email already exists:**
```
const userExists = await User.findOne({ email: req.body.email });
if (userExists) return res.status(400).send('Email already exists.');
```

### Building the login request
```
router.post('/login', loginValidate, async (req, res) => {
  // Validate form:
  const errors = validationResult(req);
  if (!errors.isEmpty()) return res.status(422).json({ errors: errors.array() });

  // Check if email exists:
  const user = await User.findOne({ email: req.body.email });
  if (!user) return res.status(404).send('Invalid email or password');

  // Check if password is correct:
  const validPassword = await bcrypt.compare(req.body.password, user.password);
  if (!validPassword) return res.status(404).send('Invalid email or or password');

  res.send('logged in');
});
```

### Setting up JSON web tokens
Using the jsonwebtoken package we can create a web token, like:

```
const token = jwt.sign({ _id: user._id, email: user.email }, secret);
res.header('auth-token', token).send({ message: 'Logged in successfully!', token });
```

### Protecting a route
To protect a route, we use a middleware to verify the token that we get back from our authentication request.

```
module.exports = function (req, res, next) {
  const token = req.header('auth-token');
  if (!token) return res.status(401).send('Access denied.');

  // Verify the token:
  try {
    const verified = jwt.verify(token, secret);
    req.user = verified;
    next();
  } catch (err) {
    res.status(400).send('Invalid token.');
  }
}
```

### React Native frontend for authentication app
Using the secureTextEntry property for TextInput, we can secure the password input.
