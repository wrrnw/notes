# Questions Summary

## 1. Git
- Know basic git commands


## 2. JavaScript, Node & Express, API Servers & REST
- Suppose we have the HTML element: `<p id="demo"></p>`. Write the JavaScript code(including the `<script>` tags) to display *Hello World* in the element
	``` html
	<script>
	function myFunction() {
		document.getElementById("demo").innerHTML = "Hello World";
	}
	</script>
	```
- List at least two different ways of accessing an HTML element using JavaScript
	1. document.getElementById('idname'):  its ID name
	2. document.getElementsByClassName('classname'): by the given classname
	3. document.getElementsByTagName('tagname'): using the tag name
	4. document.querySelector(): using the css style selector
- What is Node.js?
	- Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient
- What is npm?
	- The node.js package manager, which is the largest ecosystem of open source libraries in the world
- What is Express?
	- Express is a minimal and flexible Node.js web application framework
- How to Express?
	1. Create dir and app.js
	2. Install express: `npm install express --save`
	3. Require Express: `const express = require('express');`
	4. `const app = express();`
	5. Create routes: `/: print Hello World`
	6. Listen on a port
	``` js
	app.listen(3000, function() {
		console.log('Express serving at port 3000');
	});
	```
- How to create a Routes including id?
	- `/post/:id`
- How to retrieve a id
	- `req.params.id`
- Write a very simple express application which will display *Hello World* when as user accesses the homepage
	``` js
	var express = require('express');
	var app = express();
	app.get('/', function(req, res) {
		res.send("Hello World");
	})
	```
- What is Client API?
	- Client API or Web Browser API or Client-side Web API are components that run on the client side, i.e. the browser. There are many APIs that exists for different purposes, for example, to load data dynamically (AJAX), and access and manipulate multimedia content.
- What is AJAX?
	- AJAX stands for Asynchronous JavaScript And XML, which is a mechanism of loading dynamic content within a page without loading the entire page
- What is REST?
	- Stands for Representational State Transfer. It is a architectural principle that defines client-server relationship and how state stored. RESTful server is stateless that it does not remember state on the server. Each request must contain all of the information needed to fulfill the request
	- Client remembers everything it needs
	- Passes this to the server when it wants to get something done
	- The server doesn't need to remember anything about the client
	- Often use HTTP protocol verbs(GET, PUT, POST, DELETE)


## 3. MongoDB
- Advantages of MongoDB
	- NoSQL: No transactions & No joins
- What is Mongoose?
	- Mongoose is a MongoDB object modeling tool. It provides a schema-based solution to model your database
- Define a schema named *student* with two attributes *name* and *ID*. You can choose appropriate properties for the attributes
	``` js
	var mongoose = require('mongoose');
	var Schema = mongoose.Schema;
	var student = new Schema({
		name: String,
		id: Date
	});
	```
- Know how to write controller.js with MongoDB


## 4. Responsive Web Design (HTML & CSS)
- Know CSS grid details
- What is the general approaches of responsive design
	1. Add some viewport tags or elements to each of the pages
	2. Use CSS grid to organize content
	3. Choose breakpoint to decide when we reorganize the content using media queries
- How to achieve media queries, please give one example using code:
	``` html
	<link rel="stylesheet" href="styles.css">
	<link rel="stylesheet" media="screen and (min-width:500px;)" href="large.css">
	```
- How to achieve responsive design regarding above code?
``` css
.page {
	display:grid;
	grid-template-columns:2fr 1fr 1fr;
	grid-template-rows:4em auto;
	grid-template-areas:
		"article header aside"
		"article figure figure";
}

@media screen and (min-width: 922px) {
.page {
	grid-template-columns:1fr 3fr;
	grid-template-rows:1fr 2fr auto;
	grid-template-areas:
		"header header"
		"figure figure"
		"aside article"
	}
}
```


## 5. Security
- What is MD5?
	- MD5 is the most widely known hashing function
- What is XMLHttpRequest(XHR)?
	- XMLHttpRequest(XHR) is an API in the form of an object whose methods transfer data between a web browser and a web server
- In risk assessment, what do we call an event that provide signs that an identified risk may actually be happening?
	- Trigger
- In risk assessment, what is Risk?
	- An undesirable event with the potential to have a negative impact on the project
- In risk assessment, what is Trigger?
	- An event that provides noticeable signs for the group that the risk may actually be happening
- In risk assessment, what is Likelihood?
	- Chance of the risk occurring, rated on the likely, possible or unlikely
- In risk assessment, what is Impact?
	- Extend to which the group will suffer as a result of risk occurring, rated as major, moderate or minor
- In risk assessment, what is Contingency Plan?
	- What to do in the event of the risk actually happening


## 6. Testing
- State two reasons for testing your web-application
	1. error-free - that is contain no bugs. We should test for both syntactic and semantic errors
	2. predictable. We implement functionality to achieve certain tasks. We want to make sure that when we execute a functionality, the outcomes are as we intended to be, not only the first time but always
	3. Resilient to changes - that is be able to handle changes to functionality. Over the life of our web application, we will either enhance existing functionalities or implement new ones. When we change a functionality, we can re-run all of our tests to ensure that other components that may be dependent on the changed components continues to function as we intended
- What is Mocha?
	- Mocha is a test framework running on Node.js and in the browser. We use Mocha for testing software functionality written in JavaScript. We write our own test cases and run the tests with Mocha to identify potential flaws in our web applications
- Draw a diagram to show the basic testing cycle
- Know how to write testing code


## 7. SEO & Accessibility
- What is SEO?
	- SEO stands for Search Engine Optimisation. It is a set of strategies and techniques for increasing the number of visitors(visibility) to your website by obtaining a higher rank in search result pages
- What is the goal of a *crawler*?
	- It's to crawl the web pages; parse content; categorise content; and build an index
- What search engines rank depend on?
	- Search Engines rank websites depend on how keywords and elements in their content
- SEO criteria
	- Contents
	- Links to the page
	- Code Implementation
	- Authority
-  Percentage of traffic incoming from
	1. Organic(non-paid) Search - 64%
	2. Non-social referrals - 15%
	3. Direct - 12%
	4. Paid Listings - 6%
	5. Social Media - 2%
- Questions for selecting keywords
	1. Which keywords they search with?
	2. How frequently they are?
	3. How relevant they are?
	4. How competitive they are?
- 70% of keywords are searched for only hundreds of times or less. They are known as long tail of keyword demand


## 8. Localisation & Internationalisation
- When you want to design your website for international community, what are factors that you need to consider?
	- language
	- time formats
	- Currency and tex regulation
	- decimal system
	- units
	- implied meaning of symbols and colours
