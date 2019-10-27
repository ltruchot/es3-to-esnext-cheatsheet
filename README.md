# ES3 to ESNext Cheatsheet

## Controle structures

### Conditional

- classic: `if (cond) { ... } else if (cond) { ... } else { ...}`
- ternary: `var x = cond ? true : false;`
- error handling: `try {} catch (err) { ... }`
- operators: `||`, `&&`, `!`, `===`, `!==`, `<=`...

### Looping

- classic: `while (cond) { ... }`
- with counter: `for (let i = 0; i < 3; i++) { ... }`
- lists only: `const arr = [1, 2, 3]; for (let el of arr) { ... }`
- object only: `const obj = {a: 1, b: 2}; for (let key of obj) { ...}`

## Data structures

### Classics
- variables: `var x = 3;`, `let y = 4;` (es6), `const z = 5;` (es6)
- list/array: `const arr = [1, 2, 3];`
- object: `const obj = {a: 1, b: 2};`
- collections: `const coll = [{ nom: "toto", age: 12}, {nom: "titi", age: 21}]` AKA array of similar objects formatted

### Important Array methods
`const arr = [1, 2, 3];`
- `arr.push(4)` to add an item
- `arr.forEach(console.log)` to loop
- `arr.filter(a => a < 10)` to reject some values
- `arr.find(a => a === 2);` to find a value 
- `arr.map(a => a * 2)` to transform all values
- `arr.reduce((a,b) => a + b, 0));` to aggegate all values
### Types

Javascript is a loosely and dynamicaly typed languages: 

- 3 primitives: string ('' / "" / ``(es6)), boolean (true / false), number (42 / 78.98)
- 1 composed: Object (Objects, Arrays, Functions, Date, RegExp, etc.)
- 3 empty: undefined, null, NaN
- 6 falsy values : false, 0, "", NaN, undefined, null

### Further considerations
- *Primitives* are passed by *copy* (new values) / *Objects* are passed/shared by *reference* (pointing to the same memory space)
- scope of `var` is the current `function` and all descending blocks and functions. Don't use`var`with ES6 since it's lack of precision.
- scope of `const`/`let` is the current block and all descending blocks and functions.

## Functions

### Declare and execute
- 3 ways to declare it
```javascript
// named
function add (a, b) { 
    return a + b; 
}

// anonymous function, stored in a variable
const add = function () {
    return a + b;
}

// arrow function
const add = (a, b) => a + b;
```
- 1 way to run/execute it: `add(1, 2)`
- functions are *first class* in javascript: they can be passed as "values", as arguments, returned by other functions or stored in variables
- javascript is a functional language: prefer *pure unary functions* when possible, to produce a well made code

## window object

Browsers provides use a very useful object to control the window. It's named `window` and si the global scope as well
- `window.console === console // true`
- `alert("toto"); prompt("what is your name ?");`

An important part of the window object is `window.document` that represent the HTML DOM.
```javascript
const divToto = document.getElementById("toto"); 
const h1 = document.querySelector("h1");
h1.innerText = "Toto is a cool name."
divToto.innerHTML = "<p>That's true.</p>";
divToto.appendChild(document.createElement("ul"));
const ul0 = divToto.querySelectorAll("ul")[0];
document.body.addEventListener("click", (e) => e.targe.style.color = "blue");
```

An other important method is `fetch` that help us to do AJAX request

## Callbacks and Currying

- Since functions are first class, they can be passed as callbacks
```javascript
const callback = a => alert(a);
const func = (v, cb) => {
  console.log("Let's execute the function passed by argument");
  cb(v)
};
```
- Since functions can return functions, we can partially apply arguments, using currying
```javascript
const log = color => str => console.log(`%c ${str}`,`color:${color};`);
const logViolet = log("violet");
logViolet("toto");
logViolet("titi")
```
## ES6 to ESNext
Some feature of JavaScript are not fully implemented in all browsers. To use them, we need a *seed* or at least a tool like *babel*, *typescript* or *webpack* (sometimes we combine them) 

- `import` and `export`
```javascript
// toto.js
export const str = "toto";
```
```javascript
// titi.js
import { str } from "./toto";
console.log(str)
```
- `const list = ["horse", ...animals]` that spread animal array in `list`;
- `const { name } = person;` that extract the property name of the person object
- `class` that emulate OOP paradigm
- `async` and `await` to manage Promises

## Other important constructors / static objects 
- Math, JSON, Date, Promise, RegExp, Set, Map, XMLHttpRequest...

## Important dependencies

Most of the dependencies should be added with `npm` in a seed or any node project: `npm install jquery --save`

### Frameworks
- **Angular**: the big one to do everything, complex and written in TypeScript
- **React**: the light one, very powerful, functional oriented and very classic JS friendly
- **Vue**: between the two others

### Libraries
- **jquery**: control the DOM
- **axios**: AJAX requests
- **moment**: control the Dates
- **ramda**: Functional Programming helpers
- **lodash**: control Arrays and Objects
- **webpack**: create good seeds


