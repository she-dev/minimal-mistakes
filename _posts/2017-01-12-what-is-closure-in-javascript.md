---
title: What is closure in JavaScript?
excerpt: Understanding the concept of closure, how to use it, what are its benefits, how to get access to this inside the inner function, how it can help problems with avoid global variables.
modified:
header:
tags: 
---

JavaScript has function scope, not block scope like some C languages. Variables declared inside a function are not visible outside it and variables declared anywhere within a function are visible everywhere within that function.

This can cause problem if, for example, a variable is declared outside a function, as it will become a global variable and they're known to cause problems.

The concept of closure is that you create a function and one or more inner functions inside it and allow access to the methods and variables of the outer function only through the inner functions, preventing manipulation of the variables and methods. 

In the following example (taken from [JavaScript: The Good Parts](http://amzn.to/2jNNUs7)) we're declaring myObject and initializing it by calling a function that defines a value variable and returns an object with two methods. The variable is always available to `increment` and `getValue` but it's hidden from the rest of the program outside the function scope.

``` javascript
var myObject = function () {
  var value = 0;
  return {
    increment: function (inc) {
      value += typeof inc === 'number' ? inc : 1;
    },
    getValue: function () { 
      return value;
    }
  };
}();
```

It's not a function that's being assigned to myObject, it's the result of invoking that function. Notice the parentheses on the last line. The function returns an object with two methods that continue to have access to the value variable.

The variables declared in the function will continue to live as long as they are needed by one or more inner function, even after the outer function returned.
The inner function has access to the actual variables of the outer function, not copies of the variables.

The inner functions have access to all variables defined in the outer function, except for the arguments and this. You can pass this to the inner function by doing:

``` javascript
var outerFunction = function () {
  var that = this; // Workaround.
  var innerFunction = function () {
    // use that here
  };
}
``` 