# Javascript Note
### Repeat a String
In the general case, this should be done using a correct polyfill for the ES6 String.prototype.repeat() method. Otherwise, the idiom new     Array(n +       1).join(myString) can repeat n times the string myString:
```
var myString = "abc"; var n = 3;
new Array(n + 1).join(myString); // Returns "abcabcabc"
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
