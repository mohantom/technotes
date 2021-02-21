Javascript
------------

## Prototype


## Closure
a function contains or return another function which has access to outer variable
so outer variable live longer

```shell
// javascript
function outer(var1) {
  return function inner(var2) {
    console.log("outer variable: " + var1);
    console.log("inner variable: " + var2);
  }
}

outer("test");
```

```shell
// IIF
var counter = (function() {
  var privateCounter = 0;
  // private function
  function changeBy(val) {
    privateCounter += val;
  }
  
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  }
})();

console.log(counter.value()); // 0
counter.increment();
counter.increment();
console.log(counter.value()); // 2
counter.decrement();
console.log(counter.value()); // 1
```


## Currying
take the argument one at a time
```shell
// regular function
var add = (a, b) => a + b;

// currying
var addCurry = a => b => a + b;


add(1, 2); // 3
addCurry(1)(2); // 3
```


## Memoize
dynamic programming, cache values
```shell
// regular function
function fib(n) {
  if (n <= 2) {
    return 1;
  }
  
  return fib(n - 1) + fib(n - 2);
}

// with memoize to save previous calculated values in prevValues
function fib(n, prevValues = []) {
  if (prevValues[n] != null) {
    return prevValues[n];
  }
  
  let result;
    if (n <= 2) {
    result = 1;
  }
  
  result = fib(n - 1) + fib(n - 2);
  prevValues[n] = result;
  return result;
}

fib(500)
```


## Mixins
introduce methods to a class without inheritance; safe form of multiple inheritance


Course: Rapid JavaScript Training
Introduction
Online editor/parser: Jsfiddle.net, plnkr.co
JS basics
<script type="text/javascript" src="js/app.js">
console.log('Hello!');	// not executed if there is “src” !
</script>
Primitive types: Number, string, Boolean, undefined, object (array, null is also an object), function.
typeof 

// this works! two passes: first pass scan global variable
printOrder(‘9002’);
function printOrder(orderId) {	// prints fine
console.log(‘Printing order: ’ + orderId);
};
Var printOrder = function() {}	// printOrder is not a function

varlineItem= {
product: 'Widget 1',
quantity: 4,
price: 9.50
};
for(varfield in lineItem)
console.log(field + " : " + lineItem[field]); 

identifier must start with a letter, $ or _

variables, types and scope
hoisting, primitive types, undefined, null
two passes: all declarations are located and identifiers are known by the compiler -> execution
console.log(productId);  // undefined, no error
var productId= '9000';  
var total = price * quantity; // NaN
Always define function before use it to avoid issues.
Var oct = 062; // not allowed in strict mode
Number.MAX_VALUE //1.79769e+308
Number.MAX_VALUE * 2 // Infinity, -Infinity
Typeof Infinity 	// Number
Typeof NaN // Number, isNaN(aa)
‘hardware’.length // not length()
True // should be “true”!
Console.log(Boolean(‘’)) // false, 0, undefined, null
	Console.log(Boolean(‘ ‘) // true, space
Var value = 99.99; Console.log(typeof !!value);	// Boolean
Console.log(undefined == null) // true!  Types are different.

Only one global scope: window	// == this, for Node.js, it’s “global”
Var productId = 8; console.log(window.productId);  // 8
Gloable scope, function scope, block scope (in try catch)
Operators
Console.log(2000 + undefined); // NaN
Console.log(“prd” + undefined); // prdundefined
Console.log(2000 + null); // 2000
Console.log(“prd” + null); // prdnull
Console.log(3.2-2.0); // 1.2000000000000002. a.toFixed(2)
Console.log(“300” – “100”); 
300 – undefined // NaN
200 – null // 200

varobj={ valueOf:function(){return100; } };
vartotal=300-obj;
console.log(total);	// 200!
300 – “” // 300
9 % “   4   “ // 1
Var level; console.log(++level); // NaN
+'calc' // NaN
Var num1 = -parseInt(‘1000’, 2); num1 >>> 1; // 11111111… 00, carry sign
!”” // true
!new Object(); //false

Var obj={ calc : 'LogicalAND' };
var value=obj&&99;
console.log(value);	// 99! If the first is true, return the 2nd
console.log( null && 2); // null
Var val = obj && obj; // obj { … }
Var value = obj || 99; // obj {…}

true == 1 // true
true == 2 // false, true is converted to 1
42 == ‘42’ // true, ‘42’ is converted to number 42

Var obj={name:'Trigger'};
Var obj2={name:'Trigger'};
Obj == obj2 // false

Null == undefined // true
Undefined == 0 // false, normally compare with undefined will get false
Null == 0 // false
NaN == NaN // false
‘42’ < 50 // true
‘42’ < ‘142’ // false

Var total  = (99, 88, 44); // not an array
Console.log(total); // 44, the last value. DO NOT USE IT!

Arrays and references types
Object, array, date, regExp, function, primitive wrappers
Array
Entry instanceof Array
Var entries = New Array(‘trains’, ‘plains’);
Array(‘trains’, ‘plains’);
[‘trains’, ‘plains’]
entries[3] // undefined
entries.length //2
entries[10] = ‘cars’; // array is expanded to 11 length
entries.toString() // comma separated
entries.valueOf() // [‘trains’, ‘plains’]
entries.join(‘|’) // trains|plain
entries.push(‘one’, ‘more’);
entries.pop() // ‘more’, length is decreased by 1!
Entries.shift() // ‘train’, first element is out, length – 1
Entries.unshift(‘bus’) // push one element to the first one, length + 1, return the new length
Var newEntries = entires.concat([‘ship’, ‘plane’]);  // entries is unchanged
var newEntries = entries.slice(2); // take from index 2. Does not change entries
entries.slice(1,3); // take element 1 and 2
entries.slice(-2); // take the last two elements
entries.splice(1, 2); // from element index 1 (including), remove 2 elements; array is modified
entries.splice(2, 0, 99, 100); // insert 99, 100 at index 2
entries.reverse()
entries.sort() // 1, 10, 2, 3, 4, sorted by string values!!
entries.sort(function(val1, val2) { return val1 – val2; }); // use Lodash!
	Entries.indexOf(3); entries.indexOf(‘3’) // -1
	Entries.lastIndexOf(1);

Date
Var dt = new Date(0); // 1/1/1970
Date.UTC(2000, 0); // time from 1/1/1970
Vard dt = Date.now();  // time from 1/1/1970
Console.log(dt.toDateString()); // Fri Sep 25 2015

## RegEx
Var pattern = new RegExp(‘am’, ‘g’); // g means global
Var pattern = /am/g; pattern instanceof RegExp; // true
Pattern.test(“Sam I am”); // true for 1st time
Pattern.test(“Sam I am”); // true for 2nd time
Pattern.test(“Sam I am”); // false for the 3rd time
Pattern.exec(“Sam I am”); // [“a”, index: 1, input: “Sam I am”], return index
Pattern.match(“Sam I am”); // “am”, case sensitive, /gi -> case insensitive
Var pattern = /[aA]m/g; // a or A

RegExp 使用方式1
 var userPattern = new RegExp("^[a-zA-Z0-9\u4e00-9fa5]${5,8}"); //字母，数字，汉字
 var flag = userPattern.test(username);

RegExp 使用方式2
  var userPattern = /^[a-zA-Z0-9\u4e00-9fa5]${5,8}/; // 直接量
密码框：根本无法输入中文，可以不管
var pswPatter = /^[\w]{6,12}%/;
 
if (document.getElementsByName("gender")[i].checked == true);
if (car.length!=15 && car.length!=18)  //不是短路的！
var idPattern = /^[0-9]{17}[0-9x]{?}$/;  //18位身份证号码


Objects, JSON, and Prototypes
Prototypes: inheritance
Every JS object has prototype property, but we don’t always have access to it.
Property property is simply an object.
Var project = {};  project.someFunc();
Js will look for someFunc() in this order:
	Project.someFunc() -> project.prototype.someFunc() -> project.prototype.prototype.someFunc() ->… … until prototype is undefined
Prototypes
ES6 can access prototype: __proto__

Var project  = { name: ‘Phoenix’ };
Console.log(project.toString()); // [object, object]
Console.log(project.prototype); // undefined, can access it
Console.log(typeof project.__proto__); // object, DO NOT put in prod

Global constructor: Object.prototype
Console.log(typeof Object.prototype); // object
Console.log(project.__proto__ == Object); // false, Object is the constructor function
Console.log(project.__proto__ === Object.prototype); // true

Set up and control own protoypes: Object.create(obj); // obj is prototype passed in
Var project = { securityLevel: 2};
Var secretProject = Object.create(project); // secretProject.securityLevel == 2
Console.log(project.__proto__.__proto__ === Object.prototype); // true

Var task = { };
Object.defineProperty(task, ‘text’, {
value: ‘Get this job done!’,
writable: true, // default is read only
enumerable: true, // default is false
configurable: false // default is true
}); //; task.text = ‘’
Oject.getOwnPropertyDescriptor(task, ‘text’);

Project.hasOwnProperty(‘text’); // true
Object.prototype.isPrototypeOf(project); // true
Console.log(‘securityLevel’ in project); // true
Console.log(‘toString’ in securityProject); // true

Functions
Typeof Object // function
var Employee = function(name,boss){
this.name=name;
this.boss=boss;};
var newEmployee = new Employee('JJ','JDHogg');
console.log(newEmployee.boss);

Constructor
var Employee=function(name, salary){
	this.name = name;
	this.salary = salary;
	this.giveRaise = function(){};
};
var e1=newEmployee('JJ');
var e2=newEmployee('JV');
console.log(e1.giveRaise === e2.giveRaise);  // false. DO NOT add function in constructor!! Add in prototype
Employee.prototype.giveRaise = function(raise){
	This.salary += raise;
}; 
console.log(Employee.prototye); // object, we can access prototype in constructor, not in object

This
Typeof this // object
This === window // in browser
 

Call() and apply()
Control what ‘this’
varupdateZipCode=function(newZip, country){
	console.log(this);};
updateZipCode.call({zip:'11787'});  // object {zip:'11787'}, pass in ‘this’
updateZipCode.call(zipCode,'11888','us'); // comma separated
updateZipCode.apply(zipCode,['11888','us']);	// array

Closures
Keep the context in place in a function; can access field in parent function
 
// 70000, currentSalary is persisted
Event handler, setInterval function

IIFEs
Immediately invoked function expressions
Keep variables out of global scope
(function(){ console.log('Executed!'); })();
(function(){console.log('Executed!');}()); // same 

Var app={};  // global variable
(function(ns){ns.name='None';})(app);
console.log(app.name);
 
// make sure $ is jQuery
 
// same as (), no ‘+’ will not work

Recursion
 
If fn is anonymous function, fn(topEmployee.subordinates[i]) will throw error.

BOM and DOM
Browser object model, document object model
Window, system dialog, location, document, query selectors
console.log(window.screenLeft+','+window.screenTop);
console.log(window.innerWidth+','+window.outerWidth);
window.open('http://www.pluralsight.com','_blank');

console.log(newDate().getSeconds());
var id=setTimeout(function(){console.log(newDate().getSeconds());},1000);
clearTimeout(id);

setInterval(), clearInterval(id)

alert(‘hello world’)

if(confirm('DeleteEVERYTHING?!')){
	console.log('Youaskedforit!')
} else{console.log('Maybenexttime...');}

Var result = prompt('Yourname?');

Location.href, location.host, location.port, location.protocol
location.assign('http://www.pluralsight.com'); // may not execute in some browser

var element = document.getElementById('article1');
var elements = document.getElementsByTagName('p');

query selector
var element = document.querySelector('article'); // return the first match; or use '#article1', ‘.special’
var elements = document.querySelectorAll('.special'); // return an array

Event Handlers
Window events: Load, unload, abort, error, select, resize, scroll
Mouse: click, dblclick, mousedown, mouseenter, mouseleave, mousemove, moseout, mouseover, mouseup, mousewheel
Keyboard: keydown, keypress, keyp, textinput
Focus: blur, focus, focusin, focusout
HTML5: contextmenu, beforeunload
Touch: touchstart, touchmove, touchend, touchcancel

Event object properties
Bubbles, cancelable, currentTarget, defaultPrevented, detail, eventPhase, preventDefault(), stopImmedatePropgation(), stopPropagation(), target, trusted, type
// body of HTML
<input id="submit1" type="button" onclick="submitForm(this, event)"/>
// JavaScript file
function submitForm(element, event) {console.log(event.type);}
// “this” is “input”, event is “click”

Event listener
We can add multiple listeners!
var button = document.getElementById('submit1');
button.addEventListener('click',function(){console.log('ButtonClicked');});
button.removeEventListener('click',submitHandler);

Event bubbling
div2.addEventListener('click',clickHandler,true); // parent is called first
varclickHandler=functiondivClickHandler(event) {
	console.log(this.id);
	event.stopPropagation();
event.preventDefault(); // eg, click, form submission
};

Built-in Objects and Functions
parseInt(‘1234’); //1234
parseInt(‘b123’); // NaN
parseInt(‘12z23’); // 12
parseInt(‘1234.9’); //1234, no rounding
parseInt(‘C000’, 16); // 49152
parseFloat(‘123.9’) //123.9
parseFloat(123e-1’) //12.3
isFinite(Number.POSITIVE_INFINITY) // false
isNaN(NaN) // true
isNaN(9/0) // false, should be inifinity
encodeURI(“\\start\\”); // %5Cstart%5C
encodeURI(“\\start\\+”); // %5Cstart%5C+, “+” is not encoded
encodeURIComponent(“\\start\\+”); // %5Cstart%5C%2B
decodeURI(“%5Cstart%5C”) // \start\+
avoid eval()

Math.PI, abs(), ceil(), floor(), trunc(42.12)//42, sqrt(-81)//NaN
Math.max(-12, 0, 12, “88”) // 88
Math.pow(2, 3) // 8
Math.random() // a random value

‘my string’.charAt(3)
‘my string’.concat(‘ lives!’)
‘my value’.includes(‘ ‘) // true
endsWith(), startsWith, indexOf(), lastIndexOf()
‘some string’.slice(5) // string, same as substring()
‘string’.slice(-3) // ing
Substr(5, 6) // starting index, length of letters
Substring(5, 6) // starting index, ending index (excluding)

varvalidateValues=function(){
	console.log(arguments[0]);};
validateValues(1,true,'Settings');


Other topics
Error handling: 
	Normally not by try-catch-finally, but with promises

Can’t delete variable in strict mode; can’t include ‘with’.

Modules
AMD: asynchronous module definition, browser side
CommonJS: from node.js, server
ES6, SystemJS




Javascript basics
---------------------

<script language="javascript/php/c#/vbscript" src="">
无var声明的是全局变量
因为会一层一层往上找，直到顶层全局。
6中数据类型：String, Number, Boolean, Undefined, Null, object
 
==: 判断值是否相等
===: 判断值相等，类型也相同。
5 == "5"; 5 !== "5";
 
For, while, do...while, for...in
 
Var n = Math.round(Math.random()*500);
Var num = prompt('Please input a number 0~500);
If (num > n) alert('too big');
 
函数
Funciton myFunction(args) { …. Return xxx; }
一般pass by value; 但是object是pass by reference!!
 
函数名就是函数的首地址。
 
Var I = function myFunction(args) { … return xxx; }
Var I = function(args) { … return xxx;}
 
自调用匿名函数
(function(){})();
(function(first){
Jquery = xxx;
alert('hello.js' + first);
window.$=jquery; //外部$指向局部变量。
})(10);
第一个括号把匿名函数括起来表示一个整体，只有首地址；后面括号表示自动执行一次。防止重名，且只会执行一次，用于初始化。
 
变量作用域
 
 
 
形参 arguments
如果参数不确定，可以通过arguments来保存所有实参。
function display() {
    for( var i=0; i<arguments.length; i++){
        document.write(arguments[i]+'<br/>');
}
display('test1', 'test2', 'test3');
 
数组
数组的数据类型实际就是对象
 
//文本下标数组
Var arr = [1, 2, 3];
Arr['first'] = 'zhangsan';
Arr['second'='lisi';
arr.length == 3; !! //文本下标元素不计入数组长度，文本下标元素以属性加入数组！文本下标必须用for … in 进行遍历！
For( var I in arr) {
Document.write(i+':'+arr[i]+'<br>'); } //不能用arr.i!!
 
添加 .push(), .unshift(), .splice
删除 .pop, .shift(), .splice(index, how-many)
截取合并 .slice(start [,end]), .concat(), .split()
连接 .join()
 
事件编程
<div onclick="alert('hello');alert('hello2')">
//行内绑定
 
行内绑定 vs 动态绑定
//行内绑定
Function test() {
This.style.color='red'; } //this 是window
<div id='div1' onclick="test()"> javascript </div> // 不work
 
<div onclick="window.test()">javascript</div> //也不行
 
//动态绑定，加这个就可以了
Window.onload=funciton(){
Document.getElementById('div1').onclick=test; }
 
事件监听
同一个对象的多个事件，后面的灰覆盖前面的；如同 var I = 2; var I = 3;
Document.getElementById('div1').onclick=test1; 
Document.getElementById('div1').onclick=test2; 
 
基于IE
如果要制定多个事件处理，可以使用时间监听。
attachEvent(type, callback), 但只能用于IE。
Type=onclick, onsubmit, onchange
Callback: 处理程序
Document.getElementById('div1').attachEvent('onclick', test1); //not test1();
 
基于w3c模型:
  addEventListener(type, callback [, capture])
Type: click, submit, change (没有"on")
Callback: 事件处理程序
Capture:事件模型。true捕捉，false冒泡(默认)
 
事件对象event
 
对象模型
 
 
BOM模型：浏览器对象模型
打开一个网页程序是，js会自动创建对象，browser对象 -> window对象
 
 
Window.event.cancelBubble = true; //IE
Function(event){event.stopPropgation(); } //w3c
 
window对象
Alert, confirm, prompt, open, close, blur, focus, print, moveBy(x,y), moveTo(x,y), resizeBy(x,y), resizeTo(x,y), scrollBy(x,y), scrollTo(x,y), setTimeout(), clearTimeout()
 
Navigator浏览器对象
appCodeName, appName浏览器名称, appVersion, platform, onLine, cookieEnabled
 
location地址栏对象
Host, port, href, pathname, protocol, search, assign(url)
 
Screen
availHeight        可用高度    
availWidth        可用宽度
colorDepth        颜色
height            高度
width            宽度
 
document对象（DOM）
linkColor        超链接颜色
alinkColor        作用中的超链接颜色
vlinkColor        作用后的超链接颜色
bgColor            背景颜色
fgColor            字体颜色
Title            文档标题
getElementById(“id”)
getElementsByName(“name”)
getElementsByTagName(“tagname”)
 
Var x = screen.width;
Var y = screen.height;
 
Location.href='demo19.html';
Locatin.assign=''; //和href一样，页面跳转。
 
Function display() { alert('hello'); }
 
Var timer = setTimeout('display()', 3000); 
clearTimeout(timer);
// 浏览器在执行时，向系统内存抛出一个定时器对象，没有停留，而是加载这行代码后立即去执行后面语句。
 
setInterval('display()', 3000) //每3秒执行一次。setInterval会反复执行，而setTimeout只执行一次。
 
系统类
String
Length, indexOf, substr, toLowerCase, toUpperCase, replace
Date
getYear, getFullYear, getMonth, getData, getDay, getHours, getMinutes, getSeconds, getMilliseconds
 
Math
Ceil, floor, min, max, pow, random, round, sqrt
 
 
类
function 类名(){}
 
在js中，没有类的定义语句，只有function，每一个function，我们可以认为它是同名类的构造函数
 
Function person -----> 它是Person类的构造函数
 
这种函数也叫构造器
 
 
 
在js中，对象属性是动态添加的，对象属性可以使用“.”或[‘’]这两种形式表示出来
 
对象的属性可以是任何数据类型，如：字符串、数字、对象
 
在js中，一切都是对象
 
var num = 10;        //Number
var str =‘hello’;    //String
var flag = true;        //Boolean
var per = new Person();
 
三个常用关键字：
 
constructor： 返回的是对象的构造器
typeof ：返回数据类型
instanceof ：判断对象是否是某个类的实例
 
创建p1对象时，会为p1开辟相应的堆空间，然后将name和age属性以及值添加到p1所指向的堆空间中，
创建p2对象时，也会为p2对象开辟对应的空间，但p2所指向的堆空间是空的，所以
P2对象没有name和age属性
 
This
我们的习惯：在相同的类下创建的对象需要有相同的属性和方法
 
函数是由对象调起来的，在函数中的this就指向了这个对象
 
在js中，如何判断一个函数是以面向过程调用还是以面向对象形式来调用？
 
所有函数都是面向对象调用，普通函数的调用是由window对象调用的
 
 
 
Timer = setTimeout('fn()', 1000); //每隔1秒执行一次
clearTimeout(timer);

