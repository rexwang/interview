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
