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

```Object.keys```: list of keys\
```Object.values```: list of values\
```Object.entries```:
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