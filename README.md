# ES3 to ESNext Cheatsheet

## General

- **history**: invented in 1995 by Brendan Eich, for Netscape.
- **owner/maintainer**: ECMAScript
- **paradigms**: Functional > Procedural > OOP
- **strongly typed**: no
- **memory management**: callstack + garbage collector

## Control structures

### Conditional

- classic: `if (cond) { ... } else if (cond) { ... } else { ... }`
- ternary: `var x = cond ? true : false;`
- error handling: `try {} catch (err) { ... }`
- operators: `||`, `&&`, `!`, `===`, `!==`, `<=`...

### Looping

- basic: `while (cond) { ... }`
- with counter: `for (let i = 0; i < 3; i++) { ... }`
- lists only:

```javascript
const arr = [1, 2, 3];
for (let el of arr) { ... }
```

- objects only:

```javascript
const obj = {a: 1, b: 2};
for (let key in obj) { ...}
```

## Data structures

### Classics

- variables: `var x = 3;`, `let y = 4;` (es6), `const z = 5;` (es6)
- lists (including arrays/queues/stacks/matrix/collections): `const arr = [1, 2, 3];`
- object (including dictionnaries):

```javascript
const obj = {
  a: 1,
  b: "toto",
  c() {
    console.log(this.a, this.b);
  }
};
```

- collections, AKA array of similar objects formatted:

```javascript
const coll = [
  { nom: "toto", age: 12 },
  { nom: "titi", age: 21 }
];
```

### Important Array methods

```
const arr = [1, 2, 3];
```

- `arr.push(4)` to add an item (@see also `pop`, `unshift`, `shift`)
- `arr.forEach(console.log)` to loop, running the same function for each elements one by one
- `arr.find(a => a === 2);` return the first found (when the function return a truthy value)
- `arr.filter(a => a < 10)` to keep only some values (immutable\*)
- `arr.map(a => a * 2)` to transform all values (immutable\*)
- `arr.concat([5, 6, 7]);` to combine arrays (immutable\*)
- `arr.reduce((a,b) => a + b, 0));` to aggregate all values

* immutables methodes don't modify the original array: they just return a new one, so you can chain them

### Types

Javascript is a loosely and dynamically typed languages:

- 3 primitives: string (`''` / `""` / \`\` (es6)), boolean (`true` / `false`), number (`42` / `78.98`)
- 1 composed: Object (Objects, Arrays, Functions, Date, RegExp, etc.)
- 3 empty: `undefined`, `null`, `NaN`
- 6 falsy values : `false`, `0`, `""`, `NaN`, `undefined`, `null`

### Further considerations

- **Primitives** are passed by **copy** (new values)
- **Objects** are passed/shared by **reference** (pointing to the same memory space)
- scope of `var` is the current `function` and all descending blocks and functions. Don't use`var`with ES6 since it's lack of precision.
- scope of `const`/`let` is the current block and all descending blocks and functions.

## Functions

### Declare and execute

- 3 ways to declare it

```javascript
// named
function add(a, b) {
  return a + b;
}

// anonymous function, stored in a variable
const add = function() {
  return a + b;
};

// arrow function
const add = (a, b) => a + b;
```

- 1 way to run/execute it: `add(1, 2)`
- functions are _first class_ in javascript: they can be passed as "values", as arguments, returned by other functions or stored in variables
- javascript is mainly a functional language: prefer _pure unary functions_ when possible. ex:

## window object

Browsers provides us a very useful object to control the window. It's named `window` and it's the global scope as well

- `window.console === console // true`
- `alert("toto"); prompt("what is your name ?");`

An important part of the window object is `window.document` that represent the HTML DOM.

```javascript
const divToto = document.getElementById("toto");
const h1 = document.querySelector("h1");
h1.innerText = "Toto is a cool name.";
divToto.innerHTML = "<p>That's true.</p>";
divToto.appendChild(document.createElement("ul"));
const ul0 = divToto.querySelectorAll("ul")[0];
document.body.addEventListener("click", e => (e.targe.style.color = "blue"));
```

An other important method is `fetch`, that help us to do AJAX request and return a Promise (thenable object)

## Other important constructors / static objects

- **Math**, ex: `Math.random()`, `Math.max(1, 10, 100)`, `Math.round(4.95)`
- **JSON**, ex: `JSON.parse('{"result":true, "count":42}')`, `JSON.stringify({ x: 5, y: 6 })`
- **Date**, ex: `(new Date()).getFullYear()`, `Date.now()`
- **Promise**, ex: `new Promise((resolve) => resolve("toto"))`, `Promise.resolve().then(...)`, `Promise.all([get(...), post(...)]).then(...)`
- RegExp, Set, Map, XMLHttpRequest...

## Callbacks and Currying

- Since functions are first class, they can be passed as callbacks

```javascript
const display = a => alert(a);
const func = (callback, v) => {
  console.log("Let's execute the function passed by argument");
  callback(v);
};
func(display, "hello world!");
```

- Since functions can return functions, we can partially apply arguments, using currying

```javascript
const log = color => str => console.log(`%c ${str}`, `color:${color};`);
const logViolet = log("violet");
logViolet("toto");
logViolet("titi");
```

## ES6 to ESNext

Next features are not fully implemented in all browsers.

WARNING: To use them, we need tools like _babel_, _typescript_ or _webpack_ (we can combine them as a **seed**)

- `import` and `export`

```javascript
// toto.js
export const str = "toto";
```

```javascript
// titi.js
import { str } from "./toto";
console.log(str);
```

- `const list = ["horse", ...animals]` that spread animal array in `list`;
- `const { name } = person;` that extract the property name of the person object
- `class` that emulate OOP paradigm
- `async` and `await` to manage Promises

\*seed example: https://github.com/ltruchot/webpack-seed-js-sass

## Important dependencies

Most of the dependencies should be added with `NPM`: `npm install jquery --save`

### Frameworks

- **Angular**: the big one to do everything, complex and written in TypeScript
- **React**: the light one, very powerful, functional oriented and JS friendly
- **Vue**: between the two others

### Libraries

- **jquery**: control the DOM
- **axios**: AJAX requests
- **moment**: control the Dates
- **ramda**: Functional Programming helpers
- **lodash**: control Arrays and Objects
- **webpack**: create good seeds and project scaffolding
