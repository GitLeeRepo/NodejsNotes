# Overview

Notes on the ExpressJS framework for Node.js

# References

* [ExpressJS site](https://expressjs.com/)

* [ExpressJS Crash Course](https://www.youtube.com/watch?v=gnsO8-xJ8rs) YouTube video by Traversy Media

# What is ExpressJS

* A minimalistic open source web framework for Node.js

* Most popular framework for Node.js

* Uses MVC concepts (Model, View, Controller)

# Core concepts

* Middleware

* Routing 

* Template Engines - EJS, Handlebars, Jade

* Models

* Express Generators

# Installation

* Node.js is required

*  In the project folder

```
npm init

npm install express --save
```
This initializes the project folder with the package.json file, installs ExpressJS and adds its dependencies to package.json

Alternatively, you can manually add the following to package.json and run `npm install` without parameters

```
  "dependencies": {
    "express": "*",
    "body-parser": "*"
  },
```
In this case it will install express in addition to the body-parser module.  This technique of adding them manually to the package.json first and then running `npm install` is useful when you have several packages to install.

# Simple example

* Simple app.js example

```javascript
var express = require('express');

var app = express();

// Route handler
// handling GET requests to document root, 
// you would use post for POST requests
app.get('/', function(req, res){
    res.send('Hello World');
})

app.listen(3000, function() {
    console.log('Server started on port 3000');
})
```
Assuming app name is app.js run `node app` and then from a browser go to localhost:3000 to see "Hello World" displayed

# Middleware

* Middleware are functions that have access to the request and response streams and to the next middleware function

* Most modules in Express will have their own middleware that needs to be included

* You can create your own custom middleware functions

* The order of where the middleware is placed is important.  For example if you placed it after the app.listen it would not fire.

* Since middleware has access to the request and response you can whatever you want to modify the behavior of the app

## Custom middleware example

* Custom middleware function

```javascript
var logger = function(req, res, next) {
    console.log('Logging...');
    next();
}
app.use(logger);
```
Note this logger event handler will be triggered every time the app is called (page load and refreshes for example)

## body-parser middleware example

```javascript
var express = require('express');
var bodyParser = require('body-parser');
var path = require('path');
var app = express();

// body-parser middleware
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({extended:false}));
```
This enables parsing of JSON and urlencoded content

## Middleware for setting static folder

* Example

```
// static folder middleware
app.use(express.static(path.join(__dirname, 'client')));
```
Tells Express the location of static files (css, html, etc) to be sent to the client (in this case a folder off the project root called client.  Note that if you put an index.html in here it would take precedence and display instead of any server side output.  Any other non-default html file won't do that and the server output still takes precedence on the loading that path.
