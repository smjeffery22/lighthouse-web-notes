# **Jeffery Park's LHL Week 1 Notes**

## **Summary**
This file contains LHL lecture and Compass notes taken by `Jeffery Park`.

## **Table of Contents**
* Day 1 Lecture Notes
* Day 1 Compass Notes
* Day 2 Lecture Notes
* Day 2 Compass Notes
* Day 3 Lecture Notes
* Day 3 Compass Notes

## **Day 1 Lecture Notes**

## **Day 1 Compass Notes**

## **Day 2 Lecture Notes**

## **Day 2 Compass Notes**

## **Day 3 Lecture Notes**
### **Primitive Data Types**
* Boolean => false
* Null => already falsy
* String => ""
* Undefined => already falsy
* Number => 0
* Symbol => no falsy
* BigInt => 0

### **Data Structure**
Array => never falsy! because it is a structure\
Object => never falsy! because it is a structure

For accessing objects:
* **dot notaton**, shortcut, only used when we literally know the key
  * coffeePot.capacity
* **square bracket notation**, general form, used when we don't know yet, or we want a variable
  * const key = "capacity"
  * coffeePot[key]

```Object.keys()```: list of keys\
```Object.values()```: list of values\
```Object.entries()```:
  * Not the best one to use

```for...of```, for the key of the array of keys (only arrays)
```for...in```, for the key in the object (objects & its descendetns (includes arrays))\
```this``` can only be used inside an object and within function

### RECAP
Objects - **everything but the primitives** are objects\

When we know the name of the key, we can use dot notation (literal)\

When we don't know, or want to use a variable, we use the square bracket notation\

We read by acceesing the value the same way as a variable
* bob
* someObject.someKey\

We set a value by assigning it
* bob = 5
* someObject.someKey = 10\


Methods - functions defined inside an object\

```this``` - represents the context of wher the function is defined

## **Day 3 Compass Notes**
### **JavaScript Object**
Object is a collection of key-value pairs, where each key maps to a value.
```javascript
const myObject = {
  key: "value",
  anotherKey: "another value"
};
```
* Above code is **object literal** syntax.

### **Objects - Basic Concepts**
Objects:
* Contain **key-value pairs**; each key maps to a value
* Contain **keys** which are **always strings** (or symbols (less important))
* Have **unique keys**; the same key cannot appear twice in an object
* Have their keys point to **values** which can be of **any type**

### **countOnly Function**
```countOnly``` function takes in a collection of items and return counts for a specific subset of those items.\
```countOnly``` will be given an array and an object.
* Returns an object containing counts of everything that the input object listed.
![alt text](https://d.pr/i/6B4i7p+)

**Utility Function**\
```util.inspect()``` returns a string representation of an object

## **Day 4 Lecture Notes**
**variables**: *storage* for various things\
**functions**: block of code that is *reusable*

for...of: elements\
for...in: index\

```for...each```
* forEach(function(element, index, array))
  * element: 
  * index (optional):
  * array (optional):
  * Combination of
    * for c style
    * for...in
    * for...of
    * while
  * Speed: for c style > for...in & for...of > forEach
    * However, negligible difference
    * forEach is used widely for styling & readability


**Arrow Function**\
Replace the ```function``` with ```=>```
* If the function is a 1-liner, brackets are not needed
* If the function is a 1-liner and it returns something, return is not needed
* If the function has only 1 parameter, () is optional

```js
// BEFORE: anonymous callback as function expression 
[1,2,3].forEach(function (num) {
  console.log('num: ', num);
});

// AFTER: anonymous callback as arrow function
[1,2,3].forEach((num) => {
  console.log('num: ', num);
});

// ONE-LINER: further remove some characters
[1,2,3].forEach(num => console.log('num: ', num));

```

## **Day 4 Compass Notes**
In JS, functions are **first-class objects**. Fist-class objects are:
* Appear in an expression
* Be assigned to a variable
* Be used as an argument
* Be returned by a function call

### Callback Functions
A callback function:
* Is a function passed (by reference) into another function ("receiver" function)
* The "receiver" function is therefore accepting behaviour to perform by calling the callback function that it now has access to
* The receiver function can decide to call the callback function at any time, as many times as it wants

### Anonymous Functions
Functions do not need to be named or even assigned to a variable.\
**Often a callback function would not be declared or assignment to a variable.**

### Higher-Order Functions
Functions that take in callbacks are referred to as **Higher-Order Functions**\
Higher-order functions are any functions which operate on other functions
* ```forEach``` and ```filter``` are examples of higher-order functions

### Array.prototype.filter
Creates a new array with all elements that **pass the test** implemented by the provided function.
```js
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

### Array.prototype.map
Created a new array populated with the **results of calling a provided function** on every element in the calling array.

## **Day 5 Compass Notes**
### Object methods and 'this'
```js
const person = {
  firstName: 'Bob',
  lastName:  'Smith',
  fullName: function() {
    return this.firstName + ' ' + this.lastName;
  }
}
```
Functions that are attached to objects like shown above are often referred to as a "method".\
In the above case, ```this``` refers to the object the method (function) was called on.

### Recursion
An alternative to traditional looping that allows to do the same thing, just in a slightly different way.
* Not a better way, just a different way
* Some languages do not have any ```for``` and ```while``` loops

```js
1.| function countEvenToTwelve(number) {
2.|   if (number <= 4) {              // number = 0
3.|     console.log(number);          // 0
4.|     countEvenToTwelve(number+2);  // countEvenToTwelve(2)
        // if (number <= 4)             number = 2
        // console.log(number);          2
        // countEvenToTwelve(number+2);  countEvenToTwelve(4)
        //   if (number <= 4)             number = 4
        //   console.log(number);          4
        //   countEvenToTwelve(number+2);  countEvenToTwelve(6)
5.|   }
6.| }
7.| countEvenToTwelve(0);
```

* On line 4, the function is calling itself - recursion
* A recursive function will call itself to execute code over and over again until it is stopped by a condition
* Recursive function **must stop itself at some point**, otherwise it will continue to call itself forever
* `number <= 12` is referred to as a **recursive case**
  * As long as this is true, the function will continue to call itself
* `number > 12` is referred to as a **base case**
  * If this is true, the function will not call itself
* A function must have at least one recursive case and at least one base case in order to be recursive

```js
function countUpFrom(number) {
  console.log(number);
  countUpFrom(number+1);
}
countUpFrom(1);
```
* Above code will crash with the error message `RangeError: Maximum call stack size exceeded`
  * This is known as *stack overflow*

## **Weekend Compass Notes**
### Modules
```js
Module {
  id: '.',
  exports: {},
  parent: null,
  filename: '/Users/superman/codes/moduleCheck.js',
  loaded: false,
  children: [],
  paths: [ ... ] 
}
```
* Every file run by Node has access to a `module` object
* A JS file must "export" the part that it wants to be `require`-able (aka "importable")
  * **A file must export code before it can be required**
  * By default, node will export an empty object for each file
* `module.exports` tells node what to export from a file
  * Default is an empty object {}
* `require` is used with relative paths to import the exported item

### Automated Testing
**Mutual Testing**: Testing code by "write - run - check - modify - run - ..."\
**Automated Testing**: Practice of writing code to programmatically test the actual code we want to write
  * Saves testing time (avoid mutual tests)
  * Saved debugging time (catches bugs earlier)
  * Easier to program (work on part(s) of code at a time)
  * Easier to come back to a program after some time
  * Easier to work together
  * Acts as documentation (reading tests is a great way to learn about how code is meant to be used)
  * Improves the quality of our code

[What are Unit Testing, Integration Testing and Functional Testing?](https://codeutopia.net/blog/2015/04/11/what-are-unit-testing-integration-testing-and-functional-testing/)

**Unit Testing**\
Practice of testing small pieces of code, typically individual functions.
  * Give the function some inputs and check if the outputs are correct
  * Helps to write better code, because a code that is hard to unit test usually has poor design
  * Chcek and fix bugs

Unit testing should be used all the time as it not only prevent bugs, but also improve the code design\
Popular tools for unit testing include Mocha, Jasmine and Tape.

