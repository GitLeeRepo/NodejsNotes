# Overview

Notes on Node.js server side JavaScript environment

# References

* [Main Site](https://nodejs.org/en/)

* [Node.js for Beginners](https://www.youtube.com/watch?v=U8XF6AFGqlc) YouTube video by Traversey Media.  Several of the notes here taken from this video.

# Installing and running on Windows

* Straightforward msi install

[Download](https://nodejs.org/en/)

* To run the Node.js shell (REPL - Read Evaluate Print Loop) from command line:

`node` - displays the interactive shell from which you can run JavaScript, including multi-line commands such as **for loops** and **functions**.

Note: Make sure the Add Path was selected during installation (default) so it is on the path.

Note: the installation also installs a shortcut to this command that you can search for

* To exit the node shell

`.exit`

# Run in Visual Studio

* Make sure Node.js was installed with Visual Studio Installer

* Create a new Node.js project with one of the provided templates.

# NPM package manager

* Make sure it was part of the install (default)

* Used to install Node.js packages and modules

* Example - Installing a NPM package local to the project

`npm install express`

Installs the **express** module into the **node_modules** folder

* Example - Installing a NPM package globally

`npm install -g express`

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

* "dependencies" lists all the required modules (use an astricks to specify the latest version of a module.

* You can use `npm init` to create this file for you.

# Creating -g REST APIs

* Node is used extensively for creating REST APIs
