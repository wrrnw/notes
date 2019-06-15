# Reading Notes for Book \<Professional JavaScript for Web Developers\>

## Chapter 1 What is JavaScript

### 1.1 A Short History

### 1.2 JavaScript Implementation

### 1.3 JavaScript Versions



## Chapter 2 JavaScript in HTML



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
#### 3.1.6 Keywords and Reserved words
#### 3.1.7 Variables
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

### 3.2 Data Types
- There are five simple data types (also called primitive types) in ECMAScript: Undefined, Null, Boolean, Number, and String. There is also one complex data type called Object, which is an unordered list of name-value pairs. Any values can be represented as one of six.

#### 3.2.1 The typeof Operator
- The *typeof* operator is used to determine the data type of a given variable
	- "undefined" if the value is undefined
	- "boolean" if the value is Boolean
	- "string" if the value is string
	- "number" if the value is number
	- "object" if the value is an object (other than a function) or *null*
	- "function" if the value is a function
- Note that because *typeof* is an operator and not a function, no parentheses are required (although they can be used)
- Calling *typeof null* returns a value of "*object*", as the special value *null* is considered to be an empty object reference
#### 3.2.2 The Undefined Type
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

#### 3.2.3 The Null Type
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
#### 3.2.4 The Boolean Type
- The Boolean type has only two literal values: *true* and *false*. These values are distinct from numeric values, so *true* is not equal to 1, and *false* not equal to 0.
- To convert a value into its Boolean equivalent, the special *Boolean()* casting function is called
``` javascript
var message = "Hello world!"
var messageAsBoolean = Boolean(message);
```

#### 3.2.5 The Number Type



### 3.3 Working with flow-control statements




### 3.4 Understanding functions




## Chapter 4 Variables, Scope, and Memory

## Chapter 5 Reference Types

## Chapter 6 Object-Oriented Programming

## Chapter 7 Function Expressions

## Chapter 8 The Browser Object Model

## Chapter 9 Client Detection

## Chapter 10 The Document Object Model

## Chapter 11 DOM Extensions

## Chapter 12 DOM Level 2 and 3

## Chapter 13 Events

## Chapter 14 Scripting Forms

## Chapter 15 Graphics With Canvas

## Chapter 16 HTML5 Scripting

## Chapter 17 Error Handling and Debugging

## Chapter 18 XML in JavaScript

## Chapter 19 ECMAScript For XML

## Chapter 20 JSON

## Chapter 21 AJAX and COMET

## Chapter 22 Advanced Techniques

## Chapter 23 Offline Applications and Client-side Storage

## Chapter 24 Best Practices

## Chapter 25 Emerging APIs
