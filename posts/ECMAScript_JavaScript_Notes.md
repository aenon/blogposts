# ECMAScript (JavaScript) Notes

Notes and examples about ECMAScript (JavaScript) based on the following articles

* [Learn ES2015](https://babeljs.io/learn-es2015/)
* [A Re-introduction to JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript) 
* [ES6 in Depth](https://hacks.mozilla.org/category/es6-in-depth/)
* [JS: ECMAScript 2015 Features](http://xahlee.info/js/js_ECMAScript_2015_features.html)
* [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS).

Check the compatibility table for your version of [node ](http://node.green/) and [browser](http://kangax.github.io/compat-table/es6/).

## Types
JavaScript Types 

*   [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)
*   [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)
*   [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)
*   [Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol) **(new in ES2015)**
*   [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
    *   [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
    *   [Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function)
    *   [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
    *   [RegExp](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
*   [null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)
*   [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)

```js
let a
typeof a // 'undefined'
typeof 42 // 'number'
typeof "hello" // 'string'
typeof true // 'boolean'
typeof {b: "c"} // 'object'
typeof ((n) => n + 1) // 'function'
typeof ['Apple', 'Banana'] // 'object'
typeof new Date() // 'object'
typeof /ab+c/i // 'object
typeof null // 'object'
typeof undefined // 'undefined'
typeof Symbol() // 'symbol'
```

## Numbers
```js
// double-precision 64-bit
// beware of 0.1 + 0.2 == 0.3 (false)
0.1 + 0.2 == 0.30000000000000004
// Number.EPSILON: tolerance value
if (!Number.EPSILON) {
    Number.EPSILON = Math.pow(2, -52)
}
// compare numbers
let areClose = (a, b) => {
    return Math.abs(a - b) < Number.EPSILON}
areClose(0.1 + 0.2, 0.3) // true

0o100 // 64 octal, don't use capital letter O
0100 // 64 (not allowed in strict mode)
0b1011 // 11 binary
0xf3 // 243 hexadecimal

// built-in object Math
Math.sin(3.5) 
// built-in function to convert to int
parseInt('123', 10)
// use "+" to convert string to number
+ '42' // 42
// NaN: Not a Number
NaN + 5 // NaN
isNaN(NaN) // true
1 / 0 // Infinity
-1 / 0 // -Infinity
isFinite(NaN) // false
isFinite(Infinity) // false

```

## Strings
Supports full **Unicode**.
```js
'你好'.length // 2
"\u{20BB7}" // '𠮷'
// new RegExp behaviour, opt-in ‘u’
"你好".match(/./u)[0].length // 1
'我在使用 StackEdit'.length // 14
'你好'.charAt(0) // '你'
'你好'[0] // '你'
'早上好'.replace('早上', '晚上') // '晚上好'
'我叫 Xilin'.toUpperCase() // '我叫 XILIN'
```


## Other Types
```js
// null, undefined and Boolean
isFinite(null) // true
isFinite(undefined) // false
// Boolean: "", NaN, null, undefined are false
Boolean(null) // false
Boolean(undefined) // false
Boolean('') // false
```

## Variables
`let`: block level variables. `let` is the new `var`.
`const`: const variables cannot be reassigned, but their properties can still be mutated.
`var`: traditionally the only var type. Not preferred.  

Rule:  **(need to reassign) ? use `const` : use `let`**.

The type of declared variable without value is `undefined`.

In the following case, the result can be different. 
```js
// using var i, the same counter object works for 
// all the 6 elements
for(var i = 1; i < 6; i++) {
  document.getElementById('my-element' + i)
    .addEventListener('click', function() { alert(i) })
}
```
```js
// each element has its own counter
for(let i = 1; i < 6; i++) {
  document.getElementById('my-element' + i)
    .addEventListener('click', function() { alert(i) })
}
```

Ref: [ES6+: var, let or const?](https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75)

## Operators
```js
// +-*/ just like others
// % is not modulo
12 % 5 // 2
-1 % 2 // -1
NaN % 2 // NaN
5.5 % 2 // 1.5
// ** exponential not supported in some browsers
// + will convert type
1 + '1' // 11
+'3' // 3
+true // 1
+false // 0
+null // 0
+((val) => val) // NaN

null + 1 // 1
1 + undefined // NaN
null == undefined // true
null === undefined // false
123 == '123' // true
1 == true // true
123 === '123' // false
1 === true // false
```

## Control structures
**Iterator + `for` .. `of`**
```js
// for loop
for (const value of array) {
    // do something with value
}
for (const property in object) {
    // do something with object property
}
// iterator and for loop
let fibonacci = {
    [Symbol.iterator]() {
        let pre = 0, cur = 1
        return {
            next() {
                [pre, cur] = [cur, pre + cur]
                return { done: false, value: cur }}}}}
for (const n of fibonacci) {
    if (n > 1000)
        break
    console.log(n)
}

// if else
if (name == 'puppies') {
    name += ' woof'
} else if (name == 'kittens') {
    name += ' meow'
} else {
    name += '!'
}
// while and do-while
while () {}
do {} while ()
// && and ||
var name = o && o.getName() // execute the second if the first succeeds
var name = cachedName || (cachedName = getName() // caching values
// ternary operator
var allowed = (age > 18) ? 'yes': 'no'
// switch: compares with === operator
switch (action) {
    case 'draw':
        drawIt()
        break
    case 'eat':
        eatIt()
        break
    default:
        doNothing()
}
```

## Objects
JavaScript objects can be compared with Python dictionaries. Properties can be accessed with dot or bracket notation.
```js
// two ways to create an obj
var obj = new Object()
var obj = {} // more common

var obj = {
  name: 'Carrot',
  for: 'Max', // 'for' is a reserved word, use '_for' instead.
  details: {
    color: 'orange',
    size: 12
  }
}
// access/assign properties using dot or bracket notation
obj.name // 'Carrot'
obj.details.color // 'orange'
obj['details']['size'] // 12
// bracket notation can set/get properties using reserved words
obj.for = 'Simon' // syntax error. "for" is a reserved word
obj['for'] = 'Simon' // works
// object prototype
function Person(name, age) {
    this.name = name
    this.age = age
}
var Harry = new Person('Harry', 24)
```

### Arrays
Objects with numerical properties (accessible only by bracket notation), and a special property called `length`.
```js
// also two ways to create
let arr = new Array() // create an array
let arr = [] // more common

let arr = [
    "hello world",
    42,
    true
]
arr[0]			// "hello world"
arr[1]			// 42
arr[2]			// true
arr.length		// 3
typeof arr		// "object"
// loop through an array
for (let i = 0; i < arr.length; i++) {
    // Do something with arr[i]
}
// also loop through
for (const item of arr) {
    // Do something with item
}
arr.push(item) // append
// other methods: toString(), toLocalString(), concat(...), join(sep), push(...), reverse(), shift(), slice(start[, end]), sort([compfn]), splice, unshift

// reduce
let numbers = [0, 1, 2, 3]
let result = numbers.reduce(
    (sum, num) => {return sum + num}
) // 6
```
[More on `reduce`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce).

### Functions
```js
// define a function
let foo = () => 42
let foo = () => {return 42} // same
// a function may have properties
foo.bar = "hello"
typeof foo // 'function'
typeof foo() // 'number'
typeof foo.bar // 'string'
// arguments array
let avg = (...args) => {
    let sum = 0
    for (let i = 0; i < args.length; i++) {
        sum += args[i]
    }
    return sum / args.length
}
avg(2, 3, 4, 5); // 3.5

// named IIFEs (Immediately Invoked Function Expressions)
// like a anonymous function with a name
// useful in recursions 
let averageNumber = ((...args) => {
    let sum = 0
    for (let i = 0; i < args.length; i++) {
        sum += args[i]
    }
    return sum / args.length
}) (2, 3, 4, 5)
console.log(averageNumber) // 3.5

// ES3025: convert arguments to a real Array
const args = Array.from(arguments) 
```
More on [Arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions).

### Custom objects
```js
// JS uses functions as classes
function makePerson(first, last) {
    return {
        first: first,
        last: last
    }
}
function personFullName(person) {
    return person.first + ' ' + person.last
}
s = makePerson('Simon', 'Sun') // 
s.first // 'Simon'
s.last // 'Sun'
personFullName(s) // 'Simon Sun'

// better: attach a function to an object
function makePerson(first, last) {
    return {
        first: first,
        last: last,
        fullName: function() {
            return this.first + ' ' + this.last
        }
    }
}
s = makePerson('Simon', 'Sun')
s.fullName() // 'Simon Sun'

// better: make use of "this"
// this is how classes are defined in JavaScript
function Person(first, last) {
    this.first = first
    this.last = last
    this.fullName = function() {
        return this.first + ' ' + this.last
    }
}
let s = new Person('Simon', 'Sun')
s.fullName // 'Simon Sun'

// better: shared functions
function personFullName() {
    return this.first + ' ' + this.last
}
function Person(first, last) {
    this.first = first
    this.last = last
    this.fullName = personFullName
}
s = new Person('Simon', 'Sun')
fn = s.fullName // now we are able to do this
fn() // 'Simon Sun'

// even better: use '.prototype'
function Person(first, last) {
    this.first = first
    this.last = last
}
Person.prototype.fullName = function () {
    return this.first + ' ' + this.last
}
s = new Person('Simon', 'Sun')
s.fullName() // 'Simon Sun'
```

### Inner functions
Scope of parent function is accessible
```js
function parentFunc() {
    // accessible to nestedFunc
    let a = 1 
    function nestedFunc() {
        // parentFunc can't use this
        let b = 4 
        return a + b
    }
    return nestedFunc() // 5
}
```

### Closures
```js
let makeAdder = (a) => {
    return (b) => {return a + b}
}
let x = makeAdder(5)
let y = makeAdder(20)
x(6) // 11
y(7) // 27
```

```js
let sayHello = (name) => {
    let text = 'Hello ' + name
    let say = () => console.log(text)
    return say
}
let say2Lucky = sayHello('Lucky')
say2Lucky() // Hello Lucky
```
> Written with [StackEdit](https://stackedit.io/).
