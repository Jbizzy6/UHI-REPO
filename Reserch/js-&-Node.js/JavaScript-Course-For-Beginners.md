
notes written from a video course by Programming with Mosh on YouTube -- https://www.youtube.com/watch?v=W6NZfCO5SIk


what is JavaScript
- one of the most popular and Widley used languages in the world, currently growing faster than any other language
- you can do front end, back end, and full stack applications with JavaScript
- initially could only be used on the browser as a front end language however in the modern day it can be used for applications such as games, web / mobile apps, real time networking apps, etc

where does JS code run
- initially only ran in browsers with a JavaScript Engine
- Node came along and allowed JavaScript code to run outside of a browser

JavaScript in browsers
- script element required for JavaScript code
- it is best practise to put JavaScript code at the end of the body element
- all statements in JavaScript need to be terminates with a semi-colon

Separation of concerns
- we want to separate HTML and JavaScript in our code
- HTML should be all about content while JavaScript is all about behaviour
- while we are only working with one HTML and one JS file for now we can simply get and display our JS code with the script tag e.g. ``<csript src=index.js></script>``

Variables
- ``let`` keyword used to define variables, e.g. `let name`
- variable naming rules: cannot be a reserved keyword, should be meaningful, names cannot start with a number, cannot contain a space or hyphen, names are case sensitive
- you can declare multiple variables on the same line by using `,` however best practise states its better to declare each variable on a separate line

Constants
- there are situations where we do not want the value of a variable to change as it could lead to bugs or problems, in these scenarios we use constants
- the value of a constant cannot change
- we declare a constant with `const`
- the best practice is that if we do not need to re-assign our variables value we use `const` otherwise we use `let`

primitive types
- two category's of types - Primitive / Value types, and Reference Types
- the primitive types are as follows: String, Number, Boolean, undefined, null
-  here is an example of a string / string literal `let name = 'josh';`
- here is an example of a number / number literal `let age = '30';`
- here is an example of a Boolean / Boolean literal `let isAllowed = true;`
- undefined is a value that appears when a variable is not initialized however we can manually set variables to be undefined e.g. `let name = undefined;` 
- null is used when we explicitly want to clear the value of a variable e.g. `let secection = null;`

dynamic Typing
- unlike other languages JavaScript is a Dynamic Language
- there are two types of languages - Static and Dynamic
- in static languages when we declare a variable its type is set and cannot be changed in the future however in dynamic languages the type of a variable can change in runtime
- we can use the `typeof` operator to check the type of a variable
- the type of a variable will be determined at runtime based on the value assigned to them
- unlike in other languages the number type in JS handles both integers and floating point numbers 

Objects
- Objects are a reference type along with Arrays, and Functions
- an object can be thought of as a collection of variables and features that define that object, if we use the example of a person we have a list of attributes such as name, age, height etc. in JS we can bundle those individual variables together into an object that we can then reference in our code
- this serves to make our code cleaner
- we can declare an object similar to other variables, both let and const can be used
- e.g. `let person = {};` the curly braces are called the object literal and its what declares our object
- between the curly braces we add one or more key value pairs that are the properties of the object in our example we want our person object to have two properties - name and age
example
````javascript
let person = {
	name: 'Josh',
	age: 19
};
````
- there are two ways to work with the properties in our object, the first way is called the dot notation, we do this by calling the name of our object, followed by a dot, and then the name of the property we want to interact with e.g. `person.name = 'Cass';` would change our name property to Cass instead of Josh
- the other way is called bracket notation in which we use square brackets, then pass in the name of the target property between single quotes, and then we can interact with the property e.g. `person['name'] = 'Cass';`
- dot notation is more concise and shorter and therefore should be the default approach however the bracket notation is used to deal with more complex functions and should be used then

arrays
- in our projects we may deal with a list of objects and in those situations we use an array to store the list
- to declare an array we use square brackets which are referred to as an array literal e.g. `let listOfObjects = [];`
- each element in an array is given an index which determines its location in the array starting at zero and increasing with each element
- the length of our array and the objects inside are once again dynamic and can change at runtime
- arrays are also objects and as such we can access its properties with the dot notation
- the main takeaway for now is that an array is a data structure we use to represent a list of items

functions
- a fundamental building block in JavaScript
- a function is a set of statements that we use to preform a task or calculation
- declared with the `function` keyword then the name followed by curly brackets which can be left empty but are required for the syntax, and then curly braces which enclose our functions code, e.g. `function helloWorld() {}`
- all the code inside the curly braces is referred to as the body of the function
- we can call the function by simply typing the name of the function wit its brackets and a semicolon to declare it as a statement e.g. `helloWorld();`
- functions can take inputs that can change how the function behaves
- we can add a variable in-between the functions brackets known as a parameter and its a variable that is only meaningful inside of the function
- we can have multiple parameters in a function

this marks the end of the YouTube course

if and if else statements
(taught by the same youtuber but on a different video -- https://www.youtube.com/watch?v=IsG4Xd6LlsM)
- two types of conditional statements - if..else, and switch...case, this video covers if...else

syntax
```javascript
if (condition) {
	statement
}
else if (secondCondition) {
	statement
}
```
- there is no limit to the amount of conditions we can have in a if statement
- we can use `else` instead of `if else` to return a statement should none of our if statements apply

loops (same youtuber - https://www.youtube.com/watch?v=s9wW2PpJsmQ)
- there are different types of loops, those being for, while, do...while, for...in, and for...of. they all do the same thing but there's a difference in how they start and end

for loops
- written simply as `for ()` and requires three statements, the first statement is our initial expression and its where we declare or initialize a variable, typically the variable we use is called `i` and is short for index, its common convention to use it in for loops and we call it the loop variable, we also typically set it to 0. then we have our condition and its where we want to compare the value of `i` with something else, the loop will run as long as the condition evaluates to true we could use this to set how long we want our loop to run 
- example: `for (let i = 0; i < 5)` this would run the loop five times because once `i` is no longer less than 5 the condition is no longer met and the loop must stop
- the third part of the loop is called the increment expression, for example if we used `i++` as our increment expression it would increment `i` by one and following the condition the loop would do this five times, the completed loop would look like this `for (let i = 0; i < 5; i++)`
- we then follow the loop with our statement, using a code block if we have multiple statements

a completed for loop with a statement to print hello world to the console 5 times would look like this
```javascript
for (let i = 0; i < 5; i++) {
	console.log('hello world');
}
```

