
by Krish Jaiswal -- https://www.freecodecamp.org/news/get-started-with-nodejs/?utm_source=chatgpt.com

## What is Node
- Environment to run JavaScript code
- uses googles V8 engine to convert JavaScript to machine code
- does NOT have access to browser objects like the DOM, window or Local Storage due to being outside of the browser
- Node is intended for server-side programming while the aforementioned browser features are intended for client-side programming
- Node provides lots of APIs and modules to preform operations such as file handling, creating server and more

## installing NodeJS
- can be downloaded from this link -- https://nodejs.org/
- its as simple as downloading the latest version for your operating system
- when installed you can run the command ``node-v`` and if its installed correctly the version number should appear in the terminal

## Global Variables
-  ``__dirname``: this variable stores the path to the current working directory
- ``__filename``: this variable stores the path to the current working file
- we can define our own global variables ``global.myVariable = 'hello world'``

## Modules in NodeJS
- a module is a specific block of code that can be used to preform a specific tasks or provide specific functionality 
- the main reason to use modules is it helps to organise code into smaller more manageable pieces. a module can be imported at any time and can be used flexibly which helps to create reusable code
- an example: if were working with function that handle a large volume of JSON data we can separate the JSON data and the code that works with it into separate files that can be imported whenever we need to use them

## writing our own modules

following the example of the document we will attempt to define a function called ``sayHello()`` in a file called ``hello.js`` it will accept a name as a parameter and print a message to the console as the output, we will then import the app.js file and use it there

This is the code in `hello.js` file:

```javascript
function sayHello(name){
    console.log(`Hello ${name}`);
}

module.exports = sayHello
```

This is the code in `app.js` file:

```javascript
const sayHello = require('./hello.js');

sayHello('John');
sayHello('Peter');
sayHello('Rohit');
```

The file `hello.js` can be called the `module` all modules have an object called ``exports`` which contains all the variables and functions you want to export from the module

The `app.js` file imports the `sayHello()` function from `hello.js` and stores it in the `sayHello` variable. To import something from a module, we use the `require()` method which accepts the path to the module. Now we can simply invoke the variable and pass a name as a parameter. Running the code in `app.js` file will produce the following output:

```javascript
Hello John
Hello Peter
Hello Rohit
```

**more on exporting modules

in this example we have a function that we want to export and use in our app

```javascript
function myFunction() {
	console.log('Hello world')
}

module.exports = myFunction;
```

we define the function then export it using `module.exports`, to then access the function we can declare a variable that requires that function and then we can use the function

```javascript
const myFunction = require('./myModule');

myFunction();
```
it is important to note that the parameter in `require` is the file path to the file that has our function.

problems can arise when attempting to export multiple functions with multiple exports
```javascript
// module.js

function myFunction() {
  console.log('Hello from myFunction!');
}

function myFunction2() {
  console.log('Hello from myFunction2!');
}

// First Export
module.exports = myFunction;

// Second Export
module.exports = myFunction2;
```
in this code the only module that gets exported is `myFunction2` as its overwriting the original export.

the problem can be solved if we assign `module.exports` to an object containing all the functions we want to export
```javascript
// myModule.js

function myFunction1() {
  console.log('Hello from myFunction1!');
}

function myFunction2() {
  console.log('Hello from myFunction2!');
}

module.exports = {
  foo: 'bar',
  myFunction1: myFunction1,
  myFunction2: myFunction2
};
```
this exports an object with three properties: foo, myFunction1, myFunction2

any module that requires this module now has access to all three properties
```javascript
// app.js

const myModule = require('./myModule');

console.log(myModule.foo); // logs 'bar'
myModule.myFunction1(); // logs 'Hello from myFunction1!'
myModule.myFunction2(); // logs 'Hello from myFunction2!'
```
it is common practice to group multiple exports into an object when working with multiple `module.exports`

## types of modules

Two types of modules - Built in Modules which are modules included in node by default and are able to be used without installation only needing to be imported to use, and External Modules which are created by other developers, requiring us to install them first before we can use them

some popular built in modules are OS, PATH, FS, HTTP

OS Module
provides methods/functions with which we can gain information about our operating system

PATH Module
the PATH module comes in handy when working with file directory paths providing various methods with which we can 
- join path segments together
- tell if a path is absolute or not
- get the last portion/segment of a path
- get the file extension from a path

FS Module
this module helps with file handling operations such as:
- Reading a file (Sync or async)
- writing to a file (sync or async)
- deleting a file
- reading the contents of a director
- renaming a file
- watching for changes in a file
- much more

## Event driven programming

event driven programming is a programming paradigm where program flow is largely determined by events or user actions rather than by the programs logic. in this type of programming the program listens for events and when they occur it executes some code/function that runs in response to that event, this event could be anything from a mouse click to a button click

in short we write code designed to listen and wait for events to occur and then run code that responds to that event

in order to implement event driven programming we need to remember 2 things:
- There is a function called `emit()` which causes an event to occur.  
    For example, `emit('myEvent')` emits/causes an event called `myEvent`.
    
- There is another function called `on()` which is used to listen for a particular event and when this event occurs, the `on()` method executes a listener function in response to it. For example, Consider this code: `on('myEvent', myFunction)`: Here we are listening for an event called `myEvent` and when this event takes place, we run the `myFunction` listener function in response to it.

We can access the `on()` and `emit()` functions by creating an instance of the `EventEmitter` class. The `EventEmitter` class can be imported from a built-in package called `events`.

**Points to Note:

There are 3 points you should note while working with events in Node.  
Each point in shown in action in the corresponding code snippets:

- There can be multiple `on()`'s for a single `emit()`:

Check out the following code, where multiple `on()` functions are listening for a single event to happen (`userJoined` event) and when this event is emitted in the last line of the code using the `emit()` function, you will see that the all the listener functions which were attached to the `on()` function get's executed:

```javascript
// Importing `events` module and creating an instance of EventEmitter class
const EventEmitter = require('events');
const myEmitter = new EventEmitter();

// Listener Function 1: sayHello
const sayHello = () => {
    console.log('Hello User');
}

// Listener Function 2: sayHi
const sayHi = () => {
    console.log('Hi User');
}

// Listener Function 3: greetNewYear
const greetNewYear = () => {
    console.log('Happy New Year!');
}

// Subscribing to `userJoined` event
myEmitter.on('userJoined', sayHello);
myEmitter.on('userJoined', sayHi);
myEmitter.on('userJoined', greetNewYear);

// Emiting the `userJoined` Event
myEmitter.emit('userJoined');
```

You can think of it this way: Each time the `userJoined` event is emitted, a notification is sent to all the `on()` functions listening for the event and then all of them will run their corresponding listener functions: `sayHello`, `sayHi`, `greetNewYear`.

Thus, when you run the code, you will see the following output printed in the console:

```text
Hello User
Hi User
Happy New Year!
```

- The `emit()` can also contain arguments which will be passed to the listener functions:

In the following code, We are using the `on()` method to subscribe to an event called `birthdayEvent` and when this event is emitted, we run the `greetBirthday()` function in response to it.

The extra parameters mentioned in the `emit()` function, gets passed as parameters to all the listener functions which will run in response to the `birthdayEvent`. Therefore `John` and `24` gets passed as parameters to the `greetBirthday()` function.

```javascript
const EventEmitter = require('events');
const myEvent = new EventEmitter();

// Listener function
const greetBirthday = (name, newAge) => {
    // name = John
    // newAge = 24
    console.log(`Happy Birthday ${name}. You are now {newAge}!`);
}

// Listening for the birthdayEvent
myEmitter.on('birthdayEvent', greetBirthday);

// Emitting the birthdayEvent with some extra parameters
myEmitter.emit('birthdayEvent', 'John', '24');
```

The following output will be seen printed in the console: `Happy Birthday John, You are now 24!`.

- The `emit()` function should always be defined after the `on()` function(s):

The entire process of communication between `on()` and `emit()` works like this: Before emitting any event, you need to make sure that all the listener functions have subscribed/registered to that event. Any function which is registered as a listener after the event has been emitted, will not be executed.

Check out the following code where this process is studied in detail:

```javascript
const EventEmitter = require('events');
const myEmitter = new EventEmitter();

// Listener Function 1 - sayHi
const sayHi = () => {
    console.log('Hi User');
}

// Listener Function 2 - sayHello
const sayHello = () => {
    console.log('Hello User');
}

// Registering sayHi function as listener
myEmitter.on('userJoined', sayHi);

// Emitting the event
myEmitter.emit('userJoined');

// Registering sayHello function as listener
myEmitter.on('userJoined', sayHello);
```

When the above code is executed, we see `Hi User` printed in the console but `Hello User` is not printed.

The reason behind this is: First we had registered the `sayHi` function as the listener using `myEmitter.on('userJoined', sayHi)`. Next we emit the `userJoined` event which results in execution of the `sayHi` function. In the next line we are registering the `sayHello` function as the listener, but it's already too late to do this because `userJoined` event has been emitted. This signifies the importance of defining all the `on()` functions before we emit the event using `emit()`.

You can also think of it this way: When you use `emit()` to trigger an event, NodeJS looks for any corresponding `on()` methods that have been defined in your code above the `emit()` method. If it finds any, it will execute them in order to handle the event.

## HTTP Module

this module helps to create web servers

the acronym stands for Hypertext Transfer Protocol, its used to transfer data over the internet which allows communication between clients and servers

the client sends a request to the server in the form of a URL with some additional information such as headers and query requirements

the server then processes the request and preforms the necessary operations sending the response back to the client.

## Components Of Request-Response

Both the Request (sent by client to the server) and the Response (sent by server to the client) comprises of 3 parts:

1. **The Status Line**: This is the first line of the request or response. It contains information about the message, such as the method used, URL, protocol version, and so on.

2. **The Header**: This is a collection of key-value pairs, separated by colon.  
    The headers include additional information about the message such as the content type, content length, caching information, and so on.

3. **The Body**: The Body contains the actual data being sent or received. In the case of requests, it might contain form data or query parameters. In the case of responses, it could be HTML, JSON, XML, or any other data format.

## What are HTTP Methods?

HTTP methods, also known as HTTP verbs, are actions that a Client can perform on a Server. The 4 HTTP Methods are:

- GET: Retrieves a resource from the server
- POST: Inserts a resource in the server
- PUT: Updates an existing resource in the server
- DELETE: Deletes a resource from the server

This might sound complicated, but let's try to understand these methods with the help of an example:

1. **GET:** Retrieves a resource from the server  
    When you enter [`http://www.google.com`](http://www.google.com/) in your web browser's address bar and press enter, your browser sends a HTTP GET request to the Google server asking for the HTML content of the Google homepage. That's then rendered and displayed by your browser.
2. **POST**: Inserts a resource in the server  
    Imagine you're filling out a registration form to create an account on Google. When you submit the form, your browser sends a POST request to Google's server with the data you typed in the form fields like: Username, Age, Birthdate, Address, Phone Number, Email, Gender and so on.

The server will then create a new user account in its database storing all the information sent to it using the POST Request. So a POST request is used to add/insert a resource in the server.

3. **PUT**: Updates an existing resource in the server  
    Now imagine you want to update your Google account's password. You would send a PUT request to the server with the new password. The server would then update your user account in its database with the new password.
4. **DELETE**: Deletes a resource from the server  
    Finally, imagine you want to delete your Google user account. You would send a DELETE request to the server indicating that you want your account to be deleted. The server would then delete your user account from its database.

Note that these are just examples. The actual requests and their purposes may vary.

## Creating a server

1. Import the http module `const http = require('http');`
2. the module provides us with the `http.createServer()` function which helps in creating the server. the function accepts a call-back function with 2 parameters - `req` which stores the incoming request object, and `res` which is the response from the server. this call-back function is executed every time someone hits the server

this is how we can create a server using `createServer()` function:
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    res.send('Hello World');
})
```

Note: `res.send()` is a function attached on the `res` object using which we can send some data back to the client. Here once we are done setting up the server, you will see a `Hello World` message in your web browser.

**Step 3:** Listening the server at some port using the `listen()` method.

The `listen()` function in Node.js `http` module is used to start a server that listens for incoming requests. It takes a port number as an argument and binds the server to that port number so that it can receive incoming requests on that port.

In the below code, we use the `listen()` function to start the server and bind it to port 5000. The second argument to the `listen()` function is a callback function that is executed when the server starts listening on the specified port. We are using this callback function just to display a success message in the console.

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    res.end('Hello World');
})

server.listen(5000, () => {
    console.log('Server listening at port 5000');
})
```