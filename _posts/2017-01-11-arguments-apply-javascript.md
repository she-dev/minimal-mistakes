---
title: Arguments parameter and apply method
excerpt: Understanding the arguments parameter in JavaScript and the apply method to add functionality to our code.
modified:
header:
tags:
---

Arguments
---------

In JavaScript, functions have a *bonus* parameter called arguments.
When a function is invoked you can access all arguments passed to it accessing **arguments**.
This allows writing functions that take an unspecified number of parameters:

``` javascript
var sum = function () { var i, sum = 0;
  for (i = 0; i < arguments.length; i += 1) {
    sum += arguments[i];
  }
  return sum;
};
console.log(sum(4, 8, 15, 16, 23, 42));
```

Arguments is an array-like object. It looks like an array but doesn't have all the methods that an array has. It will contain all the parameters passed to the function, even those in excess, that means, those that weren't assigned in the function.


Apply
-----

> Because JavaScript is a functional object-oriented language, functions can have methods. 
**JavaScript: The Good Parts by Douglas Crockford**


The method *apply* can be used to invoke functions with some extra features.
It allows the invocation of a function with an array of arguments and you can choose the value of *this* for the invoked function.

The apply method takes two parameters: this and the array of parameters.

``` javascript
var add = function (a, b) {
  return a + b;
}
// Make an array of 2 numbers and add them.
var numbers = [3, 4];
var sum = add.apply(null, numbers);
sum;
> 7
```
In this example  `null` is passed as *this* and `numbers` as the parameters of the function.