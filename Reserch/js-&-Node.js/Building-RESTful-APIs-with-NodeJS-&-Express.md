
presented by Emmanuel Henri on LinkedIn Learning -- https://www.linkedin.com/learning/building-restful-apis-with-node-js-and-express-16069959/introduction-to-apis-and-the-libraries?autoSkip=true&resume=false&u=56746241

## 1. Setting up
this tutorial will use a few standard library's such as:
- Node.js
- Express
- MongoDB
- Babel

we installed mongo dB and initialized our project adding on a bunch of babel dependencies, express, nodemon, and body-parser

we also created a file `.babelrc` to compile our code with the latest version of JavaScript into readable code for our server

## 2. initial server build

### Restful API Refresher
- a way to transact with a backend using HTTP protocols
- Using GET, POST, PUT and DELETE calls to the back end
- Interacting with endpoints created on the back end
- GET: gets the data
- POST: adds new data
- PUT: updates data
- DELETE: deletes data

### Initial server setup

the first step in creating our server is use nodemon to do `NPM start` and start our server automatically and restart it whenever we change our code

to do this we go into our `package.json` file and in the `scripts` object we change our `test:`  and replace it with the following 
```json
"start": "nodemon ./index.js --exec babel-node"
```

once we do this we need to create our `index.js file`

we then import express and create our app variable along with our port
```javascript
import express from 'express';

const app = express();
const PORT = 3000
```

we can then make our first endpoint using `app.get` in this first example we create our first endpoint and send back to the server what port we are running on using a template string (a template string being a string that has the capability of having a variable passed into it and then read)

```javascript
app.get('/', (req, res) =>
    res.send(`Node and express server is running on poert ${PORT}`)
);
```

we can then add a listener that takes in our port variable and print to the browser console
```javascript
app.listen(PORT, () => 
    console.log(`your server is running on port ${PORT}`)
);
```

testing this by running our server with `npm start` shows us the log in our console and when we open `localhost:3000` in our browser we are greeted with our endpoint message

**Initial server files and folders

before we start adding endpoints its a good idea to map out our file and folder structure first

this tutorial starts with a source folder `src` then adding a `controllers` folder, `models` folder, and a `routes` folder, all within the source folder

- the controllers are function that allow us to get information into the endpoints and forward it to whoever is calling it
- the routes are basically the endpoints
- the models are the schema models for our database

we then create a file in each of our folders

**Basic routing endpoints

any application needs routes in order to call a URL

we can call a route to go to a specific page in a webpage but we can also call routes to define endpoints in our application. we will be using routes for our endpoints

the first thing we need to do is edit our index.js file to be able to load the file were going to create
```javascript
import routes from './src/routes/projectRoutes';
```

we can then run our routes inside the app
```javascript
routes(app);
```

then inside of our routes file we can add a function called `routes` that takes in our app. we can then add our first route called `contact` which will give our app our get, put, update, and delete commands
```javascript
const routes = (app) => {
    app.routes('/contact')
    .get

    .post

    app.route('/contact/:contactID')
    .put

    .delete
}
```

we can then create our routes to these commands

for our get command we can give it its request response functionality
```javascript
.get((req, res) =>
    res.send('GET request sucess')
)
```

we can do the same thing with the post request, as well as the the Put and DELETE routes
```javascript
.POST((req, res) =>
    res.send('POST request sucess')
)
```

then testing this in postman by connecting it to our local host URL `localhost:3000/contact` we can verify if each of these commands are working, which after testing they are.

**basics of middleware and uses

middleware is any function that has access to the request and response objects in our app. It can make changes to the objects, end them, call the next function in the stack etc

an example of middleware can be a console log stating who our request is from in our GET function
```javascript
 .get((req, res, next) =>{
        //middleware
        console.log(`request from: ${req.originalUrl}`)
        console.log(`Request Type: ${req.method}`)
        next();
    }, (req, res, next) => {
        res.send('GET request sucess')
    }
    )
```
its important to note here that we need the `next()` function to continue with our response after our middleware has ran, the continued response takes place inside the `next()` function. we also have to pass in `next` into our `.get` as a parameter

the response in the console when running the get request looks like this
```
request from: /contact
Request Type: GET
```

## 3. database setup

this course uses mongoDB as a database for this API, however currently the project I am trying to build does not require a separate database and can work with false in-memory data. as such I have chosen to skip this section of the course as its not currently relevant

## 4. CRUD Operations

**Create POST endpoint
