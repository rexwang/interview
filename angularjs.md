# Angularjs Interview questions

### Angular executing order
1. app.config()
2. app.run()
3. directive's compile functions (if they are found in the dom)
4. app.controller()
5. directive's link functions (again if found)

[example link](http://jsfiddle.net/ysq3m/)

Run blocks - get executed after the injector is created and are used to kickstart the application. Only instances and constants can be injected into run blocks. This is to prevent further system configuration during application run time.

Run blocks are the closest thing in Angular to the main method. A run block is the code which needs to run to kickstart the application. It is executed after all of the service have been configured and the injector has been created. Run blocks typically contain code which is hard to unit-test, and for this reason should be declared in isolated modules, so that they can be ignored in the unit-tests.

One place you see run blocks used is for **authentication**.

### Directive Isolated Scope
##### Expression &
```
<div ng-controller="ChoreCtrl">
  <kid done="logChore(chore)"></kid>
</div>
```
```
var app = angular.module('myApp', []);

app.controller('ChoreCtrl', function($scope) {
  $scope.logChore = function(chore) {
    alert(chore + ' is done');
  };
});

app.directive('kid', function() {
  return {
    restrict: 'E',
    scope: {
      done: '&'
    },
    // When the scope done equals to '&', that means whatever passed in directive's
    // attribute 'done' is used to replace 'done'. So in the template, the 'done'
    // in ng-click is replaced by the value of 'done' in the directive. To pass variables,
    // we need to use special syntax, which use an object.
    template: '<input type="text" ng-model="chore">{{chore}}' +
              '<button ng-click="done({chore: chore})">Click Me</button>'
  };
});
```
##### String @
```
<div ng-app="phoneApp">
  <div ng-controller="AppCtrl">
    <drink flavor="{{ctrlFlavor}}"></drink>
  </div>
</div>
```
```
var app = angular.module('phoneApp', []);

app.controller('AppCtrl', function($scope) {
  $scope.ctrlFlavor = 'black burry';
});

app.directive('drink', function() {
  return {
    scope: {
      flavor: '@'
    },
    // Here whatever is inside the flavor attribute will be evaluated
    // as a string and passed in the template. This is why the binding
    // in controller still works, because the 'ctrlFlavor' is evaluated
    // as a string, its value is 'black burry', then the string
    // 'black burry' is passed into template.
    template: '<div>{{flavor}}</div>'
  };
});
```
### Difference between Service and Factory
```
app.service('myService', function() {

  // service is just a constructor function
  // that will be called with 'new'

  this.sayHello = function(name) {
     return "Hi " + name + "!";
  };
});

app.factory('myFactory', function() {

  // factory returns an object
  // you can run some code before

  return {
    sayHello : function(name) {
      return "Hi " + name + "!";
    }
  }
});
```
### Directive's Injecting, Compiling, and Linking functions
When you create a directive, there are essentially up to 3 functions layers for you to define:
##### Compile
This is where angular actually compiles your directive. This compile function is called just once for each references to the given directive. For example, say you are using the ng-repeat directive. ng-repeat will have to look up the element it is attached to, extract the html fragment that it is attached to and create a template function. To this template function you pass data and the return value of that function is the html with the data in the right places.

The compilation phase in Angularjs returns the template function. This template function is called **linking** function.

##### Linking phase
The linking phase is where you attach the data($scope) to the linking function and it should return your linked html. This is the function where you want to make changes to the linked html. In Angular if you write code in the linking function, it's generally the post-link function(by default). It is kind of a callback that gets called after the linking function has linked the data with the template.

##### Controller
The controller is a place where you put in some directive logic. This logic can go into the linking function as well, but then you would have to put that logic on the scope to make it "shareable". The problem with that is you would then be corrupting the socpe with your directives stuff which is not really something that is expected. So what is the alternative if two directives want to talk to each other? Of course you can put that logic into a service and then make both of directives depend on that service but that just bring in more dependency. The alternative is to provide a Controller for this scope(usually isloated scope), and then this controller is injected into another directive when that directive "requires" the other one.
