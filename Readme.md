# Javascript Note
### Repeat a String
In the general case, this should be done using a correct polyfill for the ES6 String.prototype.repeat() method. Otherwise, the idiom new     Array(n +       1).join(myString) can repeat n times the string myString:
```
var myString = "abc"; var n = 3;
new Array(n + 1).join(myString); // Returns "abcabcabc"
```

## Arrays
### Converting Array-like Objects to Arrays
* JavaScript has "Array-like Objects", which are Object representations of Arrays with a length property. For example:
```
var realArray = ['a', 'b', 'c']; var arrayLike = {
  0: 'a',
  1: 'b',
  2: 'c',
  length: 3
};
```

Common examples of Array-like Objects are the arguments object in functions and HTMLCollection or NodeList objects returned from methods like document.getElementsByTagName or document.querySelectorAll.
However, one key difference between Arrays and Array-like Objects is that Array-like objects inherit from `Object.prototype` instead of `Array.prototype`. This means that Array-like Objects can't access common Array
prototype methods like forEach(), push(), map(), filter(), and slice():
```
var parent = document.getElementById('myDropdown');
var desiredOption = parent.querySelector('option[value="desired"]'); var domList = parent.children;
domList.indexOf(desiredOption); // Error! indexOf is not defined. domList.forEach(function() {
arguments.map(/* Stuff here */) // Error! map is not defined. }); // Error! forEach is not defined.
function func() { console.log(arguments);
}
func(1, 2, 3); // → [1, 2, 3]
```

### Spread operator
With ES6, you can use spreads to separate individual elements into a comma-separated syntax:
```
let arr = [1, 2, 3, ...[4, 5, 6]]; // [1, 2, 3, 4, 5, 6]

// in ES < 6, the operations above are equivalent to
arr = [1, 2, 3];
arr.push(4, 5, 6);
```

```
let arr = [..."123456"]; // ["1", "2", "3", "4", "5", "6"]
```

## Objects
* Variables that are assigned a non-primitive value are given a reference to that value. That reference points to the object’s location in memory. The variables don’t actually contain the value.

## Scope
* Let's start by looking at what would happen if we used `var`
```
var printsToBeExecuted = [];

for (var i = 0; i < 3; i++) {  
  printsToBeExecuted.push(() => console.log(i));
}

printsToBeExecuted.forEach(f => f());  
// Output: 3, 3, 3
```
Again, if you're used to block scope, this would feel a bit odd. You would expect `0, 1, 2` right?

The explanation is simply that a loop is not a scope when using `var`. So instead of creating a local variable `i` for each increment, it'll end up printing the final value for the variable for all the functions.

```
var printsToBeExecuted = [];

for (let i = 0; i < 3; i++) {  
  printsToBeExecuted.push(() => console.log(i));
}

printsToBeExecuted.forEach(f => f());  
// Output: 0, 1, 2
```
### Explain "hoisting".
only the declaration is hoisted, the assignment (if there is one), will stay where it is.
Function declarations have the body hoisted while the function expressions (written in the form of variable declarations) only has the variable declaration hoisted.
```
// Function Declaration
console.log(foo); // [Function: foo]
foo(); // 'FOOOOO'
function foo() {
  console.log('FOOOOO');
}
console.log(foo); // [Function: foo]

// Function Expression
console.log(bar); // undefined
bar(); // Uncaught TypeError: bar is not a function
var bar = function () {
  console.log('BARRRR');
};
console.log(bar); // [Function: bar]
```
### What is the difference between == and ===?
2 dấu bằng thì ép kiểu rồi mới so sánh, 3 dấu bằng thì so sánh luôn chứ không ép kiểu


### Bitwise XOR (^)
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_XOR

Given an array of integers, where all elements but one occur twice, find the unique element.
a = [1, 2, 3, 4, 3, 2, 1]

```
lonelyinteger(a) { return a.reduce((a, b) => a ^ b) }
```
```
I learn better with examples, so here I go trying to explain to my future self.

Let's say we have an array with: [1, 2, 2, 3, 1] We, know just by eyeballing it, the lonely integer is: 3 but we want to solve it using bit manipulation.

Just for notes: bit for 1=001, for 2=010, for 3=011 to get the answer, we just simply XOR all the values, and the remainder would be the lonely integer. since if the same number is being XOR with that same number, it will get 0.

back to example: first xor: 1^2 = 001^010 = 011 = 3 second xor (using the value from first xor): 3^2 = 011^010 = 001 = 1 third xor (using the value from previous xor): 1^3 = 001^011 = 010 = 2 last xor (using the value from previous xor): 2^1 = 010^001 = 011 = 3

that's how we get the answer 3.
```
### Ví dụ về dùng Map, Set để giải thuật toán

![image](https://user-images.githubusercontent.com/61957094/121404997-b8504100-c986-11eb-9270-4d06f0964b48.png)
![image](https://user-images.githubusercontent.com/61957094/121405037-c1411280-c986-11eb-9a53-41cb2c5b2df4.png)
)

### Những bài giải thuật toán hay
##### ================================================================

![image](https://user-images.githubusercontent.com/61957094/121464214-a8178080-c9dd-11eb-99b3-d0ea837a6229.png)
```
function firstDigit(s) {
  return s.match(/\d/)[0]
}
```

##### ================================================================
![image](https://user-images.githubusercontent.com/61957094/121466669-0181ae80-c9e2-11eb-85c4-cd37d3d767b6.png)

```
function differentSymbolsNaive(s) {
  return new Set(s).size
}
```

##### ================================================================
![image](https://user-images.githubusercontent.com/61957094/121490927-b1194980-c9ff-11eb-8ba7-fb92f41dac83.png)

```
function growingPlant(upSpeed, downSpeed, desiredHeight) {
    return upSpeed > desiredHeight ? 1 : Math.ceil((desiredHeight - upSpeed) / (upSpeed - downSpeed)) + 1;
}
```
