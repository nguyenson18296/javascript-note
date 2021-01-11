# Javascript Note
### Repeat a String
In the general case, this should be done using a correct polyfill for the ES6 String.prototype.repeat() method. Otherwise, the idiom new     Array(n +       1).join(myString) can repeat n times the string myString:
```
var myString = "abc"; var n = 3;
new Array(n + 1).join(myString); // Returns "abcabcabc"
```
