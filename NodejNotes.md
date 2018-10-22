# Overview

Notes on Node.js server side JavaScript environment

Node.js is/has/does:

* Server-side JavaScript environment
* Event-driven, asynchronous programming model
* Extensible through modules
* NPM - Node Package Manager - powerful and  easy to use command line package manager
* Reduces the complexity of server-side application development with Node itself and its many modules
* Useful for building REST APIs
* "The biggest difference between Node.js and PHP is that most functions in PHP block until completion (commands execute only after previous commands have completed), while functions in Node.js are designed to be non-blocking (commands execute in parallel, and use callbacks to signal completion or failure)." [Wikipedia](https://en.wikipedia.org/wiki/Node.js)

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

# Installing and running on Windows

## Install

* Straightforward MSI install

	[Download](https://nodejs.org/en/)

## Run

* To run the Node.js shell (REPL - Read Evaluate Print Loop) from command line:

	`node` - displays the interactive shell from which you can run JavaScript, including multi-line commands such as **for loops** and **functions**.

	Note: Make sure the Add Path was selected during installation (default) so it is on the path.

	Note: the installation also installs a shortcut to this command that you can search for

* To run a script from the command line

	```
	node example.js
	```

* To exit the node shell

	```
	.exit
	```

	or

	`Ctr-C Ctrl-C`

# Install on Ubuntu

```
sudo apt-get install build-essential
sudo apt-get install nodejs npm
```

# Run in Visual Studio

* Make sure Node.js was installed with Visual Studio Installer
* Create a new Node.js project with one of the provided templates.

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

# Packages and Modules

## Popular Modules

* Express - Web development framework
* Connect - Extensible HTTP server framework.  Base line for Express
* Socket.io - Server side component for web sockets
* Pug / Jade - Template engine inspired by HAML.  Default template manager for Express
* Mongo/Mongoose - Wrappers to interact with MongoDB

## package.json

* Important JSON file that goes in the root of your module or project folder.  Configuration file used to tell how to install your module or app.
* "main" in this file is the entry point script for the project
* "dependencies" lists all the required modules (use an asterisks to specify the latest version of a module.
* You can use `npm init` to create this file for you.

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

# Examples

## Simple Server App
 
* Create the project folder with a file named **server.js**
* Create the package.json file

	```
	npm init
	```
	Follow the prompts making sure the "main" entry point is **server.js**

* Enter code in **server.js**

	```
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

* Run script

	```
	node server
	```
	This will run the server.  The server will remain running until you type `Ctrl-c`.  The console output `Server started on port: 3000` will display.  If you connect to the server in the browser with `localhost:3000` it will display `Hello World`

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
	This will run the server.  The server will remain running until you type `Ctrl-c`.  The console output `Server started on port: 3000` will display.  If you connect to the server in the browser with `localhost:3000` it will display the index.html web page read from the file system.

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
