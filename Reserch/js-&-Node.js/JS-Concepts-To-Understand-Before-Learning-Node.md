
written by Musab Habeeb -- https://www.freecodecamp.org/news/javascript-concepts-to-know-before-learning-node-js/#:~:text=This%20opens%20up%20opportunities%20in,to%20understand%20before%20learning%20Node.

**Expressions

a unit or block of code that contains a value. there are five basic types of expressions: primary, arithmetic, string, logical, and left-hand side expressions

Primary
- consists of basic keywords in JS, a common example is the `this` keyword
- `this['item']`

Arithmetic
- these expressions take a number and use an arithmetic operator to preform a calculation
- `2 + 3 , 2* 3 , 2 ** 3`

string
- strings form expressions when concatenated
- `console.log('Hello' + 'World')`

logical
- expressions in which various values are compared 
- `10 > 2 , 2 < 10 , c === 2`

left-hand side
- expressions where values are assigned to a variable
- `obj = {}`

**data types
- eight data types - string, number, Boolean, Object, Null, Undefined, Symbol, and BigInt
- out of these eight the only unfamiliar ones are Symbol and BigInt
- Symbol: created by calling the `Symbol()` function, used to create a unique value
- BigInt: a special type of number that provides support for numbers with a length a normal number cant hold

**classes
- a template for creating objects containing data and functions that manipulate data
- functions used in classes are called methods
the syntax for declaring a class looks like this
```javascript
class TemplateClass {
	constructor() {}
	method() {}
	method() {}
}
```

here is an example where we make a class called visitor
```js
class Visitor {
    constructor(name) {
        this.name = name;
    }
    introduce() {
        console.log(`My name is ${this.name} and I am a visitor`)
    }
}
```
we can crate a new class from this class by using the new class syntax, the new class can access any method from its parent class
```js
let visitor = new Visitor("Jeff");

// visitor can call the introduce method in its parent class.
visitor.introduce();
```

**Variables

a named storage for JS data, created using the `var`, `let`, or `const` keywords. Variables made with `var` are function scoped, variables made with `let` are block scoped and variable made with `const` are also block scoped however their value cannot be changed at runtime (therefore they are constant)

**functions

a function is a block of code that can preform a specific task
```javascript
function exampleFunction() {
	return "does something";
}
```
a function take in inputs called arguments and outputs results. we can invoke the function by calling its name with closed brackets `exampleFunction();`

we can assign a function to a variable and call the variable when we want to invoke the function

**Arrow functions

arrow functions are concise and compact ways to write a function. They have some deliberate limitations to their usage
- they cannot be used as a method
- they cannot be used as a constructor
- arrow functions use yield within their own bodies

example syntax
```javascript
const example = () => {
	return "something"
}
```

**this Keyword

the `this` keyword in JS refers to an object that is executing a function or a code. it can be used:
- in an object method
- Alone
- in object method bindings

//note to self: might need to do more research on `this`

**Loops

loops are used when we want to execute a block of code multiple time under specific conditions and there are 5 types:
- for loops
- for … in loops
- for … of loops
- while loops
- do … while loops
`for` loops are used when we want to execute code a number of times, `for … in` loops are used to loop through the properties of an object, `for … of` loops are used to loop through the values of iterable object like arrays, strings, maps, etc, `while` loops execute a block of code while a certain condition is true, `do ... while` loops executes a block of code first with out any conditions then loops the code while a condition holds true.

example of `for`
```js
for (let i = 0; i < 5; i++) {
    return i;
}
```

example of `for ... in`
```js
for (let prop in obj) {
    return obj.prop;
}
```

example of `for ... of`
```js
let numArr = [2, 4, 6, 8]
for (let val of numArr) {
    return val ** 2
}
```

example of `while`
```js
while (i < 20) {
    return i;
    i++;
}
```

example of `do ... while`
```js
while (i < 20) {
    return i;
    i++;
}
```

**Scopes

the scope is the current context of execution and is where variables and expressions can be accessed. there is a hierarchical arrangement to JS scope making it possible for lower scopes to access higher scopes.
The scopes are as follows
- global
- module
- Function
- Block
global scope is the default for all code running in script mode while module scope is the default for all code running in module mode

function scope is created by functions and block scope is created by variables

example of function and block scope
```js
// function scope
function introduce(name) {
    let age = 19;
    console.log(`My name is ${name}`);
    console.log(`I am ${age} years old`);
}

let firstAge = 22

// block scope
if (firstAge === 22) {
    let secondAge = 33;
    console.log(`I am ${secondAge} years old`);
}
```

**Arrays

arrays can either be declared using square brackets `[]` or by using the array constructor `array()`

**accessing array elements

can be done in three ways:
- using their index
- using the arrays `length` property
- using a loop

to access an element by index we call the name of the array followed by the index number in square brackets `newArray[1]`

to access an element with the length property we use the property then subtract a number from it to get the index of the element we want to access
```js
// function scope
function introduce(name) {
    let age = 12;
    console.log(`My name is ${name}`);
    console.log(`I am ${age} years old`);
}

let firstAge = 13

// block scope
if (firstAge === 13) {
    let secondAge = 20;
    console.log(`I am ${secondAge} years old`);
}
```

to access an element using a loop, we can use a `for` loop or a `for ... of` loop
```js
 let newArray = ["Idris", "Daniel", "Joseph"];
  for (let i = 0; i < newArray.length; i++) {
      return newArray[i]
  }
  
  //this will loop through the array and return every element
```

**Important Array Methods

there are over 15 array methods built in to JavaScript however the ones most useful in Node.js are:
- `push()` and `pop()`
- `shift()` and `unshift()`
- `map()`
- `sort()`
- `forEach()`

the `push()` method is used to add an item to the end of an array while the `pop()` method is used to remove an item from the end of an array
```js
let arr = [1, 2, 3, 9]

arr.push(21);

console.log(arr)    // [1, 2, 3, 9, 21]

arr.pop()

console.log(arr)    // [1, 2, 3, 9]
```

the `unshift()` and `shift()` method are similar to `push()` and `pop()` however they add and remove items from the start of the array instead of the end, `unshift()` adds and `shift()` removes
```js
let arr = [1, 2, 3];

arr.unshift(0);

console.log(arr);    // [0, 1, 2, 3]

arr.shift();

connsole.log(arr);    // [1, 2, 3]
```

The `map()` method iterates through the elements of an array and calls a function on each element of the array. It returns a new array that contains the result of each function call:
```javascript
let fruits = ["Apple", "Grape", "Cashew"];

let mappedFruits = fruits.map(item => item + "s");
console.log(mappedFruits); // ["Apples", "Grapes", "Cashews"]
```

The `sort()` method sorts an array in place and returns the same array in a sorted form.

The default order of the `sort()` method is ascending order. Strings are sorted in alphabetical order:
```javascript
let numbers = [8, 7, 5];
let fruits = ["Apple", "Grape", "Cashew"];

let sortedNumbers = numbers.sort();
let sortedFruits = fruits.sort()

console.log(sortedNumbers);  // [5, 7, 8]
console.log(sortedFruits);  // ["Apple", "Cashew", "Grape"]
```

The `forEach()` method loops through the array and calls a function for every element of the array:
```javascript
let fruits = ["Apple", "Grape", "Cashew"];

fruits.forEach(fruit => console.log(fruit));
//  "Apple"
//  "Grape"
//  "Cashew"
```

**Template Literals

Template literals are enclosed in backticks, just like strings are enclosed in quotes. They allow you to store multiline strings and also interpolate strings with embedded expressions.

The example below shows a basic template literal:

```js
let basic = `I write codes`
```

You can write a template literal that stores multiline strings like this:

```js
let multiLine = `I write codes                     
        I debug codes`;
```

You can use the dollar sign and curly braces to embed expressions in template literals.

In the example below, the function `myName` is embedded in the display variable with a template literal:

```js
function myName(Musab, Habeeb) {        
    alert("Joshua Ross");    
}    

let display = `This displays my name ${myName()}`
```

**Strict mode

JavaScript is a sloppy language in the sense that it allows you to write code that is not allowed in other languages. Some of the code you write in JavaScript has errors but, JavaScript does not throw an error.

Strict mode does the following:

- It throws errors for JavaScript silent errors.
    
- It fixes mistakes that makes it difficult for JavaScript engines to perform optimizations.
    
- It prohibits some syntax likely to be defined in future versions of the ECMAScript.
    

Strict mode works in an entire script file and functions, but it does not work in block scopes.

To invoke script mode you will add the `"use strict";` syntax to the top of the code you want to apply it to. You can apply strict mode to a script like this:
```js
"use strict";

let name = "Joshua";

console.log(name);
```

Also, you can apply strict mode to a function like this:
```js
function sayHi(name) {
    "use strict";
    console.log(`Hi ${name}`);
}
```