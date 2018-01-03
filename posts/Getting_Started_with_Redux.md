# Getting started with Redux

Redux 

Store -> Provider -> Containers -> Components -> User -> Actions -> Reducers -> Store...

## Principles
* Represent the **whole state** of the application as a **single JavaScript object**: the state (state tree) (store). 

* State is redundant. All changes must be done with actions - JS objects describing what is changed. Use strings as action type.

* Reducer: pure functions - no side effect. Reducer calculates new state with old state and the action.

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

## localStorage

