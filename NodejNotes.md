# Overview

Notes on Node.js server side JavaScript environment

# References

* [Main Site](https://nodejs.org/en/)
* [Node.js for Beginners](https://www.youtube.com/watch?v=U8XF6AFGqlc) YouTube video by Traversy Media.  Several of the notes here taken from this video.
* [Node.js and Express from Scratch](https://www.youtube.com/watch?v=k_0ZzvHbNBQ&list=PLillGF-RfqbYRpji8t4SxUkMxfowG4Kqp)

## My Other Notes

* [ExpressJsNotes](https://github.com/GitLeeRepo/NodejsNotes/blob/master/ExpressJsNotes.md#overview)
* [JavaScriptNotes](https://github.com/GitLeeRepo/JavaScriptNotes/blob/master/JavaScriptNotes.md#overview)
* [PHPNotes](https://github.com/GitLeeRepo/PHPNotes/blob/master/PHPNotes.md#overview)
* [PythonNotes](https://github.com/GitLeeRepo/PythonNotes/blob/master/PythonNotes.md#overview)
* [RestApiNotes](https://github.com/GitLeeRepo/RestApiNotes/blob/master/RestApiNotes.md#overview)
* [curlNotes](https://github.com/GitLeeRepo/RestApiNotes/blob/master/curlNotes.md#overview)
* [WordPressNotes](https://github.com/GitLeeRepo/WordPressNotes/blob/master/WordPressNotes.md#overview)

## Code examples

* [NodeJsSandbox](https://github.com/GitLeeRepo/NodeJsSandbox)

# Concepts and Terminology

## Node.js

* **Server-side JavaScript** environment
* **Event-driven**, **asynchronous** programming model
* Extensible through **modules**
* **NPM** - **Node Package Manager** - powerful and  easy to use command line package manager
* Reduces the complexity of server-side application development with Node itself and its many modules
* Useful for building **REST APIs**
* "The biggest difference between Node.js and PHP is that most functions in PHP block until completion (commands execute only after previous commands have completed), while functions in Node.js are designed to be **non-blocking** (commands execute in parallel, and use **callbacks** to signal completion or failure)." [Wikipedia](https://en.wikipedia.org/wiki/Node.js)
* Works on a **single thread** using **non-blocking I/O calls** which helps to make it very fast and efficient.
* Supports tens of thousands of **concurrent connections**
* Use **EventEmmitter** class to **bind events to listeners**

## NPM

* **Node.js Pakage Manager** used to install **Node.js packages** and **modules**
* Easy to specify and link **dependencies**
* **Modules** get installed in **node_modules** folder when installed **locally** with **`npm install <package>`**.
* **Modules** can also be installed **globally** with **`npm install -g <package.`**
* **npm init** is used to create an initial **package.json** file.  It will prompt you to enter several of the properties, and can easily be edited using a text editor for additional customization.
* **package.json** -- is initially created with **npm init** and is stored in the root folder of your project.  It contains the **name of the application**, various **dependecies** and **scripts** for your project, among several other properties.

# Installing and running on Windows

## Install

* Straightforward MSI install [Download](https://nodejs.org/en/)

# Install on Ubuntu

```
sudo apt-get install build-essential
sudo apt-get install nodejs npm
```

# Download Docker image and Run in a Docker Container

**DockerHub Official** versions: [hub.docker.com/_/node/](https://hub.docker.com/_/node/)

```bash
# to get the latest
$ docker pull node
# get a specific version (8.12 Debian Strech in this case)
$ docker pull node:8.12-stretch
```

**docker run** example:

This example maps a folder in the container to a folder on the host and uses the **start** script in the **package.json** file to run app (this assumes you already set up and app and created a **package.json** file).

```bash
docker container run --name node01 -d -p 3000:3000 -v $(pwd)/site:/usr/src/app node:8.12-stretch npm start
```

Example **Dockerfile** to create your own image:

```
FROM node:8.12-stretch
WORKDIR /usr/src/app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["npm", "start"]
```

# Run in Visual Studio

* Make sure Node.js was installed with Visual Studio Installer
* Create a new Node.js project with one of the provided templates.

# node Command

## Running node without parameters

If you run **node** without any parameters it brings up the **interactive shell** (referred to as **REPL** - Read Evaluate Print Loop) in which you can enter **JavaScript** statements interactively. 

```bash
$ node
> var x = 5
undefined
> x
5
> x + 3
8
> for (var i = 0; i < 5; i++) {
... console.log(i);
... }
0
1
2
3
4
.exit
```

Note the **undefined** above is not an error, it means you just don't have any output from that statement.  Also note that you can **exit the interactive shell** by either pressing **Ctrl+C twice** or by entering **.exit**

Also note that you can't run **browser commands** such as **document.getElementById("x")** since it is not running in the context of the **browser** and the **DOM**.

## Running the node command with a Script

Running the **node** command with a **script** for an **argument** runs that script.

```bash
$ node http_server.js
Server running at http://127.0.0.1:3000/
```

In addition to **server** side scripts, you can run any **JavaScript** you want to run from the **commandline** making it useful for running scripts that don't necessarily have to do with servers and web browsers.

## Simple Web App without External Modules

This web app does not have any **dependencies** defined in the **packages.json** file, you could in fact get by without a package.json, but a basic one is incuded here.  It does use **built-in** modules, such as the **http module** which is included with the **require('http')**

### Example Node.js File

```nodejs
const http = require('http');

const hostname = '127.0.0.1'
const port = '3000'

const server = http.createServer((req, res) => {
   res.statusCode = 200;
   res.setHeader('Content-type', 'text/plain');
   res.end('Hello World');
});

server.listen(port, hostname, () => {
   console.log('Server started on port: ' + port);
});
```

### Corresponding package.json File

```jason
{
  "name": "simple_server",
  "version": "1.0.0",
  "description": "Test",
  "main": "server01.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Traeven",
  "license": "ISC"
}
```

### Running the App

There are a couple of different ways to run this app

* Using the **node command**

```bash
$ node server01.js
Server started on port: 3000
```

* Using the **npm start**

This assumes you have defined a **start script** in the **package.json** file, which is actually running the same commands as above, i.e., **node server01.js**

```bash
$ npm start

> simple_server@1.0.0 start /home/tracy/source/nodejs/SimpleServer
> node server01.js

Server started on port: 3000
```

# NPM package manager

* Make sure it was part of the install (default)
* Used to install Node.js packages and modules
* Example - Installing a NPM package local to the project

```
npm install express
```

Installs the **express** module into the **node_modules** folder

* Example - Installing a NPM package globally

```
npm install -g express
```

Note that since the **JavaScript** for this app specified ** hostname = '127.0.0.1'** you will only be able to view it on a brower on the **localhost**.  If you want to view it remotely use an **IP address** that is accesible on your network.

To **terminate the server** press **Ctrl+C** on the console.

# Packages and Modules

## Popular Modules

* Express - Web development framework
* Connect - Extensible HTTP server framework.  Base line for Express
* Socket.io - Server side component for web sockets
* Pug / Jade - Template engine inspired by HAML.  Default template manager for Express
* Mongo/Mongoose - Wrappers to interact with MongoDB

## package.json

* Important JSON file that goes in the root of your module or project folder.  Configuration file used to tell how to install your module or app.
* "main" in this file is the **entry point** script for the project
* "dependencies" lists all the required modules (use an asterisks to specify the latest version of a module.
* You can use `npm init` to create this file for you.

Example:

```json
{
  "name": "express_sandbox",
  "version": "1.0.0",
  "description": "Sandbox app for learning ExpressJS",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "dependencies": {
    "body-parser": "*",
    "ejs": "^2.5.7",
    "express": "*",
    "express-validator": "^4.2.1",
    "mongojs": "^2.4.1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/GitLeeRepo/ExpressJsSandbox.git"
  },
  "author": "Traeven",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/GitLeeRepo/ExpressJsSandbox/issues"
  },
  "homepage": "https://github.com/GitLeeRepo/ExpressJsSandbox#readme"
}
```

## Live Server Module

* Useful for creating a live http server for a particular project directory.  This is useful for example when you want to test AJAX calls using a local file system file, since security restraints don't allow you to use the local file system
* To install

```
npm install -g live-server
```
Installs it globally

* To run, type this in your project directory

```
live-server
```
Will run the server on port 8080

* For more advanced configuration options refer to the [GitHub repository](https://github.com/tapio/live-server) for this module.
* Note that you can dynamically make changes to your project files without having to restart the server.

# Creating REST APIs

* Node is used extensively for creating REST APIs

TBD

# Examples

## Serve an HTML file using the fs (file system module)

* Create the project folder with a file named **server.js**
* Create the package.json file

```
npm init
```
Follow the prompts making sure the "main" entry point is **server.js**

* Enter code in **server.js**

```
const http = require('http');
const fs = require('fs');


const hostname = '127.0.0.1'
const port = '3000'

fs.readFile('index.html', (err, html) => {
if (err) {
   throw err;
}

const server = http.createServer((req, res) => {
   res.statusCode = 200;
   res.setHeader('Content-type', 'text/html');
   res.setHeader('Server', 'My Superduper Web Server');
   res.write(html);
   res.end();
});

server.listen(port, hostname, () => {
   console.log('Server started on port: ' + port);
});
});
```

* Run script

```
node server
```

This will run the server.  The server will remain running until you type `Ctrl+c`.  The console output `Server started on port: 3000` will display.  If you connect to the server in the browser with `localhost:3000` it will display the index.html web page read from the file system.

# NPM

## Various NPM commands

### Getting installed module versions

* Listing all packages

Select either local list or global list   
```
npm list 

npm list -g
```

* Getting a specific module version

```
npm list modulename
```
