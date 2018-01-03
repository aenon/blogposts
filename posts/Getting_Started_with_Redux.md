# Getting started with Redux

Redux 

Store -> Provider -> Containers -> Components -> User -> Actions -> Reducers -> Store...

## Principles
* Represent the **whole state** of the application as a **single JavaScript object**: the state (state tree) (__store__). 

* State is redundant. All changes must be done with __actions__ - JS objects describing what is changed. Use strings as action type.

* __Reducer__: pure functions - no side effect. Reducer calculates new state with old state and the action.

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

## JSX

* include `/` in self-closing tabs.
* exactly one outermost element per JSX expression.
* className
* evaluate js in jsx with `{}`
```jsx
function makeDoggy(e) {e.target.setAttribute('src', 'IMGURL');}
```

* cannot use `if`
* user-defined componengs must be capitalized

