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

### Closure
Closures have access to their outter function's variables even after outter function returns.
Closures store references to the outter function's variables, which means closures can access updated variables.

### Prototype
There are two interralted concepts with ***prototype*** in Javascript:

  1. First, every JavaScript function has a ***prototype property*** (this property is empty by default), and you attach properties and methods on this prototype property when you want to implement inheritance.
  2. The second concept with prototype in JavaScript is the ***prototype attribute***. An object's prototype points to the object's parent. The prototype attribute is normally referred to as the prototype object, and it's set automatically when you create a new object.

Why is prototype important and when it is used?
  1. Prototype property is important because JavaScript doesn't have classical inheritance based on Classes, and therefore all inheritance in Javascript is made possible through prototype property. For example, you can create a fruit function and add properties and methods to the function's prototype property, and all instance of the Fruit function will inherit all Fruit's properties and methods.
  2. Prototype attribute is important for accessing object's properties and methods. For example, if you want to access a property of an object, the search begins directly on the object, if your JS runtime can't find the property there, it then looks for the property on the object's prototype. If the property is not found on the object's prototype, the search moves to the prototype of the object's prototype, its grandfather. And this continues until there is no more prototype. **This in essence is the prototype chain**.

### Javascript Design Pattern

##### Memoization Pattern
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

##### Singleton Pattern
```
var mySingleton = (function() {
  var instance;
  function init() {
    function privateMethod() {}
    return {
      publicMethod: function() {},
      publicProperty: 'I am public'
    }
  }
  
  return {
    getInstance: function() {
      if (!instance) {
        instance = init();
      }
      return instance;
    }
  }
}());
```

##### Observer Pattern
```
var Subject = (function() {
  function Subject() {
    this._list = [];
  }
  
  Subject.prototype.observe = function(obj) {
    this._list.push(obj);
  };
  
  Subject.prototype.unobserve = function(obj) {
    for (var i = 0; i < this._list.length; i++) {
      if (this._list[i] === obj) {
        this._list.splice(i, 1);
        return true;
      }
    }
    return false;
  };
  
  Subject.prototype.notify = function() {
    var args = Array.prototype.slice.call(arguments, 0);
    for (var i = 0; i < this._list.length; i++) {
      this._list[i].update.apply(null, args);
    }
  };
  
  return Subject;
}());
```

##### Decorator Pattern
A function decorator accepts a function, decorates it's call and returns the wrapper, which alters default behavior. For example, a doublingDecorator accepts a function func and returns the decorated variant which doubles the result
```
function doublingDecorator(func) {
  return function() {
    return 2 * func.apply(this, arguments);
  };
}
```
```
// Useage:
function sum(a, b) {
  return a + b;
}

var doubleSum = doublingDecorator(sum);

doubleSum(1,2); // 6
doubleSum(2,3); // 10
```
An Object decorator delegates extra reponsibilities to the object where it doesn't make sense to subclass it. e.g.
```
//What we're going to decorate
function MacBook() {
    this.cost = function () { return 997; };
    this.screenSize = function () { return 13.3; };
}
/*Decorator 1*/
function Memory(macbook) {
    var v = macbook.cost();
    macbook.cost = function() {
        return v + 75;
    }
}
 /*Decorator 2*/
function Engraving( macbook ){
   var v = macbook.cost();
   macbook.cost = function(){
     return  v + 200;
  };
}
/*Decorator 3*/
function Insurance( macbook ){
   var v = macbook.cost();
   macbook.cost = function(){
     return  v + 250;
  };
}
var mb = new MacBook();
Memory(mb);
Engraving(mb);
Insurance(mb);
console.log(mb.cost()); //1522
console.log(mb.screenSize()); //13.3
```

```
Array.prototype.push = function() {
    for( var i = 0, l = arguments.length; i < l; i++ ) this[this.length] = arguments[i];
    return this.length;
};
```
##### Dependency Injection
There are three ways a component(object or function) holds its dependencies.
  1. The component can create the dependency, typically by calling the new operator.
  2. The component can look up the dependency, by referring to a global variable.
  3. The component can have the dependency passed to it where it is needed.

The first two options of creating or looking up dependencies are not optimal because they hard code the dependency to the component. This makes it difficult to modify the dependency. This is especially problematic in tests, where it is often desirable to to provide mock dependencies for test isolation.

The third one is more viable, since it removes the responsibility of locating the dependency from the component. The dependency is simply given to the component.
