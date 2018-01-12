# React

## JSX

* include `/` in self-closing tabs.
* exactly one outermost element per JSX expression.
* className
* evaluate js in jsx with `{}`
```babel
function makeDoggy(e) {e.target.setAttribute('src', 'IMGURL');}
```

* cannot use `if`
* using ternary operator is ok
* using && 
```babel
{Math.random() < 0.5 && <li>that item</li>}
```

* key: JSX attribute
```babel
<li key={'person_' + i}>{person}</li>
```

* user-defined components must be capitalized

## React without JSX

```babel
// React with JSX

const h1 = <h1>Hello world</h1>;
```

```javascript
// React without JSX

// React.createElement(
//   type,
//   [props],
//   [...children]
// )

const h1 = React.createElement(
  "h1",
  null,
  "Hello, world"
);
```

## React Component
[Reference](https://reactjs.org/docs/react-component.html)
```babel
class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}

ReactDOM.render(
  <MyComponentClass />, 
  document.getElementById('app')
);
```

```babel
class Button extends React.Component {
  scream() {
    alert('AAAAAAAAHHH!!!!!');
  }

  render() {
    return <button onClick = {this.scream}>AAAAAH!</button>;
  }
}
```
## import and export 

```babel
import {Navbar} from './NavBar';
```
```babel
export class NavBar extends React.Component {
  render () {

  }
}
```

immutability with `slice()`
```babel
const squares = this.state.squares.slice();
squares[i] = 'X';
this.setState({squares: squares});
```

## this.props

pass variables and functions

```babel
class Greeting extends React.Component {
  render() {
    return (
      <h1>Hi there, {this.props.name}!</h1>
    );
  }
}

ReactDOM.render(
  <Greeting name='Groberta' />, 
  document.getElementById('app')
);
```

this.props.children: content between opening and closing JSX tags

```babel
<MyComponent>Childrenhere</MyComponent>
```

## this.state

component maintains its own state

```babel
constructor(props) { // sets the initial state
  super(props); // important
  this.state = {mood: 'decent'};
}
```

changes state by `this.setState()`

```babel
this.setState({
  hungry: true
})
```

Use `this` in a method:
```babel
this.methodName = this.methodName.bind(this) 
```

## Pass a Component's State

```babel
class Parent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {name: 'Lucky'}; // the state of Parent
  }
  render() {
    return <Child name={this.state.name} />;
  }
}
class Child extends React.Component {
  render() {
    return <h1>Hello, my name is {this.props.name}</h1>; // the prop of Child
  }
}
```

`props` are used to store information that can only be changed by other components
`state` is used to store information that can be changed by the component itself.

## Update parent state

Parent: pass handle function to Child
`<Child name={this.state.name} onChange={this.changeName} />`
Child: define a handleChange function that can be passed an event object
```babel
  handleChange(e) {
    const name = e.target.value; // important
    this.props.onChange(name);
  }
  render() {
    <button onClick={this.handleChange}> </button>
  }
```

## Styles

```babel
const styleMe = <h1 style={{ background: 'lightblue', color: 'darkred' }}>Please style me! I am so bland!</h1>;
```

Inject css-like objects into a `JSX` element.

Style names are written in camelCase. 

`"20px"` can be written as a number `20`.

```babel
const styles = {
  marginTop: 20,
  backgroundColor: "green"
};
```

### Styles in a JavaScript file
```babel
// style.js
export const styles = {
  marginTop: 20,
  backgroundColor: "green"
};
```

and used in other files
```babel
// app.js
import {styles} from './style.js'
```

## Container / Presentational Components

Seperate business logic from presentational logic.

* Presentational components: renders JSX. Only contains "render()" function.
* Container components: business logic. imports the presentational components

A presentational component is always rendered by a container Component

### Functional Presentational Component

more concise

```babel
// A component class
export class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}

// A stateless functional component
export const MyComponentClass = () => {
  return <h1>Hello world</h1>;
}
```

With props
```babel
// Normal way to display a prop using a variable:
export class MyComponentClass extends React.component {
  render() {
    let title = this.props.title;
    return <h1>{title}</h1>;
  }
}

// Stateless functional component way to display a prop using a variable:
export const MyComponentClass = (props) => {
  let title = props.title;
  return <h1>{title}</h1>;
}
```

## PropsTypes

```babel
BestSeller.propTypes = {
  title: React.PropTypes.string.isRequired,
  weeksOnList: React.PropTypes.number.isRequired
}
```

```babel
// same for stateless functional component
GuineaPigs.propTypes = {
  src: React.PropTypes.string.isRequired
}
```

## React Forms

```
<input 
  type="text" 
  value={this.state.userInput}
  onChange={this.handleUserInput} 
/>
```

## Controlled / Uncontrolled Components

A uncontrolled component maintains its own state.

Prefer controlled components for Redux

## Mounting Lifecycle Methods

These methods are called in order:

* componentWillMount
* render
* componentDidMount

```babel
componentWillMount() { // this runs only the first time the component is mounted
  alert('AND NOW, FOR THE FIRST TIME EVER...  FLASHY!!!!');
}
```

`componentDidMount` can be used to place AJAX calls or use `setTimeout` or `setInterval`.

## Updating Lifecycle Methods

* componentWillReceiveProps: `nextProps`
* shouldComponentUpdate: component will not update if `shouldComponentUpdate` returns false
* componentWillUpdate: `nextProps` and `nextState`
* render
* componentDidUpdate: `prevProps` and `prevState`

## Unmounting Lifecycle Methods

`componentWillUnmount`: 

`Unmount`: not `umount`.


# Getting started with Redux

Store -> Provider -> Containers -> Components -> User -> Actions -> Reducers -> Store...

## Principles
* Represent the **whole state** of the application as a **single JavaScript object**: the state (state tree) (__store__). 

* State is redundant. All changes must be done with __actions__ - JS objects describing what is changed. Use strings as action type.

* __Reducer__: pure functions - no side effect. Reducer calculates new state with old state and the action.

## Writing a counter

Test the function with expect

```js
const counter = (state = 0 , action) => {
  return state
}

expect (
  counter(0, { type: 'INCREMENT' })
).toEqual(1)

console.log('Test passed!')

```

if the reducer receive undefined state argument, returns initial state of application.

## App structure

```js
// reducer
const counter = (state = 0, action) => {}

// component
const Counter = ({value, onIncrement, onDecrement}) => ()

// store: getState, dispatch and subscribe
const { createStore } = Redux
const store = createStore(counter)

const render = () => {} // getState and dispatch
render() // initial state
store.subscribe(render) // subscribe
```


## Write our own `createStore`

```js
const createStore = (reducer) => {
  let state
  let listeners = []
  // 3 methods: getState, dispatch and subscribe
  const getState = () => state
  const dispatch = (action) => {
    state = reducer(state, action)
    listers.forEach(listener => listener())
  }
  const subscribe = (listener) => {
    listeners.push(listener)
    return () => {
      listeners = listeners.filter(l => l !== listener)
    }
  }
  dispatch({}) // get the initial value
  // returns a Redux store
  return { getState, dispatch, subscribe} 
}

```


## render with ReactDOM
```babel
const render = () => {
  ReactDOM.render(
    <Counter 
      value={store.getState()}
      onIncrement = {() => 
        store.dispatch({
          type: 'INCREMENT'
        })
      }
      onDecrement = {() =>
        store.dispatch({
          type: 'DECREMENT'
        })
      }
    />,
    document.getElementById('root')
  )
}

```

## expect and deep-freeze

