Node.js
[About Node.js](https://nodejs.org/en/about/)

Node.js is "an asynchronous event-driven JavaScript runtime, Node.js is designed to build scalable network applications...Users of Node.js are free from worries of dead-locking the process, since there are no locks. Almost no function in Node.js directly performs I/O, so the process never blocks. Because nothing blocks, scalable systems are very reasonable to develop in Node.js."

Where is Node.js found?

* Microservices and APIs
* Serverless Cloud Functions
* Command Line Applications
* Desktop Applications

Node is a run-time environment for running JS code. It is based on the Google Chrome V8 JS engine.

Do not use Node for CPU-intensive apps. LIke image processing or some other heavy processing. Since Node is single threaded, other requests will have to wait while the one heavy processing request is executed. The requests need to be handled quickly.

Should only be used for data-intensive apps and real-time apps. Maybe can be used for a game server.

## Getting Started with Node  
* Node is a runtime environment for executing JS code.  
* Essentially, Node is a C++ program that embeds Chrome’s v8 engine, the fastest JS engine in the world.  
* We use Node to build fast and scalable networking applications. It’s a perfect choice for building RESTful services.  
* Node applications are single-threaded. That means a single thread is used to serve all clients.  
* Node applications are asynchronous or non-blocking by default. That means when the application involves I/O operations (eg accessing the file system or the network), the thread doesn’t wait (or block) for the result of the operation. It is released to serve other clients.  
* This architecture makes Node ideal for building I/O-intensive applications.  
* You should avoid using Node for CPU-intensive applications, such as a video encoding service. Because while executing these operations, other clients have to wait for the single thread to finish its job and be ready to serve them.  
* In Node, we don’t have browser environment objects such as window or the document object. Instead, we have other objects that are not available in browsers, such as objects for working with the file system, network, operating system, etc. 

## Module

console.log() // console is global object in JS
setTimeout() // global function
clearTimeout()
setInterval()
clearInterval()

All these functions are a part of the **window** object in the browser.

var message = ‘’; // creates a global variable and attach to window object.
Window.message

In Node:
Global.console

File variables and functions are only accessible in the file, ie they are scoped to the file. They are not included in the global object.

Avoid defining variables and functions in the global scope. They can overwrite each other. Better to use modules.

Every file in a node application is a module. All variables or functions are scoped to that file. All of these are private by default. If they are to be seen from without the module, they need to be explicitly exported. Every node app as a least one module (or file) known as the main module.

somefile.js:  

    // the variable url and the function log are scoped to this module. They are not
    // visible out side the module.
    
    var url='http:/logger.io/log;
    
    function log(message) {
        // send message via HTTP request to logger service
        console.log(message);
    }
    
    // add the log method to the exports object and set it to log
    module.exports.log = log;
    
    // can also export variable
    module.exports.url = url;
    
When an item is exported (variable, object, function, ...), the exported name can be different from the item being exported:

    module.exports.endpoint = url;

Module is an object that resides in a module. Each module has one. It is a json object.

Can export a single function or an object.

To export single function:

    module.exports = someFunc;

Node takes all the code in a file (module) and wraps it in a function:

    (function (exports, require, module, __filename, __dirname) {
        // all the code in a module
    }

That is, Node does not execute the code directly. It calls the wrapper function which then calls the module code.

Creating package.json:
$npm init -y

$npm list    // to list all of the installed packages and their dependencies
$npm list --depth=0  // to list only your project’s dependencies

Semantic Version
Major.Minor.Patch
^4.6.7   // interested in any version where the major version is 4. The minor and patch version can change, but not the major version. This is same as 4.x

~1.8.6 // interested in any patch version. 1.8.x. Major and minor versions must be 1 and 8 respectively.

$npm view <package> // view registry info for a package
$npm view mongoose

$npm view mongoose dependencies  // only look at the dependency property
$npm view mongoose versions // display all versions of mongoose

To install a specific version:
$npm install mongoose@2.4.3

$npm outdated // this lists the packages and their currently installed version, the “wanted” version and the latest version.

$npm update  // only works for minor and patch number releases

$npm i -g npm-check-updates  // -g installs package globally
$npm-check-updates -u   // to update package.json
Or
$ncu -u

Then to $npm install to actually update the package to the new version.

$npm i jshint --save-dev   // development dependency ie not for production

$npm uninstall mongoose  // to uninstall package
$npm i -g npm   // to update npm to latest version

$npm -g outdated  // to see which global packages are outdated

Express for ease in creating routes
Joi for validation

Building RESTful APIs with Express
So, in this section, you learned that:
-
REST defines a set of conventions for creating HTTP services:
-
POST: to create a resource
-
PUT: to update it
-
GET: to read it
-
DELETE: to delete it
-
Express is a simple, minimalistic and lightweight framework for building web
servers.
// Build a web server
const express = require(‘express’);
const app = express();
// Creating a course
app.post(‘/api/courses’, (req, res) => {
    // Create the course and return the course object
    resn.send(course);
});
// Getting all the courses
app.get(‘/api/courses’, (req, res) => {
     // To read query string parameters (?sortBy=name)
     const sortBy =
req.query.sortBy
;
     // Return the courses 
     res.send(courses);
});
// Getting a single course
app.get(‘/api/courses/:id’, (req, res) => {
    const courseId =
req.params.id;
    // Lookup the course
    // If not found, return 404
    res.status(404).send(‘Course not found.’);
    // Else, return the course object
    res.send(course);
});
// Updating a course
app.put(‘/api/courses/:id’, (req, res) => {
    // If course not found, return 404, otherwise update it
    // and return the updated object.
});
// Deleting a course
app.delete(‘/api/courses/:id’, (req, res) => {
    // If course not found, return 404, otherwise delete it
    // and return the deleted object.
});
// Listen on port 3000
app.listen
(3000, () => console.log(‘Listening...’));
-
We use
Nodemon
to watch for changes in files and automatically restart the
node process.
-
We can use environment variables to store various settings for an application. To
read an environment variable, we use
process.env.
// Reading the port from an environment variable
const port = process.env.PORT || 3000;
app.listen(port);
-
You should never trust data sent by the client. Always validate! Use
Joi
package
to perform input validation.

A middleware function is a function that takes a request object and either returns a response to the client or passes control to another middleware function. Route handler functions are middleware functions.






Green ovals are middleware functions. This is the request processing pipeline.


3rd Party Middleware
helmet // helps secure  your app
morgan // to log http requests




Electronjs.org

"Electron JS is a runtime framework that allows the user to create desktop-suite applications with HTML5, CSS, and JavaScript. It’s an open source project started by Cheng Zhao, an engineer at GitHub.

It is basically a blend of two incredibly popular technologies: Node.js and Chromium. Thus, any web application you have written can run on Electron JS. Similarly, any Node.js application you write can utilize this technology."

### Apps based on Electron ###

* Skype
* Github Desltop
* Hyper
* VSCode
* Slack
* Atom
* etc

### Node.js is create from ###  
* Chrome's V* JavaScript runtime engine
* libuv for asynchromous I/O and the event loop


### Tesing

* Mocha
* Chai
* Sinon
* Istanbul

### Why Node

* Easy to run JS on backend server (V8)
* Built-in modules (fs, http, crypt, zip,
* Asynchronous APIs (no threads), non-blocking
* C++ addons - can write these in C++ and install them in node.
* Has good debugger and other utilities
* NPM
* Module dependency manager (CommonJS)

[Node.js for React](https://jscomplete.com/learn/why-node-for-react)

[Node Test](http://bit.ly/node-test)



[Code for Course](https://github.com/jscomplete/ngs)

### Node with Mosh



