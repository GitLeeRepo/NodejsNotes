# Overview

Notes on the ExpressJS framework for Node.js

# References

* [ExpressJS site](https://expressjs.com/)

## YouTube Videos	

* [ExpressJS Crash Course](https://www.youtube.com/watch?v=gnsO8-xJ8rs) YouTube video by Traversy Media
* [ExpressJS Crash Course](https://www.youtube.com/watch?v=gnsO8-xJ8rs) -- Brad Traversy	
* [Node.js and Express from Scratch](https://www.youtube.com/watch?v=k_0ZzvHbNBQ&list=PLillGF-RfqbYRpji8t4SxUkMxfowG4Kqp) -- Brad Traversy	

## My Other Notes	

* [NodejNotes](https://github.com/GitLeeRepo/NodejsNotes/blob/master/NodejNotes.md#overview)

## Code Repositories

* [ExpressJsMongoDemo01](https://github.com/GitLeeRepo/ExpressJsMongoDemo01)

# What is ExpressJS

* A minimalistic open source web framework for Node.js

* Most popular framework for Node.js

* Uses MVC concepts (Model, View, Controller)
  * Model -- Store the data
  * View -- Display the interface
  * Contoller -- direct traffic and load views

# Core concepts

* Middleware

* Routing 

* Template Engines - EJS, Handlebars, Jade/Pug

* Models

* Express Generators -- generates boiler plate apps

# Installation

* Node.js is required

* In the project folder

```
npm init
npm install express --save
```
This initializes the project folder with the **package.json** file, **installs Express** and with the **--save** parameter it adds an entry to the **dependencies** to **package.json**

Alternatively, you can **manually** add the following to **package.json** and run **`npm install` without parameters**.

```
"dependencies": {
  "express": "*",
  "body-parser": "*"
},
```
In this case it will install express in addition to the body-parser module.  This technique of adding them manually to the **package.json** first and then running **`npm install`** without parameters is useful when you have several packages to install.

```bash
## to install packages added manually in package.json
$ npm install
```

## Install nodemon

If you haven't already installed **nodemon** you will probably want to, that way you don't have to **restart the server** everytime you make a change.  You use this in placed of **`node appname`**, i.e., use **'nodemon appname`** instead.  This should be installed **globally**

```bash
npm install nodemon -g
```

# Simple example

## package.json

```json
{
  "name": "customer_app",
  "version": "1.0.0",
  "description": "Simple Customer Management App",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "dependencies": {
    "express": "*",
    "body-parser": "*"
  },
  "author": "Traeven",
  "license": "ISC"
}
```

Make sure you have **run npm install** to install the dependencies:

```bash
## to install packages added manually in package.json
$ npm install
```

## app.js

* Simple app.js example
* Requires express
* House a **get route handler** for sending a **response**.  It handles **requests** and **responses** (the **req** and **res** parameters.
* Note this example is using **pre-ES6** syntax, using **require** instead of **import** and using the **pre-ES6** **inline function** style (not **arrow functions**)

```JavaScript
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

* Variation of the above app.get() outputting JSON

```
app.get('/', function(req, res){
    res.json(people);
})
```
This takes the people JavaScript object and outputs it as JSON

# Middleware

* Middleware are functions that have access to the request and response streams and to the next middleware function
* Most modules in Express will have their own middleware that needs to be included
* You can create your own custom middleware functions
* The order of where the middleware is placed is important.  For example if you placed it after the app.listen it would not fire.
* Since middleware has access to the request and response you can whatever you want to modify the behavior of the app

## Custom middleware example

* Custom middleware function

```JavaScript
var logger = function(req, res, next) {
    console.log('Logging...');
    next();
}
app.use(logger);
```
Note this logger **event handler** will be triggered every time the app is called (page load and refreshes for example). The **next()** function passes control to the **next middleware function**.  The **app.use()** function call is necessary to **use this middleware**, which is why it is triggered every time that app runs.

## body-parser Middleware Example

```JavaScript
var express = require('express');
var bodyParser = require('body-parser');
var path = require('path');
var app = express();

// body-parser middleware
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({extended:false}));
```
This enables parsing of JSON and urlencoded content

## Middleware for Setting Static Folder

* Example

```
// static folder middleware for css files and any other static resources
// create this as a subdirectory of your project folder
app.use(express.static(path.join(__dirname, 'public')));
```

Tells Express the location of **static files (css, html, etc)** to be sent to the client (in this case a folder off the project root called **public**.  Note that if you put an **index.html** in here it would **override/take precedenc over** the **app.get res.send() output** displaying the **index.html** instead.  Any other non-default html file won't do that and the server output still takes precedence on the loading that path.

# Views and Template Engines

## EJS

* Install

```
npm install ejs --save
```

* Example code for template view

```
var express = require('express');
var path = require('path');
var app = express();
...

// set view engine
app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, 'views'));

/* ===== Route handlers ===== */

// render the views/index.ejs view
app.get('/', function(req, res){
    res.render('index');  
})

app.listen(3000, function() {
    console.log('Server started on port 3000');
})
```
In this case a simple HTML snippet was placed in the views/index.ejs file which is then output by the res.render() method.

The res.render() can be modified to use the template feature of the view engine (ejs in this case)

```
app.get('/', function(req, res){
    res.render('index', { title:"View Demo"});
})
```

If views/index.ejs contains the following:

```
<h1><%= title %></h1>
```
it will displays the "View Demo" text in the `<h1>` tag when rendered.

# Route handling

Route handling is used for responding to requests from specific HTTP methods (GET, POST, PUT, DELETE) and specific URIs

## Handling GET requests

* Example getting data from MongoDB and rendering it using the index view template

```JavaScript
app.get('/', function(req, res){
    db.users.find(function (err, docs) {
        res.render('index', 
        { 
            title:"Users",
            users: docs
        });
    });
})
```

## Handling POST requests

* Adding a user to a MongoDB database with post

```JavaScript
app.post('/', function(req, res) {
    var newUser = {
        first_name: req.body.first_name,
        last_name: req.body.last_name,
        email: req.body.email
    }
    db.users.insert(newUser, function(err, result){
        if (err) {
            console.log(err);
        }
    });          
})
```
Note this uses the same URI as the GET example.  This is ok because they are two different HTTP methods (GET & POST).  An alternative end-point could have been `app.post('/users/add', function(req, res)` as but one example.

## Handling DELETE requests

* Example of deleting a user from a MongoDB with the delete method

```JavaScript
app.delete('/users/delete/:id', function(req, res){
    db.users.remove({ _id: ObjectId(req.params.id)}, function(err, result){
        if (err){
            console.log(err);
        }
        else {
            res.statusCode = 200;
            console.log(result.n + ' user(s) deleted');
        }
    });
    console.log('delete: ' + req.params.id + ' - status: ' + res.statusCode);    
    res.redirect('/');
})
```
This example use an '`:id` selector as part of the URI.  This is a placeholder for the req.params.id that is represented in the index view with the data-id attribute in `<a href="#" class="deleteUser" data-id="<%=user._id%>">Delete</a>` which is assigned the MongoDB \_id value.

Note that this delete could have been represented by the same "/" end-point as the GET and POST since it is a different HTTP method, but in this case a different URI was used, with a redirect back to the original end-point.
