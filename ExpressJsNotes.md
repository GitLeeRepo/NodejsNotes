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

* Example custom middleware function

```javascript
var logger = function(req, res, next) {
    console.log('Logging...');
    next();
}

app.use(logger);
```
Note this logger event handler will be triggered every time the app is called (page load and refreshes for example)

