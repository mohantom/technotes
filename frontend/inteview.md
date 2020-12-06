

## Move and sort evens
```shell script
/*
  Write JavaScript/React code here and press Ctrl+Enter to execute.

  Try: mountNode.innerHTML = 'Hello World!';
   Or: ReactDOM.render(<h2>Hello React!</h2>, mountNode);
*/

'use strict';

/**
 * @param values {Array} An array of integers
 * @return an array of integers of the same length, with the odd
 *         values appearing first, in the same order as in the original
 *         array, and the even values at the end of the array, in ascending order.
 *
 * The function should not mutate the original array.
 *
 * See tests below for example input with expected output.
 */
ffunction moveAndSortEvens(values) {
 
   
   const oddVals = [];
   const evenVals = [];
   
   values.forEach(value => {
     const isEven = value % 2 === 0;
     
     if (isEven) {
       evenVals.push(value)
     } else {
       oddVals.push(value);
   });
   
   evenVals.sort((a,b) => {
     return a - b;
   });
   
   return [...oddVals, ...evenVals];
 }
 
 
 ///////////// Tests //////////////
 
 var expect = require('chai').expect;
 
 // It should produce a properly ordered array
 expect(moveAndSortEvens([1, 2, 3, 4, 5]))
   .to.eql([1, 3, 5, 2, 4]);
 
 expect(moveAndSortEvens([5, 4, 3, 2, 1, 0]))
   .to.eql([5, 3, 1, 0, 2, 4]);
 
 expect(moveAndSortEvens([4, 1, -9, 0, -2, 11, 3, 2, 8, -1]))
   .to.eql([1, -9, 11, 3, -1, -2, 0, 2, 4, 8]);
 
 expect(moveAndSortEvens([191, 180, 20, 19, 18, 1, 0]))
   .to.eql([191, 19, 1, 0, 18, 20, 180]);
 
 // It should not mutate the original array
 var original = [1, 2, 3];
 moveAndSortEvens(original);
 expect(original).to.eql([1, 2, 3]);
 
 
 console.log('======= All Tests Passed. =======');


```


## Squares
```shell script
'use strict';

const expect = require('chai').expect;

const nums = [ 7, 2, 11, 4, 9, 0, 1, 7, 14, 3 ];

// complete the statement so that
// squares contains each of the values in nums,
// squared.

const squares = nums.map(num => num * num);



expect(squares).to.deep.equal([ 49, 4, 121, 16, 81, 0, 1, 49, 196, 9 ]);

// complete the statement
// so that evenSquares contains only the
// members of squares that are even.

 const evenSquares = squares.filter(num => num % 2 === 0);

expect(evenSquares).to.deep.equal([ 4, 16, 0, 196 ]);

// complete the statement
// so that sumSquares contains 
// the sum of all squares

 const sumSquares = squares.reduce((accum, num) => accum += num);

expect(sumSquares).to.equal(526);


console.log('======= All Tests Passed. =======');

```

## Calculator
```shell script
// Calculator should take an initial value and allow chained add and subtract commands
// result contains the current calculated value.

class Calculator {
  constructor(initialValue) {
    this.value = initialValue;
  }
  // implement required functionality
  add(value) {
    this.value += value;
    return this;
  }
  subtract(value) {
    this.value -= value;
    return this;
  }
  
  get result() {
    return this.value
  }

}

const calc = new Calculator(0)
  .add(10)
  .subtract(3)
  .add(1);


//////////////// TESTS ////////////////

const actual = calc.result;
console.log('foobar', actual);

const expected = 8;

console.assert(actual===expected, actual + "===" + expected);


console.log('======= All Tests Run. =======');
```


## Test scope
```shell script
// comment this line to run after answering below

function testScope() {

  var y = 1;

  console.log(x); // undefined

  if (true) {
    var x = 2;
  }
  
  (function() {
    var z = 3;
    y = 4;
  })();
  
  console.log(x); // undefined
  console.log(y); // 4
  console.log(z);// undefi
}

testScope();

/*
what will this print when we run it?
enter your answers below as 'line #: result'

*/
```


## Timeout
```shell script
// comment this line to run after answering below

for (let i = 0; i < 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, 0);
}
console.log('hello');

/*
what will this print when we run it?
enter your answer below:

// hello
//5
//5
//5
//5
//5


*/
```


## Join words
```shell script
// change joinWords to support multiple calls
// see test for example usage

function joinWords(...args1) {
  return function (...args2) {
#    return args1.join(" ") + " " + args2.join(" ");
    return [...args1, ...args2].join(" ");
  }
  //return a + " " + b;
}

/// Tests
var expect = require("chai").expect;

let greet = joinWords("Hello");
expect(greet("World")).to.equal("Hello World");

greet = joinWords('Hey', 'there!');
expect(greet("Where", "is", "Foo", "Bar?")).to.equal("Hey there! Where is Foo Bar?")

// greet = joinWords("Hello ", "World", " ! ");
// expect(greet("Where", "are", " you ", "Foo", "Bar", "?")).to.equal(
//   "Hello World! Where are you Foo Bar?"
// );

console.log("======= All Tests Passed. =======");
```


## Async
```shell script
var expect = require('chai').expect;

async function getResult() {
  // Change this function to get the test to pass
  return await p1() * await p2();
}

// Code below should not be changed

getResult()
  .then(result => expect(result).to.eql(6))
  .then(() => console.log('All tests passed'))


function p1() {
  return delay(2)
}

function p2() {
  return delay(3);
}


function delay(x) {
  return new Promise(res => setTimeout(() => res(x), 1000))
}
```