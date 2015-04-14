# Javascript Interview Questions

### Useful tricks
Get integer and change data type at the same time
```
'10.567890'|0  // 10
'10.567890'^0  // 10
-2.23456789|0  // -2
```
Change date to number
```
var d = +new Date(); // 1295698416972
```
Object like array to array
```
var arr = [].slice.call(arguments);
```
Random numbers
```
Math.random().toString(16).substring(2); // 14 digits
```
Combine arrays
```
var a = [1,2,3];
var b = [4,5,6];
Array.prototype.push.apply(a, b);
console.log(a); // [1,2,3,4,5,6]
```
