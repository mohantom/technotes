Javascript best practice
---------------------------
Course: JavaScript best practices
Syntax
Semicolon
Restricted production: continue, break, return, throw…
 
; is auto-inserted -> return;
Return {
	Hi: ‘hello’
};
Use semicolons with JSHint (or ESLint) to prevent potential issues.

Linting
JSLint: first one, 2002 Douglas Crockford, not very configurable
JSHint: fork of JSLint, much more configurable, built in package support, not extensible
ESLint: custom rules support, lots of configuration
JSHint.com
	Gulp with JShint
	Npm install -g jshint
Curly braces
Put the curly braces at the same line
Function service() {
}
Equality
If variables are too different type, they are converted to be the same!
Use triple equals
Var x = 1, y = ‘1’
If(x == y) // true!
If(x === y) // false, no type conversion

Var x;
If(x) // check if x exists, same as if(x == true), does not work if x = 0;
If(typeof x !== ‘undefined’)  // this is better!

Variables
Hoisting: js default behavior of moving all declarations to the top of the current scope.
 
Only “var” is moved to top, myVariable is undefined.
Best practice: all var declarations go to the top of the scope. No need to assign values.

Functions
First class object (same as other object: int…), can assign function to a variable
 
Expression(); // exception
Q: difference of named function and function assigned to variable?
Best practice: define variable and functions at top.

Behaviors
Global variables
 
Print() is before the console.log(stringToPrint), otherwise it blows.
Strict mode
‘use strict’;
Can be put inside a function
Read only properties
 
It does not blow up.
But ‘use strict’ will throw exception.
Deleting stuff
 
Does not blow up. Unless ‘use strict’.
Delete only works when deleting something from an object. It doesn’t delete variables.
Dupes, duplicates
Function x(a, b, a) {
	Console.log(a);
}
Error in ‘use strict’
Octals and hexidecimals
Var x = 120;
Y = 012; // octal, == 10
Z = 0x12; // 18
‘use strict’
Y = parseInt(12, 8);  // convert ‘012’ to integer, 10
With
 
‘use strict’ does not allow ‘with’!
Better way:
(function(newVar) {
	Console.log(newVar);
](obj.a.b.c))

This
Var obj = {
	Val: ‘Hi there’,
	printVal: function() {
		console.log(this.val);
	}
};
 
Var print = obj.printVal;
Print(); // same as window.print(), but no val in window!
Obj2.printVal = obj.printVal;
Obj2.printVal(); // this is obj2
This in new objects
 
Greeter.greet();
Greeter.delayedGreeting();
setTimeout(this.greet, 1000); // same as window.setTimeout(); does not work!
setTimeout(this.greet.bind(this), 1000); // works too
‘_this’ is a copy of ‘this’. In Angular, ‘var ctrl = this’.

Async patterns
Callbacks
Avoid Christmas tree code, use named function 
In node.js, function findUser(err, results)
If(err) {
	Return done(err, null); // use return to finish
}

Promises
 
Promisejs.org
Return new Promise(function(fulfill, reject) {
	setTimeout(function() {
		console.log(message);
		fulfill(); }, 500)
	});

 
Return a promise for each function:
 

ES6 and Babel
$ npm install –save-dev babel-preset-es2015
$ babel app.js -o es6.js // convert to es5
Async – await (ES7)
 
.babelrc
{
	“presets” : [
	“stage-3”
	],
	“plugins”:[]
}

Production code
$ Npm init // create package.json file
“engines”: {
	“node”: “<4.2.1” // your code only works for version less than 4.2.1
}
$ npm install code
$ npm install express –save
“dependencies” : {
	“express”: “^4.13.4”  // close to this version
}
$ npm config set save=true  // auto save for –save
$ npm config set save-exact=true // remove “^”

Environment
Console.log(‘Express listening on port: ‘ + process.env.PORT);
$ npm install -g foreman
In package.json
“scripts”: {
	“test”: “echo \”Error: no test specified\” and exit 1“,
	“start”: “node app.js” // 
$ nf start // set default port, etc
File .env
	{
		“port”: 9000,
		“connection”: {
			“sql”:””,
			“mongo”:””
		}
	}
Cross platform
In Win and Mac: filename is NOT case sensitive/myObject
Best practice: all use lower case, my-object.js

Simplify your world
 
Bets practices
Kiss principal: keep things simple and stupid

