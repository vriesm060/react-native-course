# React Native Course
*Following a React Native course from Udemy.*

---

# Apps :iphone:
*Click on any of the links to go to the project repositories.*

[1.0]: https://github.com/vriesm060/todo-app
[2.0]: https://github.com/vriesm060/news-app
[3.0]: https://github.com/vriesm060/home-listing-app
[3.1]: https://github.com/vriesm060/home-listing-app-client
[3.2]: https://github.com/vriesm060/home-listing-app/tree/master/server
[4.0]: https://github.com/vriesm060/authentication-system-app
[4.1]: https://github.com/vriesm060/authentication-system-app-client
[4.2]: https://github.com/vriesm060/authentication-system-app/tree/master/server

| [Todo App][1.0] | [News App][2.0] | [Home Listing App][3.0] | [Authentication System App][4.0] |
| :-------------- | :-------------- | :---------------------- | :------------------------------- |
| [Client][1.0]   | [Client][2.0]   | [Client][3.1]           | [Client][4.1]                    |
|                 |                 | [Server][3.2]           | [Server][4.2]                    |

---

# Table of contents :page_facing_up:
* **[Setup](#setup)**
  * [Expo init](#expo-init)
* **[Features](#features)**
  * [State](#state)
  * [React Hooks](#react-hooks)
  * [Spread operator](#spread-operator)
* **[Styling in React Native](#styling-in-react-native)**
  * [Platform specific styles](#platform-specific-styles)
  * [Images in React Native](#images-in-react-native)
  * [Fonts in React Native](#font-in-react-native)
  * [Icons in React Native](#icons-in-react-native)
* **[Navigation in React Native](#navigation-in-react-native)**
  * [Three types of navigation](#three-types-of-navigation)
  * [Stack Navigator](#stack-navigator)
  * [Tabs navigation](#tabs-navigation)
  * [Drawer navigation](#drawer-navigation)
* **[State management with Redux](#state-management-with-redux)**
  * [Flow](#flow)
  * [Setting up reducers](#setting-up-reducers)
  * [Redux Actions](#redux-actions)
  * [Use Redux in Components](#use-redux-in-components)
* **[Building web server using Express and MongoDB](#building-web-server-using-express-and-mongodb)**
  * [Setup MongoDB with schema](#setup-mongodb-with-schema)
  * [Routing](#routing)
* **[Combining React Native frontend with NodeJS Backend](#combining-react-native-frontend-with-nodejs-backend)**
  * [Connect React Native to the server](#connect-react-native-to-the-server)
  * [Add a form to post data to the server](#add-a-form-to-post-data-to-the-server)
  * [Add validation to form in react native](#add-validation-to-form-in-react-native)
  * [Add post request to the server](#add-post-request-to-the-server)
* **[Authentication system server side](#authentication-system-server-side)**
  * [The setup](#the-setup)
  * [Building the user register request](#building-the-user-register-request)
  * [Building the login request](#building-the-login-request)
  * [Setting up JSON web tokens](#setting-up-json-web-tokens)
* **[Authentication system client side](#authentication-system-client-side)**
  * [Register a user using React Native and NodeJS](#register-a-user-using-react-native-and-nodejs)
  * [Storing tokens using AsyncStorage](#storing-tokens-using-asyncstorage)
* **[Deploying React Native Apps](#deploying-react-native-apps)**
  * [For iOS](#for-ios)
  * [For Android](#for-android)

---

# Setup
In order to run React Native on your computer, you can either use the **React Native CLI** or the **Expo CLI**. For this course I'm using Expo, since it is easier to start out with. The React Native CLI is better for more experienced React Native developers. Both CLIs have pros and cons.

**Differences between Expo CLI and React Native CLI**
| Expo CLI                                         | React Native CLI                                                 |
| :----------------------------------------------- | :--------------------------------------------------------------- |
| Managed workflow                                 | Manually install and configure some dependencies                 |
| Same installation steps on Mac, Windows or Linux | The instructions are different depending on the operating system |
| Limited to the Expo ecosystem                    | Full flexibility                                                 |

*You can switch between the two at any time.*

## Expo init
Once you have installed the **Expo CLI**, creating a new project is as simple as running the command `expo init my-app-name`.
You will be taken through some initializing steps after which your Expo project gets installed.

In order to test and run applications, you'll need an **Android Emulator**, which you can install from the [Android Studio](https://developer.android.com/studio) and/or the **iOS Simulator**, which you can install using [Xcode](https://developer.apple.com/xcode/).

>Android Emulator can be used on both Windows and Mac, iOS Simulator only on a Mac.

You can run your Expo project using the command `expo start`. This will bring up the React Native Dev Tools in a browser window. In here you can run your app on either the Android Emulator or iOS Simulator. This can also be done by pressing `a` or `i` in the terminal respectively.

---

# Features

## State
In React Native, just like in React JS, you use state in a component to store values that can change over time.

## React Hooks
When you use functional components in React JS or React Native, you can use React Hooks in place of constructor and functions like componentDidMount, which are used in class based components.

Declaring a state variable using React Hooks is done like this:

`const [todoItem, setTodoItem] = useState('');`

*Declare a state with a variable (todoItem) and a function (setTodoItem) that takes a default value ('').*

## Spread operator
Generates a copy of the existing variable.

`...todoList`

---

# Styling in React Native
In React Native you style your components using JavaScript. You therefore use **camelCase** instead of hyphens. Styling is done using flexbox. A big difference from the web is the axis working with flexbox. The main axis in React Native is the y-axis, and the cross axis is the x-axis. Opposite of using flexbox for the web.

So, in React Native, applying `justifyContent: center` means the flex items will be centered vertically, along the main (y) axis, as opposed to the web.

## Platform specific styles
Both iOS and Android have their own way of styling components. Often you want to style components the same way for both platforms, but if you want to apply a specific style, you can: 

`backgroundColor: Platform.OS === 'ios' ? '#72bcd4' : '#fff',`

## Images in React Native
The core component `<Image />` has two ways of requiring a source, locally and from the web.

**Requiring a local source:**

`<Image source={require('../../assets/news.jpeg')} />`

**Requiring a source from the web:**

`source={{uri: 'https://www.conchovalleyhomepage.com/wp-content/uploads/sites/83/2020/05/BREAKING-NEWS-GENERIC-1.jpg?w=1920&h=1080&crop=1'}}`

## Fonts in React Native
In order to use custom fonts, locally or from the web, you need to load them into your app first.
Install **expo-font** and import it: `import * as Font from 'expo-font';`.

Using the following async function you can load in your fonts:
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

## Icons in React Native
Import icons from the expo library: `import { MaterialIcons } from '@expo/vector-icons';`.

---

# Navigation in React Native
Navigation in React Native is done by using the React Navigation packages. Install the following packages:

`yarn add @react-navigation/native`

`yarn add react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view`

## Three types of navigation
In React Native there are three different types of navigation.

* **Stack navigation:**  
  Move from one page to the other by stacking screens ontop of each other.
* **Tabs navigation:**  
  Move to different screens as tabs. Tabs are usually placed on the bottom of the screen.
* **Drawer navigation:**  
  Create a hamburger menu button which reveals a drawer style menu from the side. Also natively accessible by swiping from the side of the screen.

## Stack Navigator
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

Create a stack navigator tree using the **createStackNavigator** function. Within this tree you can then place the different screens available, like so:

`<Stack.Screen name="NewsList" component={NewsListScreen} />`

Setup a screen as part of a stack navigator. The name is relevant for moving between one screen to another in the navigator and give it a component to render. 

>Using React Navigation will give screens a navigation prop, which has methods like goBack and navigate. Navigate will automatically give the screen a back button. You have the option to turn this off.

You can move between screens within a stack by using the `navigate` method:

`props.navigation.navigate('NewsDetails')`

## Tabs navigation
```
<Tabs.Navigator>
  <Tabs.Screen name="Home" component={HomeNavigator} />
  <Tabs.Screen name="Favorites" component={FavoritesNavigator} />
</Tabs.Navigator>
```

You can use tab navigation to navigate between different stacks, each containing screens.

## Drawer navigation
```
<Drawer.Navigator>
  <Drawer.Screen name="News" component={TabsNavigator} />
  <Drawer.Screen name="About" component={AboutScreen} />
</Drawer.Navigator>
```

Creates a drawer coming in by default from the left of the screen when swiping from left to right.

### Add a hamburger menu
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

# State management with Redux
Redux makes it easy to manage the state (data) of an application. With Redux, the state is kept in a central **store**, accessible to every component that needs to use it.

## Flow
A component can trigger an event. This event can be dispatched to a **reducer**, which updates the state in the central Redux **store**. From there the updated states are passed back to the connected components via the **actions**.

Make use of the `combineReducers` function to combine all the reducers in the store.

```
const rootReducer = combineReducers({
  news: newsReducer,
});
```

Create the store using `createStore(rootReducer, middleware)`.

Use the store as a `<Provider></Provider>` component, wrapping the App.

## Setting up reducers
Reducers are JS functions that take two parameters, state and actions.

```
const initialState = {
  articles: [],
  favorites: [],
}

export default function (state = initialState, action) {
  return state;
}
```

## Redux Actions
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

>You can make HTTP requests and fetch other type of data in the actions part of Redux, so you can use it in the state.

## Use Redux in components
Using `useSelector` you can select data from the state.
With `useDispatch` you can dispatch actions to the reducer.

**Dispatch an action:**
```
const dispatch = useDispatch();

useEffect(() => {
  dispatch(newsAction.fetchArticles());
}, [dispatch]);
```

**Use the data from the store:**

`const articles = useSelector(state => state.news.articles);`

---

# Building web server using Express and MongoDB
For the [Home Listing App][3.0] and the [Authentication System App][4.0] I've made use of custom made APIs. This is done in the backend using Express routing and MongoDB as a database. The APIs are used in the React Native Apps to display data. A nice lesson on combining a React Native frontend and NodeJS backend. This course is all about React Native, so I will not dive too deep into the NodeJS backend. I already have experience working with NodeJS and thus everything here is not new to me. However, in order to know what kind of data I'm working with, I've made a quick overview of the backend.

## Setup MongoDB with schema
The data that will be stored in the MongoDB database is setup using a schema. To create this, I make use of the NPM package **Mongoose**.

### Schema
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

## Routing
The routing is done using **Express**. You use a post request to post the data from a form into the database. This creates a new instance of the House schema with the formdata. This data can then be placed in a new database entry.

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

### Validation
Before placing the data in the database, the formdata needs to be validated.

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

# Combining React Native frontend with NodeJS Backend
I setup a React Native app for the [Home Listing App][3.0] using the React Native features I've learned in previous sections. Setting it up with a stack and tab navigator.

## Connect React Native to the server
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

## Add a form to post data to the server
To actually post the data to the NodeJS API, you need to make a form on the React Native frontend. This form is build using the **Formik** package.

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

## Add validation to form in react native
Validation is also handled on the frontend, before posting the data to the API. I use **Yup** to validate the React Native form and define a schema for the validation.

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

## Add post request to the server
Post the formdata to the server using fetch. This is handled in the action.

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

# Authentication system server side
This section of the course is all about learning to create an authentication system. Working with protected data and storing tokens.

## The setup
A client, in my case the React Native App, sends a request with authentication to the server. In response it gets a token. This token is stored on the client side and gets send to the server on subsequent requests whenever the client wants to make a request to the server. 

This is the authentication system I will build.

## Building the user register request
I start of on the server side, creating the user register request handler.

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

Because you're dealing with secure data like email and password, it's important to take good care of the data. One important thing to do is to hash the password, so you don't store the actual value in the database.

To hash the password, I use a package called **bcryptjs**.

### Hashing the password
```
const salt = await bcrypt.genSalt();
const hashPassword = await bcrypt.hash(req.body.password, salt);
```

Besides hashing the password, I'll also check if the email already exists, so there are no duplicates in the database.

### Check if email already exists
```
const userExists = await User.findOne({ email: req.body.email });
if (userExists) return res.status(400).send('Email already exists.');
```

## Building the login request
Next is the login request. Here I get the login credentials that the user entered in the login form. In this request I do the opposite of the register request. Check if the email is correct and exists in the database and use **bcryptjs** to validate the password.

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

## Setting up JSON web tokens
Last thing to do is to apply a token to the request header. By doing this I can check if the user is logged in on subsequent visits.

Using the **jsonwebtoken** package I can create the web token.

```
const token = jwt.sign({ _id: user._id, email: user.email }, secret);
res.header('auth-token', token).send({ message: 'Logged in successfully!', token });
```

### Protecting a route
To protect a route, I use a middleware to verify the token that I get back from the authentication request.

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

And now the server requests are done. Next up is the authentication on the client side.

---

# Authentication system client side
Now that the authentication is done on the server side and the requests are all handled, it's time to work on the client side. 

Here the user can register by entering an email, full name and password and can login using their new credentials.

<!-- Using the **secureTextEntry** property for TextInput, we can secure the password input. -->

## Register a user using React Native and NodeJS
When a user fills in a registration form with a full name, email and password and submits this, a redux action dispatches the user data to the NodeJS backend.

### Form submit handler
```
onSubmit={(values) => {
  dispatch(authAction.registerUser(values))
    .then(() => {
      navProps.navigation.navigate('Home');
    })
    .catch(err => console.log(err));
}}
```

Logging in uses the same approach, only without needing the full name.

### Backend register handler
```
try {
  const savedUser = await user.save();
  const token = generateToken(user);
  res.send({
    success: true,
    data: {
      id: savedUser._id,
      fullName: savedUser.fullName,
      email: savedUser.email,
    },
    token,
  });
} catch (err) {
  res.status(400).send({
    success: false,
    err,
  });
}
```

## Storing tokens using AsyncStorage
When a user has already registered, you can use the generated token to login the existing user. For this to work, you need to store the token in the React Native frontend. I do this using **Async Storage**.

In the login and register screens, when submitting the form and dispatching the data from the backend, I can store the token using Async Storage. Since this is an async function, you have to add the `async` keyword before the function that uses the resultData, like:

```
dispatch(authAction.loginUser(values))
  .then(async (result) => {
    if (result.success) {
      try {
        await AsyncStorage.setItem('token', result.token);
        navProps.navigation.navigate('Home');
      } catch (err) {
        console.log(err);
      }
    } else {
      Alert.alert(result.message);
    }
  })
  .catch(err => console.log(err));
```

In the homescreen I can then get the token back from the storage:
```
const loadProfile = async () => {
  const token = await AsyncStorage.getItem('token');
  if (!token) props.navigation.navigate('LoginScreen');
}

useEffect(() => {
  loadProfile();
});
```

### Decoding tokens
To decode the user tokens I use a package called **JWT Decode**.

`const decoded = jwtDecode(token);`

---

# Deploying React Native Apps
To deploy a React Native App through Expo to either iOS or Android, you'll have to follow these steps.

1. Update the `app.json` file with the right information, like **name**, **icon**, **platforms**, **splashscreen**, etc.
2. Publish the app using the command `expo publish`. This will publish the app to Expo. You need an Expo account for this.
3. Build the app:
    * **iOS:** Run the command `expo build:ios`
    * **Android:** Run the command `expo build:android`

## For iOS
If you want to build an app for iOS, you need a paid Developer account. To build, just run the command `expo build:ios`, and this should take you through the process.

## For Android
You can build an app for Android using the command `expo build:android`. You can specify if you want to build an APK (`expo build:android -t apk`) or an App Bundle file (`expo build:android -t app-bundle`). APKs are generally used for testing internally and externally. If you really want to publish your app in the Google Play Store, build an App Bundle.

For updating an app, you need to apply a keystore, which you can generate using Expo.

For more detailed documentation on deploying React Native Apps using Expo, click [here](https://docs.expo.io/distribution/building-standalone-apps/).