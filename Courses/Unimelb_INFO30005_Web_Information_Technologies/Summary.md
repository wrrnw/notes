# INFO30005 Web Information Technologies Summary


## Overview
- Version: 2019 Semester 1
- Lecturer: [Eduardo Oliveira](https://www.eduoliveira.com/) and [Ronal Singh](https://cis.unimelb.edu.au/people/rr-singh)
- Full stack project based course
- Programming part has not been teached in detail, which means you need to find many other resources to learn full stack dev



## Week 1 Lecture 1 Introduction to the subject (Not Examinable)


## Week 1 Lecture 2 History of Web & Introduction to web development (Not Examinable)
- **History**
	- WWW: World Wide Web
	- URL: Uniform Resources Locator
	- HTML: HyperText Markup Language
	- HTTP: HyperText Transport Protocol
	- Type of Web Hosts
		- Self-Service
		- Co-Located
		- Dedicated
		- Virtual Private(VPS)
		- Cloud
		- Shared
		- Managed
	- ISP: Internet Service Provider
	- DNS: Domain Name Server
		- Request Recursive Name Server
		- Root Name Server
- **Web Dev**
	- Web 1.0 - Static Web
		- Content: Reading content, Personal Site, Content Ownership, Taxonomies
		- Tech: HTML, HTTP, Synchronous, Client-Server
	![Web Illustration_1](Image/Web_illustration_1.png)
	![Web Illustration_2](Image/Web_illustration_2.png)
	- Web 2.0 - Wisdom Site
		- Web apps that behave like native app
		- AJAX: Asynchronous JavaScript and XML
		- Content: Creating Content, Blogs & Profiles, User Content, Folksonomies
		- Tech: HTML, AJAX, HTTP, JSON, Asynchronous, Peer-to-Peer, REST, SOAP
		- Front-End
			- Web Design: Photoshop, Illustrator, Dreamweaver, XD
			- Front-End Dev: HTML, CSS, JavaScript, Angular
		- Back-End:
			- Application: PHP(cake), Ruby(Rails), JS(Node), Python(Django)
			- Server: Apache, IIS, GWS, Express
			- Database: MySQL, MongoDB, Oracle, S2Lite
![Web1.0](Image/Web1.0.png)
![Web2.0](Image/Web2.0.png)
![HTML5](Image/HTML5.png)


## Week 2 Lecture 1 Basic Technologies - Git
- Why use version control
	- Compare Files
	- Identify Differences
	- Merge Changes
	- Revert to previous working code
	- Snapshot
- Commands
	- `git init`: creates the repo
	- `git clone`: clones a remote repo
	- `git status`: status of repo
	- `git add <file>`: add file to staging area
	- `git add -A`: add all to staging area
	- `git checkout -- <file>`: undo uncommitted changes
	- `git add *.<extension>`: add all with extension to staging area
	- `git commit -m "<message>"`: commit changes to repo
	- `git log`: show commit history
	- `git checkout <commit_id>`: move head to that commit
	- `git revert --no-commit <id>..HEAD`
	- `git commit` revert to that commit
	- `git diff` compares with last commit
- `pull` and `push`
	- `pull`: to synchronize all of changes in the server to my local machine
	- `push`: put all of the local changes to the server
- Branches
	- `git branch`: show branches
	- `git checkout -b <branch>`: create a new branch
	- `git merge <branch>`: merges with branch
	- `git branch -d <branch>`: delete branch
- Some advises
	1. Commit often
	2. Commit related changes together
	3. Commit completed work
	4. Branch before you build
	5. Commit with meaningful message
	6. Agree on a workflow
- Atlassian SourceTree
- .gitignore


## Week 2 Lecture 2 Basic Technologies - JavaScript
### HTML - Structure
- `<b><\b>` **bold** in HTML4; visual emphasis in HTML5
- `<i><\i>` *italic* in HTML4; Alternative voice in HTML5
- `<u><\u>` underline in HTML4; non-textual annotation IN HTML5
- `<s><\s>` ~~strikethrough~~ in HTML4; Incorrect in HTML5
- `<em>` Emphasis or stress
- `<strong>` Importance
- `<mark>` Relevance
### CSS - Presentation
### JavaScript - Behaviour
- Print to console
	- `console.log("starting to print")`
- HTML + JavaScript
``` html
<!DOCTYPE html>
	<html>
		<body>
			<h1>A Web Page<\h1>
			<p id="demo">A paragraph<\p>
			<button type="button" onclick="myFunction()">Try it<\button>
			<script>
				function myFunction() {
					document.getElementById("demo").innerHTML = "paragraph changed."
				}
			<\script>		
		<\body>
	<\html>
```
- Better to divide into modules
	- `<script src="myScript.js"><\script>`
- Variables
	- a


## Week 3 Node & Express
- What is **Node**?
	- Node.js is a JavaScript **runtime** built on Chrome's V8 JavaScript engine. Node.js uses an **event-driven**, **non-blocking I/O** model that makes it **lightweight** and **efficient**. Node.js package ecosystem, npm, is the largest ecosystem of open source libraries in the world
- What is Node good for?
	- I/O Bound Application
	- JSON APIs
	- Big Data
	- Single-Page Applications
- Advantages of Node
	- Npm
	- Use JavaScript
	- Great Libraries
	- High-performance
	- Open source
	- Great for apis
	- Asynchronous
	- Great Community
	- Great for realtime apps
	- Great for command line utilities
- Npm (Node Package Manager)
	- Package manager for JS
	- Public registry
	- Centralised
	- Accessible via the cmd
	- Easy to share code
	- `npm install <package>`
	- `var <varname> = require("package");`
	- `npm init`
	- answer questions
	- check *package.json*
- Modularising Your Code
``` js
module.export = {
	key : value
}
```
``` js
const library = require('./library.js');
let value = libirary.key;
```
- Core Packages
	- *fs*: file system
	- *net*: TCP client and servers
	- *http* and *https*: basic web server
	- *dns*: domain name resolution
	- *assert*: writing tests
	- *os*: querying the operating system
- **Express**
	- Streamlined Node
	- Server methods
	- Routing
	- Easy APIs
	- Middleware friendly
- **Comparison between Node.js and Express.js**
	- Node.js is a platform for building server-side event-driven I/O application using JavaScript
	- Express.js is a framework based on Node.js for building web-application using principles and approaches of Node.js
- **Express Application Example**
	- Create dir and app.js
	- Install express: `npm install express --save`
	- Require express
	- `var app = express();`
	- Create routes:
		- `/: print Hello World!`
		- `/bye: print Goodbye World!`
	- Listen on a port
``` js
const express = require('express');
const app = express();

app.get('/', function(req, res) {
	res.send("Hello World");
});

app.get('/bye', function(req, res) {
	res.send("Goodbye world");
});

app.listen(3000, function() {
	console.log('Express serving at port 3000');
});
```
- Routes
	- `/` Just the URL
	- `*` catch all
	- `/:pattern` catches URLs that match the pattern
		- e.g. `/post/:id`
		- `www.blog.com/post/123123` matches
		- `www.blog.com/123123` does not match
		- id can be retrieved: `req.params.id`
- Organising Node Project
	- package.json
	- public/
	- node_modules/
	- app.js
	- models/
	- views/
	- controllers/
	- routes/
	- middleware/
- Create controller/controller.js
``` js
const posts = require('../models/posts');

module.exports.fetchMainPage = function(req, res) {
	res.send("Welcome to my Blog!");
};

module.exports.fetchAllPosts = function(req, res) {
	res.send(posts);
};

module.exports.fetchPost = function(req, res) {
	const post = posts[req.params.id];
	res.render('post_template', {post:post});
};
```
- Create routes/routes.js
``` js
const express = require('express');
const router = express.Router();
const controller = require('../controllers/controllers');

router.get('/', controller.fetchMainPage);
router.get('/posts', controllers.fetchAllPosts);
router.get('/posts/:id', controllers.fetchPost);
module.exports = router;
```
- Global vs. Local Installation
	- Local Installation
		- If you're installing something that you want to use in your program, using require(whatever'), then install it locally, at the root of your project
		- `npm root`
		- `npm list`
	- Global Installation
		- If you're installing something that you want to use in your shell, on the command line or something, install it globally, so that its binaries end up in your *PATH* environment variable
		- `npm root -g`
		- `npm list -g`


## Week 4 Lecture 1 API servers and REST
- **API** (Application Programming Interface)
![API Illustration](Image/api.png)
- **REST** (Representational State Transfer)
	- Regular way the internet works
	- Is about resources, not about functions
	- Is stateless
- **HTTP** (Hypertext Transfer Protocol)
	- HTTP verbs/methods
		- *POST* create
		- *GET* read
		- *PUT* update
		- *DELETE* delete
- **HTTP Request**
![HTTP Request Example](Image/http_request.png)
- **HTTP Response**
![HTTP Response Example](Image/http_response.png)
- **Restful Routes**
![Restful Routes Example](Image/restful_routes.png)


## Week 4 Lecture 2 MongoDB & Mongoose
- **MongoDB**
	- NoSQL: no transactions; no joins
	- Create and store objects. Arrange them in collections; Retrieve them later
	- Data store for JSON objects
- **MongoDB CRUD**
	- Create
		- `db.collection.insert(<document>)`
		- `db.collection.save(<document>)`
		- `db.collection.update(<query>, <update>, {upsert: true})`
	- Read
		- `db.collection.find(<query>, <projection>)`
		- `db.collection.findOne(<query>, <projection>)`
	- Update
		- `db.collection.update(<query>, <update>, <options>)`
	- Delete
		- `db.collection.remove(<query>, <justOne>)`
- **How to connect our app to MongoDB database**
	- Use mongoose
	- `var mongoose = require('mongoose')`
- **A whole view app**
	- under construction
- **Deploy Online**
	- Use heroku


## Week 5 Lecture 1 HTML & CSS
- Some material have been already covered in Week 2 Lecture 2
### HTML (Hyper Text Markup Language)
- `<element>` void element
- **Image and figure**
	- `<img src="kofster.jpg" alt="Barista pouring coffee into a glass bottle">`
	- It is better to separate the description and figure
``` html
<figure>
	<img src="kofster.jpg" alt="Barista pouring coffee into a glass bottle">
	<figcaption>The Barefoot Coffee Shop</figcaption>
</figure>
```
- **Lists**
``` html
<!-- Ordered list -->
<ol>
	<li></li>
	<li></li>
	<li></li>
</ol>
<!-- Unordered list -->
<ul>
	<li></li>
	<li></li>
	<li></li>
</ul>
```
- **Description Lists**
``` html
<dl>
	<dt></dt> <!-- term -->
	<dd></dd> <!-- description -->
	<dt></dt>
	<dd></dd>
</dl>
```
- **Generic Elements**
	- `<div>` block
	- `<span>` Inline
- **Identifying Elements**
	- `<div id="unique_id" class="class1 class2">`
		- id is unique but class is not
- **Tables**
``` html
<table>
	<tr>
		<th>Item</th>
		<th>Size</th>
		<th>Price</th>
	</tr>
	<tr>
		<td rowspan="3">Espresso</td>
		<td>Small</td>
		<td>$2.50</td>
	</tr>
	<tr>
		<td>Medium</td>
		<td>$3.00</td>
	</tr>
	<tr>
		<td>Large</td>
		<td>$3.50</td>
	</tr>
</table>
```
- **Links**
	- `a href="http://www.kofster.com">Kofster</a>`
	- Absolute URLs
		- `<a href="http://www.kofster.com/home">`
	- Relative
		- `<a href="/home">`
		- `<a href="#tag_id">`
- **Forms**
	- `<form action="/myaction" method="post">`
``` html
<form action="/myaction" method="post">
	Username:
	<input type="text" name="username"><br>
	Email:
	<input type="email" name="email"><br>
	Password:
	<input type="password" name="psw"><br>
	<input type="submit">
</form>
```
### CSS (Cascading Style Sheets)
- Inline
``` html
<h1 style="color:blue">Hello!</h1>
```
- Internal
``` html
<head><style>
	h1{color:blue}
</style></head>
```
- External File
``` html
<head>
	<link rel="stylesheet" href="styles.css">
</head>
```
- **Selectors**
![CSS Demonstration 1](Image/css1.png)
![CSS Demonstration 2](Image/css2.png)
![CSS Demonstration 3](Image/css3.png)
![CSS Demonstration 4](Image/css4.png)
![CSS Demonstration 5](Image/css5.png)
![CSS Demonstration 6](Image/css6.png)
![CSS Demonstration 7](Image/css7.png)
![CSS Demonstration 8](Image/css8.png)

## Week 5 Lecture 2 Design Principle: Layout, Typography, Colour (Not Examinable)


## Week 6 Lecture 1 Design Thinking (Not Examinable)


## Week 6 Lecture 2 Usability


## Week 7 Lecture 1 Responsive Design and Advanced JavaScript (Advanced JavaScript Not Examinable)


## Week 7 Lecture 2 API Client ES6, Sass, Babel (Sass & Babel Not Examinable)


## Week 8 Security and Risk (Security Principles, Risk assessment)


## Week 9 Lecture 1 Testing


## Week 9 Lecture 2 First Exam Review
### **Type of Questions**
 8 - 10 Questions including: Multiple Choice, Short Answers, Long Answers
### **Some Example Questions**
#### **Multiple Choice Questions**
- Inside which HTML element do we put the JavaScript
	- <Script\>
- How to change the HTML element below using JavaScript?  `<p id="demo">This is just a demo for you</p> `
	- `Document.getElementById("demo").innerHTML = "Hello"`
#### **Short Answers Questions**
- List three git commands to a. Clone a repository b. Add a file to staging area c. Commit a file
	- a. git clone http://www.github.com/libgit2/libgit2.git
	- b. git add *.c
	- c. git commit -m "initialisation"
- What is XMLHttpRequest (XHR)
	- XMLHttpRequest(XHR) is an API in the form of object whose methods transfer data between a web browser and a web server
- State two reasons for testing your web-application
	- Error free. That is contain no (or at least possible number of) bugs
	- Predictable. We implement functionality to achieve certain tasks. We want to make sure that when we execute a functionality, the outcomes as we intended to be, not only the first time but always
	- Resilient to changes. That is be able to handle changes to functionality. Over the life of our web application, we will either enhance existing functionality or implement new ones. When we change a functionality, we can re-run all of our tests to ensure that other components (e.g. functions or classes) that may be dependent on the changed components continues to function as we intended
- Given the following HTML&CSS, what the colour of "Hello"
``` html
 <html>
	 <body class="red">
		 <h1 class="blue">
			 Hello
		 </h1>
	 </body>
 </html>
```
``` css
.blue {
	color: blue;
}
.red {
	color: red;
}
```

- Use the following incomplete tests to answer the two questions that follow. Write the missing assertion statement for testing the value of the variable *prod*, which is expected to be equal to *2.2*
``` javascript
var assert = require('assert');
describe('Mocha Test', function() {
	it('checking the product of two numbers', function() {
		var prod = 1.0 * 2.2;
		// Missing assertion
	});
	it('check the length of a string', function() {
		assert.strictEqual("mocha".length, 5);
	});
});
```
 `assert.strictEqual(prod, 2.2);`
 #### **Long Answers Questions**
- Question 1
![Long Answers Question 1](Image/long_answers_question_1.png)
- Question 1 Answer
![Long Answers Question 1 Answer](Image/long_answers_question_1_answer.png)
- Question 2
![Long Answers Question 2](Image/long_answers_question_2.png)
- Question 2 Answer
![Long Answers Question 2 Answer](Image/long_answers_question_2_answer.png)


## Week 10 Lecture 1 Expanding your Reach (SEO, Accessibility)


## Week 10 Lecture 2 Localisation & Internationalisation


## Week 11 Lecture 1 Future of The Web (Not Examinable)


## Week 11 Lecture 2 Web of things (Not Examinable)


## Week 12 Lecture 1 Project Showcase
- No New Content


## Week 12 Lecture 2 Second Exam Review
- Go over the sample exam paper
