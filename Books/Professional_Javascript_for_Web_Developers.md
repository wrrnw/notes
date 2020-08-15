# Notes for Book \<Professional JavaScript for Web Developers\>

## Chapter 1 What is JavaScript

### 1.1 A Short History

### 1.2 JavaScript Implementation
#### 1.2.1 ECMAScript
#### 1.2.2 The Document Object Model (DOM)
#### 1.2.3 The Browser Object Model (BOM)

### 1.3 JavaScript Versions



## Chapter 2 JavaScript in HTML
### 2.1 The <script\> Element
#### 2.1.1 Tag Placement
#### 2.1.2 Deferred Scripts
#### 2.1.3 Asynchronous Script
#### 2.1.4 Changes in XHTML
#### 2.1.5 Deprecated Syntax

### 2.2 Inline Code versus External Files
### 2.3 Document Modes
### 2.4 The <noscript\> Element


## Chapter 3 Language Basics
### 3.1 Syntax
#### 3.1.1 Case-sensitivity
#### 3.1.2 Identifiers
#### 3.1.3 Comments
#### 3.1.4 Strict Mode
- To enable strict mode for an entire script, including the following at the top:
	- `"use strict"`
- To enable strict mode in just a function
	``` javascript
	function doSomething() {
		"use strict"
		// fuction body
	}
	```
#### 3.1.5 Statements
### 3.2 Keywords and Reserved words
### 3.3 Variables
- ECMAScript variables are loosely typed, meaning that a variable can hold any type of data. Every variable is simply a named placeholder for a value
- To define a variable, use the *var* operator followed by the variable name
- Using the *var* operator to define a variable makes it local to the scope in which it was defined. For example, defining a variable inside of a function using var means that the variable is destroyed as soon as the function exits
``` javascript
function test() {
	var message = "hi"; //local variable
}
test()
alert(message) //error
```
- It is possible to define a variable globally by simply omitting the *var* operator. As soon as the function *test()* is called, the variable is defined and becomes accessible outside of the function once it has been executed
``` javascript
function test() {
	message = "hi"; //global variable
}
test();
alert(message); //"hi"
```
- Although it's possible to define global variables by omitting the *var* operator, this approach is not recommended. Global variables defined locally are hard to maintain and cause confusion, because it's not immediately apparent if the omission of *var* was intentional. Strict mode throws a *ReferenceError* when an undeclared variable is assigned a value

### 3.4 Data Types
- There are five simple data types (also called primitive types) in ECMAScript: Undefined, Null, Boolean, Number, and String. There is also one complex data type called Object, which is an unordered list of name-value pairs. Any values can be represented as one of six.

#### 3.4.1 The typeof Operator
- The *typeof* operator is used to determine the data type of a given variable
	- "undefined" if the value is undefined
	- "boolean" if the value is Boolean
	- "string" if the value is string
	- "number" if the value is number
	- "object" if the value is an object (other than a function) or *null*
	- "function" if the value is a function
- Note that because *typeof* is an operator and not a function, no parentheses are required (although they can be used)
- Calling *typeof null* returns a value of "*object*", as the special value *null* is considered to be an empty object reference

#### 3.4.2 The Undefined Type
- The Undefined type has only one value, which is the special value *undefined*. When a variable is declared using *var* but not initialized, it is assigned the value of *undefined* as following:
``` javascript
var message
alert(message == undefined); //true
```
- Note that a variable containing the value of *undefined* is different from a variable that hasn't been defined at all
``` javascript
var message; //this variable is declared but has a value of undefined

//make sure this variable isn't declared
//var age

alert(message); //"undefined"
alert(age); //causes an error
```
- The *typeof* operator returns "undefined" when called on an uninitialized variable, but is also returns "*undefined*" when called on an undeclared variable, which can be a bit confusing
``` javascript
var message; //this variable is declared but has a value of undefined

//make sure this variable isn't declared
//var age

alert(typeof message); //"undefined"
alert(typeof age);     //"undefined"
```
- Even though uninitialized variables are automatically assigned a value of undefined, it is advisable to always initialize variables. That way, when *typeof* returns "undefined*, you'll know that it's because a given variable hasn't been declared rather than was simply not initialized

#### 3.4.3 The Null Type
- The Null type is the second data type that has only one value: the special value *null*. Logically, a *null* value is an empty object pointer, which is why *typeof* returns "object" when it's passed a null value
``` javascript
var car = null;
alert(typeof car); //"object"
```
- When defining a variable that is meant to later hold an object, it is advisable to initialize the variable to *null* as opposed to anything else. That way, you can explicitly check for the value *null* to determine if the variable has been filled with object reference at a later time
``` javascript
if (car != null) {
	//do something with car
}
```

#### 3.4.4 The Boolean Type
- The Boolean type has only two literal values: *true* and *false*. These values are distinct from numeric values, so *true* is not equal to 1, and *false* not equal to 0.
- To convert a value into its Boolean equivalent, the special *Boolean()* casting function is called
``` javascript
var message = "Hello world!"
var messageAsBoolean = Boolean(message);
```

#### 3.4.5 The Number Type
- Uses IEEE-754 format to represent both integers and floating-point values
- For an octal literal, the first digit must be a zero
- For a hexadecimal literal, the first two characters must be 0x (case insensitive)

##### 3.4.5.1 Floating-Point Values
- Because storing floating-point values uses twice as much memory as storing integer values, ECMAScript always looks for ways to convert values into integers.
- For very large or very small numbers, floating-point values can be represented using e-notation
- Floating-point values are accurate up to 17 decimal places but are far less accurate in arithmetic computations than whole numbers. For instance, adding 0.1 and 0.2 yields 0.30000000000000004 instead of 0.3. These small rounding errors make it difficult to test for specific floating-point values.
``` javascript
if (a + b == 0.3) {   //avoid!
	alert("You got 0.3.");
}
```
- You should never test for specific floating-point values
- It's important to understand that rounding errors are a side effect of the way floating-point arithmetic is done in IEEE-754 based numbers and is not unique to ECMAScript. Other language that use the same format have the same issues

##### 3.4.5.2 Range of Values
- Not all numbers in the world can be represented in ECMAScript, because of memory constraints
- The smallest number that can be represented in ECMAScript is stored in *Number.MIN_VALUE* and is 5e-324 on most browsers. The largest number is stored in *Number.MAX_VALUE* and is 1.7976931348623157e+308 on most browsers
- If a calculation results in a number that cannot be represented by JavaScript's numeric range, the number automatically gets the special value of *Infinity*.
- Any negative number that can't be represented is -*Infinity* (negative infinity), and any positive number that can't be represented is simply *Infinity* (positive infinity)
- To determine if a value is finite, there is the *isFinite() function
``` javascript
var result = Number.MAX_VALUE + Number.MIN_VALUE;
alert(isFinite(result)); //false
```
- Testing: Though it is rare to do calculations that take values outside of the range of finite numbers, it is possible and should be monitored when doing very large or very small calculations

##### 3.4.5.3 NaN
- *NaN* is a special numeric value, short for *Not a Number*, which is used to indicate when an operation intended to return a number has failed
- Unique properties of *NaN*
	1. Any operation involving *NaN* always returns *NaN* (for instance, Nan/10), which can be problematic in the case of multistep computations
	2. *NaN* is not equal to any value, including *NaN*
	``` javascript
	alert(NaN == NaN); //false
	```
- *isNaN()* can be used to determine if any data type passed has value "Not a number"

##### 3.4.5.4 Number Conversions
- There are three functions to convert non numeric values into numbers:
	1. *Number()* casting function. Can be used on any data type
	2. *parseInt()* function. Need to be used specifically for converting strings to numbers
	3. *parseFloat()* function. Need to be used specifically for converting strings to numbers
- The *Number()* function performs conversions based on these rules:
	- When applied to Boolean values, *true* and *false* get converted into 1 and 0, respectively
	- When applied to numbers, the value is simply passed through and returned
	- When applied to *null*, *Number()* returns *NaN*
	- When applied to strings, the following rules are applied:
		- If the string contains only numbers, optionally preceded by a plus or minus sign, it is always converted to a decimal number, so "1" becomes 1, "001" becomes 11
		- If the string contains a valid floating-point format, such as "1.1", it is converted into the appropriate floating-point numeric value
		- If the string contains a valid hexadecimal format, such as "0xf", it is converted into an integer that matches the hexadecimal value
		- If the string is empty, it is converted to 0
		- If the string contains anything other than these previous formats, it is converted to *NaN*
	- When applied to objects, the *valueof()* method is called and the returned value is converted based on the previously described rules. If that conversion results in *NaN*, the *toString()* method is called and the rules for converting strings are applied
- *parseInt()*
	- Can recognize various integer formats (decimal, octal, and hexadecimal)
	- Provide second argument the radix (number of digits) to use. If you know that the value you're parsing is in hexadecimal format, you can pass in the radix 16 as second argument
- *parseFloat()*
	- Initial zeros are always ignored
	- There is no radix mode

#### 3.4.5 The String Type
##### 3.4.5.1 Character Literals
##### 3.4.5.2 The Nature of Strings
##### 3.4.5.3 Converting to a String


#### 3.4.6 The Object Type


### 3.5 Operators

#### 3.5.1 Unary Operators
##### 3.5.1.1 Increment/Decrement
##### 3.5.1.2 Unary Plus and Minus

#### 3.5.2 Bitwise Operators
##### 3.5.2.1 Bitwise NOT
##### 3.5.2.2 Bitwise AND
##### 3.5.2.3 Bitwise OR
##### 3.5.2.4 Bitwise XOR
##### 3.5.2.5 Left Shift
##### 3.5.2.6 Signed Right Shift
##### 3.5.2.7 Unsigned Right Shift

#### 3.5.3 Boolean Operators
#### 3.5.4 Multiplicative Operators
#### 3.5.5 Additive Operators
#### 3.5.6 Relational Operators
#### 3.5.7 Equality Operators
#### 3.5.8 Conditional Operators
#### 3.5.9 Assignment Operators
#### 3.5.10 Comma Operators


### 3.6 Statements
#### 3.6.1 The if Statement
#### 3.6.2 The do-while Statement
#### 3.6.3 The while Statement
#### 3.6.4 The for Statement
#### 3.6.5 The for-in Statement
#### 3.6.6 Labeled Statements
#### 3.6.7 The break and continue Statement
#### 3.6.8 The with Statement
#### 3.6.9 The switch Statement


### 3.7 Functions
#### 3.7.1 Understanding Arguments
#### 3.7.2 No Overloading



## Chapter 4 Variables, Scope, and Memory

### 4.1 Primitive and Reference Values
#### 4.1.1 Dynamic Properties
#### 4.1.2 Copying values
#### 4.1.3 Argument Passing
#### 4.1.4 Determining Type

### 4.2 Execution Context and Scope
#### 4.2.1 Scope Chain Augmentation
#### 4.2.2 No Block-Level Scopes

### 4.3 Garbage Collection
#### 4.3.1 Mark-and-Sweep
#### 4.3.2 Reference Counting
#### 4.3.3 Performance
#### 4.3.4 Managing Memory


## Chapter 5 Reference Types

### 5.1 The Object Type

### 5.2 The Array Type
#### 5.2.1 Detecting Arrays
#### 5.2.2 Conversion Methods
#### 5.2.3 Stack Methods
#### 5.2.4 Queue Methods
#### 5.2.5 Reordering Methods
#### 5.2.6 Manipulation Methods
#### 5.2.7 Location Methods
#### 5.2.8 Iterative Methods
#### 5.2.9 Reduction Methods

### 5.3 The Data Type
#### 5.3.1 Inherited Methods
#### 5.3.2 Data-Formatting Methods
#### 5.3.3 Date/Time Component Methods

### 5.4 The RegExp Type
#### 5.4.1 RegExp Instance Properties
#### 5.4.2 RegExp Instance Methods
#### 5.4.3 RegExp Constructor Properties
#### 5.4.4 Pattern Limitations

### 5.5 The Function Type
#### 5.5.1 No Overloading (Revisited)
#### 5.5.2 Function Declarations versus Function Expressions
#### 5.5.3 Functions as Values
#### 5.5.4 Function Internals
#### 5.5.5 Function Properties and Methods

### 5.6 Primitive Wrapper Types
#### 5.6.1 The Boolean Type
#### 5.6.2 The Number Type
#### 5.6.3 The String Type

### 5.7 Singleton Built-in Objects
#### 5.7.1 The Global Object
#### 5.7.2 The Math Object


## Chapter 6 Object-Oriented Programming

### 6.1 Understanding Objects
#### 6.1.1 Types of Properties
#### 6.1.2 Defining Multiple Properties
#### 6.1.3 Reading Property Attributes

### 6.2 Object Creation
#### 6.2.1 The Factory Pattern
#### 6.2.2 The Constructor Pattern
#### 6.2.3 The Prototype Pattern
#### 6.2.4 Combination Constructor/Prototype Pattern
#### 6.2.5 Dynamic Prototype Pattern
#### 6.2.6 Parasitic Constructor Pattern
#### 6.2.7 Durable Constructor Pattern

### 6.3 Inheritance
#### 6.3.1 Prototype Chaining
#### 6.3.2 Constructor Stealing
#### 6.3.3 Combination Inheritance
#### 6.3.4 Prototypal Inheritance
#### 6.3.5 Parasitic Inheritance
#### 6.3.6 Parasitic Combination Inheritance


## Chapter 7 Function Expressions

### 7.1 Recursion

### 7.2 Closures
#### 7.2.1 Closures and Variables
#### 7.2.2 The this Object
#### 7.2.3 Memory Leaks

### 7.3 Mimicking Block Scope

### 7.4 Private Variables
#### 7.4.1 Static Private Variables
#### 7.4.2 The Module Pattern
#### 7.4.3 The Module-Augmentation Pattern


## Chapter 8 The Browser Object Model

### 8.1 The Window Object
#### 8.1.1 The Global Scope
#### 8.1.2 Window Relationships and Frames
#### 8.1.3 Window Position
#### 8.1.4 Window Size
#### 8.1.5 Navigating and Opening Windows
#### 8.1.6 Intervals and Timeouts
#### 8.1.7 System Dialogs

### 8.2 The Location Object
#### 8.2.1 Query String Arguments
#### 8.2.2 Manipulating the Location

### 8.3 The Navigator Object
#### 8.3.1 Detecting Plug-ins
#### 8.3.2 Registering Handles

### 8.4 The screen Object

### 8.5 The history Object

## Chapter 9 Client Detection

### 9.1 Capability Detection
#### 9.1.1 Safer Capability Detection
#### 9.1.2 Capability Detection Is Not Browser Detection

### 9.2 Quirks Detection

### 9.3 User-Agent Detection
#### 9.3.1 History
#### 9.3.2 Working with User-Agent Detection
#### 9.3.3 The Complete Script
#### 9.3.4 Usage


## Chapter 10 The Document Object Model

### 10.1 Hierarchy of Nodes
#### 10.1.1 The Node Type
#### 10.1.2 The Document Type
#### 10.1.3 The Element Type
#### 10.1.4 The Text Type
#### 10.1.5 The Comment Type
#### 10.1.6 The CDATASection Type
#### 10.1.7 The DocumentType Type
#### 10.1.8 The DocumentFragment Type
#### 10.1.9 The Attr Type

### 10.2 Working with the DOM
#### 10.2.1 Dynamic Script
#### 10.2.2 Dynamic Styles
#### 10.2.3 Manipulating Tables
#### 10.2.4 Using NodeLists


## Chapter 11 DOM Extensions

### 11.1 Selectors API
#### 11.1.1 The querySelector() Method
#### 11.1.2 The querySelectorAll() Method
#### 11.1.3 The matchSelector() Method

### 11.2 Element Traversal

### 11.3 HTML5
#### 11.3.1 Class-Related Additions
#### 11.3.2 Focus Management
#### 11.3.3 Changes to HTMLDocument
#### 11.3.4 Character Set Properties
#### 11.3.5 Customer Data Attributes
#### 11.3.6 Markup Insertion
#### 11.3.7 The scrollIntoView() Method

### 11.4 Proprietary Extensions
#### 11.4.1 Document Mode
#### 11.4.2 The children Property
#### 11.4.3 The contains() Method
#### 11.4.5 Scrolling


## Chapter 12 DOM Level 2 and 3

### 12.1 DOM Changes
#### 12.1.1 XML Namespaces
#### 12.1.2 Other Changes

### 12.2 Styles
#### 12.2.1 Accessing Element Styles
#### 12.2.2 Working with Style Sheets
#### 12.2.3 Element Dimensions

### 12.3 Traversals
#### 12.3.1 NodeIterator
#### 12.3.2 TreeWalker

### 12.4 Ranges
#### 12.4.1 Ranges in the DOM
#### 12.4.2 Ranges in Internet Explorer 8 and Earlier


## Chapter 13 Events

### 13.1 Event Flow
#### 13.1.1 Event Bubbling
#### 13.1.2 Event capturing
#### 13.1.3 DOM Event Flow

### 13.2 Event Handlers
#### 13.2.1 HTML Event Handlers
#### 13.2.2 DOM Level 0 Event Handlers
#### 13.2.3 DOM Level 2 Event Handlers
#### 13.2.4 Internet Explorer Event Handlers
#### 13.2.5 Cross-Browser Event Handlers

### 13.3 The Event Object
#### 13.3.1 The DOM Event Object
#### 13.3.2 The Internet Explorer Event Object
#### 13.3.3 Cross-Browser Event Object

### 13.4 Event Types
#### 13.4.1 UI Events
#### 13.4.2 Focus Events
#### 13.4.3 Mouse and Wheel Events
#### 13.4.4 Keyboard and Text Events
#### 13.4.5 Composition Events
#### 13.4.6 Mutation Events
#### 13.4.7 HTML5 Events
#### 13.4.8 Device Events
#### 13.4.9 Touch and Gesture Events

### 13.5 Memory and Performance
#### Event Delegation
#### Removing Event Handlers

### 13.6 Simulating Events
#### DOM Event Simulation
#### Internet Explorer Event Simulation


## Chapter 14 Scripting Forms

### 14.1 Form Basics
#### 14.1.1 Submitting Forms
#### 14.1.2 Resetting Forms
#### 14.1.3 Form Fields

### 14.2 Scripting Text Boxes
#### 14.2.1 Text Selection
#### 14.2.2 Input Filtering
#### 14.2.3 Automatic Tab Forward
#### 14.2.4 HTML5 Constraint Validation API

### 14.3 Scripting Select Boxes
#### 14.3.1 Options Selection
#### 14.3.2 Adding Options
#### 14.3.3 Removing Options
#### 14.3.4 Moving and Reordering Options

### 14.4 Form Serialization

### 14.5 Rich Text Editing
#### 14.5.1 Using contenteditable
#### 14.5.2 Interacting with Rich Text
#### 14.5.3 Rich Text Selections
#### 14.5.4 Rich Text in Forms


## Chapter 15 Graphics With Canvas

### 15.1 Basic Usage

### 15.2 The 2D Context
#### 15.2.1 Fills and Strokes
#### 15.2.2 Drawing Rectangles
#### 15.2.3 Drawing Paths
#### 15.2.4 Drawing Text
#### 15.2.5 Transformations
#### 15.2.6 Drawing Images
#### 15.2.7 Shadows
#### 15.2.8 Gradients
#### 15.2.9 Patterns
#### 15.2.10 Working with Image Data
#### 15.2.11 Compositing

### 15.3 WebGL
#### 15.3.1 Typed Arrays
#### 15.3.2 The WebGL Context
#### 15.3.3 Support


## Chapter 16 HTML5 Scripting

### 16.1 Cross-Document Messaging

### 16.2 Native Drag and Drop
#### 16.2.1 Drag-and-Drop Events
#### 16.2.2 Custom Drop Targets
#### 16.2.3 The dataTransfer Object
#### 16.2.4 DropEffect and effectAllowed
#### 16.2.5 Draggability
#### 16.2.6 Additional Members

### 16.3 Media Elements
#### 16.3.1 Properties
#### 16.3.2 Events
#### 16.3.3 Custom Media Players
#### 16.3.4 Codec Support Detection
#### 16.3.5 The Audio Type

### 16.4 History State Management

## Chapter 17 Error Handling and Debugging

### 17.1 Browser Error Reporting
#### 17.1.1 Internet Explorer
#### 17.1.2 Firefox
#### 17.1.3 Safari
#### 17.1.4 Opera
#### 17.1.5 Chrome

### 17.2 Error Handling
#### 17.2.1 The try-catch Statement
#### 17.2.2 Throwing Errors
#### 17.2.3 The error Event
#### 17.2.4 Error-handling Strategies
#### 17.2.5 Identify Where Errors Might Occur
#### 17.2.6 Distinguishing between Fatal and Nonfatal Errors
#### 17.2.7 Log Errors to the Server

### 17.3 Debugging Techniques
#### 17.3.1 Logging Messages to a Console
#### 17.3.2 Logging Messages to the Page
#### 17.3.3 Throwing Errors

### 17.4 Common Internet Explorer Errors
#### 17.4.1 Operation Aborted
#### 17.4.2 Invalid Character
#### 17.4.3 Member Not Found
#### 17.4.4 Unknown Runtime Error
#### 17.4.5 Syntax Error
#### 17.4.6 Syntax Error
#### 17.4.7 The System Cannot Locate the Resource Specified


## Chapter 18 XML in JavaScript

### 18.1 XML DOM Support in Browsers
#### 18.1.1 DOM Level 2 Core
#### 18.1.2 The DOMParser Type
#### 18.1.3 The XMLSerializer Type
#### 18.1.4 XML in Internet Explorer 8 and Earlier
#### 18.1.5 Cross-Browser XML Processing

### 18.2 XPath Support in Browsers
#### 18.2.1 DOM Level 3 XPath
#### 18.2.2 XPath in Internet Explorer
#### 18.2.3 Cross-Browser XPath

### 18.3 XSLT Support in Browsers
#### 18.3.1 XSLT in Internet Explorer
#### 18.3.2 The XSLTProcessor Type
#### 18.3.3 Cross-Browser XSLT


## Chapter 19 ECMAScript For XML

### 19.1 E4X Types
#### 19.1.1 The XML Type
#### 19.1.2 The XMLList Type
#### 19.1.3 The Namespace Type
#### 19.1.4 The QName Type

### 19.2 General Usage
#### 19.2.1 Accessing Attributes
#### 19.2.2 Other Node Type
#### 19.2.3 Querying
#### 19.2.4 XML Construction and Manipulation
#### 19.2.5 Parsing and Serialization Options
#### 19.2.6 Namespaces

### 19.3 Other Changes

### 19.4 Enabling Full E4X


## Chapter 20 JSON

### 20.1 Syntax
#### 20.1.1 Simple Values
#### 20.1.2 Objects
#### 20.1.3 Arrays

### 20.2 Parsing and Serialization
#### 20.2.1 The JSON Object
#### 20.2.2 Serialization Options
#### 20.2.3 Parsing Options


## Chapter 21 AJAX and COMET

### 21.1 The XMLHttpRequest Object
#### 21.1.1 XHR Usage
#### 21.1.2 HTTP Headers
#### 21.1.3 GET Requests
#### 21.1.4 POST Requests

### 21.2 XMLHttpRequest Level 2
#### The FormData Type
#### Timeouts
#### The overrideMimeType() Method

### 21.3 Progress Events
#### The load Event
#### The Progress Event

### 21.4 Cross-Origin Resource Sharing
#### 21.4.1 CORS in Internet Explorer
#### 21.4.2 CORS in other Browsers
#### 21.4.3 Preflighted Requests
#### 21.4.4 Credentialed Requests
#### 21.4.5 Cross-Browser CORS

### 21.5 Alternate Cross-Domain Techniques
#### 21.5.1 Image Pings
#### 21.5.2 Comet
#### 21.5.3 Server-Sent Event
#### 21.5.4 Web Sockets
#### 21.5.5 SSE versus Web Sockets

### 21.6 Security


## Chapter 22 Advanced Techniques

### 22.1 Advanced Functions
#### 22.1.1 Safe Type Detection
#### 22.1.2 Scope-Safe Constructors
#### 22.1.3 Lazy Loading Functions
#### 22.1.4 Function Binding
#### 22.1.5 Function Currying

### 22.2 Tamper-Proof Objects
#### 22.2.1 Nonextensible Objects
#### 22.2.2 Sealed Objects
#### 22.2.3 Frozen Objects

### 22.3 Advanced Timers
#### 22.3.1 Repeating Timers
#### 22.3.2 Yielding Processes
#### 22.3.3 Function Throttling

### 22.4 Custom Events

### 22.5 Drag and Drop
#### 22.5.1 Fixing Drag Functionality
#### 22.5.2 Adding Custom Events


## Chapter 23 Offline Applications and Client-side Storage

### 23.1 Offline Detection

### 23.2 Application Cache

### 23.3 Data Storage
#### 23.3.1 Cookies
#### 23.3.2 Internet Explorer User Data
#### 23.3.3 IndexedDB


## Chapter 24 Best Practices

### 24.1 Maintainability
#### 24.1.1 What is Maintainable Code?
#### 24.1.2 Code Conventions
#### 24.1.3 Loose Coupling
#### 24.1.4 Programming Practices

### 24.2 Performance
#### 24.2.1 Be Scope-Aware
#### 24.2.2 Choose the Right Approach
#### 24.2.3 Minimize Statement Count
#### 24.2.4 Optimize DOM Interactions

### 24.3 Deployment
#### 24.3.1 Build Process
#### 24.3.2 Validation
#### 24.3.3 Compression


## Chapter 25 Emerging APIs

### 25.1 RequestAnimationFrame()
#### 25.1.1 Early Animation Loops
#### 25.1.2 Problems with Intervals
#### 25.1.3 mozRequestAnimationFrame
#### 25.1.4 webkitRequestAnimationFrame and msRequestAnimationFrame

### 25.2 Page Visibility API

### 25.3 Geolocation API

### 25.4 File API
#### 25.4.1 The FileReader Type
#### 25.4.2 Partial Reads
#### 25.4.3 Object URLs
#### 25.4.4 Drag-and-Drop File Reading
#### 25.4.5 File Upload with XHR

### 25.5 Web Timing

### 25.6 Web Workers
#### 25.6.1 Using a Worker
#### 25.6.2 Worker Global Scope
#### 25.6.3 Including Other Scripts
#### 25.6.4 The Future of Web Workers
