# Javascript Interview Questions

### Useful tricks
##### Get integer and change data type at the same time
```
'10.567890'|0  // 10
'10.567890'^0  // 10
-2.23456789|0  // -2
```
##### Change date to number
```
var d = +new Date(); // 1295698416972
```
##### Object like array to array
```
var arr = [].slice.call(arguments);
```
##### Random numbers
```
Math.random().toString(16).substring(2); // 14 digits
```
##### Combine arrays
```
var a = [1,2,3];
var b = [4,5,6];
Array.prototype.push.apply(a, b);
console.log(a); // [1,2,3,4,5,6]
```
##### Condition
```
var a = b && 1;

is smilar with

if (b) {
  a = 1;
}
-------------------------------------------
var a = b || 1;

is smilar with

if (b) {
  a = b;
} else {
  a = 1;
}
```
##### Interchange value of two variables without creating temp variable
```
var a = 1;
var b = 2;
a = [b, b=2][0];
console.log(a); // 2
console.log(b); // 1
```

### Asynchronous Programming

##### forEach loop
```
function getStockSymbols(stocks) {
  var symbols = [];
  
  stocks.forEach(function(stock) {
    symbols.push(stock.symbol);
  });
  
  return symbols;
}

var symbols = getStockSymbols([
  { symbol: "XFX", price: 240.22, volume: 23432 },
  { symbol: "TNZ", price: 332.19, volume: 234 },
  { symbol: "JXJ", price: 120.22, volume: 5323 },
]);

console.log(JSON.stringify(symbols));
```
output: *"[\"XFX\",\"TNZ\",\"JXJ\"]"*

##### Array Map Function, great for apply transformation to every item in the array and returns a new array
```
function getStockSymbols(stocks) {
  return stocks.map(function(stock) {
    return stock.symbol;
  });
}

Array.prototype.map = function(projection) {
  var results = [];
  
  this.forEach(function(item) {
    results.push(projection(item));
  });
  
  return results;
};

var symbols = getStockSymbols([
  { symbol: "XFX", price: 240.22, volume: 23432 },
  { symbol: "TNZ", price: 332.19, volume: 234 },
  { symbol: "JXJ", price: 120.22, volume: 5323 },
]);

console.log(JSON.stringify(symbols));
```
output: *"[\"XFX\",\"TNZ\",\"JXJ\"]"*

##### Array Filter Function, returns a new array which only contains items that pass the test
```
function getStocksOver(stocks, minPrice) {
  return stocks.filter(function(stock) {
    return stock.price >= minPrice;
  });
}

var expensiveStocks = getStocksOver([
  { symbol: "XFX", price: 240.22, volume: 23432 },
  { symbol: "TNZ", price: 332.19, volume: 234 },
  { symbol: "JXJ", price: 120.22, volume: 5323 },
],
150.00);

console.log(JSON.stringify(expensiveStocks));
```

### Javascript Memoization Pattern
```
function memoize(func) {
  var memo = {},
      slice = Array.prototype.slice;
  
  return function() {
    var cacheKey = slice.call(arguments);
    if (cacheKey in memo) {
      console.log('reading cached data');
      return memo[cacheKey];
    } else {
      console.log('adding data to cache');
      return (memo[cacheKey] = func.apply(this, cacheKey));
    }
  };
}
```
Useage:
```
function add(x, y) {
  return x + y;
}

var newAdd = memoize(add);
console.log(newAdd(3,4));
console.log(newAdd(3,4));
```
