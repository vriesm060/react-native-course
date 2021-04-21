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