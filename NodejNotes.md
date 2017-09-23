# Overview

Notes on Node.js server side JavaScript environment

# References

* [Main Site](https://nodejs.org/en/)

* [Node.js for Beginners](https://www.youtube.com/watch?v=U8XF6AFGqlc) YouTube video by Traversey Media

# Installing and running on Windows

* Straightforward msi install

[Download](https://nodejs.org/en/)

* To run the Node.js shell from command line:

`node` - displays the interactive shell

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

# Popular Modules

* Express - Web development framework

* Connect - Extensible HTTP server framework

* Socket.io - Server side component for web sockets

* Mongo/Mongoose - Wrappers to interact with MongoDB

# Creating -g REST APIs

* Node is used extensively for creating REST APIs
