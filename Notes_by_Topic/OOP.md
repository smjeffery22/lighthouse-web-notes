# OBJECT ORIENTED PROGRAMMING (OOP) (LHL W2)

## **Day 5 Compass Notes**

### **Object Oriented Programming (OPP)**

- Probably the biggest concept in software development philosophy
- Object Orientation is a way of writing code that:
  - encourages **modularity**
  - **reduces duplication** through the use of objects
- `Object` is a collection of **key-value pairs** known as **properties**
  - Each key-value pair is a **state**
  - When a property's value is a **function**, it is called a **method**
  - Method is also known as the object's **behaviour**
- `this` is used inside an object whenever a method is accessing a property or another method on the same object

### **OOP Part 1: Classes & Instances**

- **Classes** is a way to perform Object Orientation
- JS's object system is based on another pattern known as _prototypes_
  - Classes were added to JS in ES6
- In OPP, classes are blueprints (templates) that we use to create instances of objects
  - Class describes what the object is going to be
  - New object can be created using the class

```js
class Pizza {
  constructor(size, crust) {
    this.size = size;
    this.crust = crust;
    this.toppings = ["cheese"];
  }

  addTopping(topping) {
    this.toppings.push(topping);
  }
}
let pizza1 = new Pizza("large", "cheese");
let pizza2 = new Pizza();
```

- To declare a class, use `class` keyword along with its name
  - Class name should be a noun
  - First letter of the class name should be capitalized
- New objects can be created from a class using `new` keyword
  - pizza1 and pizza2 are **instances** of the Pizza class
- `constructor` and `addTopping` are _methods_
  - `constructor` gets executed when an object instance is created from a class
    - Default values for an object
    - Since it's a method, values can be passed into it
- `toppings` is a _property_

### **OOP Part 2: Inheritance**

- Classes can share multiple of the same properties
- The duplication can be moved to another class
- `Inheritance` technique allows to build a new class based on an existing class

```js
// This class represents all that is common between Student and Mentor
class Person {
  // moved here b/c it was identical
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  // moved here b/c it was identical
  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

class Student extends Person {
  // stays in Student class since it's specific to students only
  enroll(cohort) {
    this.cohort = cohort;
  }
}

class Mentor extends Person {
  // specific to mentors
  goOnShift() {
    this.onShift = true;
  }

  // specific to mentors
  goOffShift() {
    this.onShift = false;
  }
}

let student1 = new Student("Jeffery Park", "Hello");
console.log(student1);
```

- _Student_ and _Mentor_ inherit behaviour and state information from _Person_ using the keyword `extends`
  - Person is the **superclass**
  - Student and Mentor are **subclasses** of the Person class
    - They are _extensions_ of Person class

### **OOP Part 3: Super**

- `super` keyword allows subclasses to have a reference on the parent class
  - **method overriding:** when a subclass implements a method that already exists in the superclass
  - Avoid repeating code that is already present in the superclass

```js
// Super class
class Person {
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

class Mentor extends Person {
  // Mentor bios need to include a bit more info
  bio() {
    return `I'm a mentor at Lighthouse Labs. ${super.bio()}`;
  }
}

// DRIVER CODE
const bob = new Mentor("Bob Ross", "I like mountains way too much");
console.log(bob.bio());
```

### **OPP Part 4: Getters and Setters**

- `Getters:` a method used to get the value of a property
- `Setters:` a method used to set the value of a property
- Benefits of using getters and setters
  - **Validating** data before assigning it to a property
  - **Computing** a value on the fly instead of simply pulling it out of a property

```js
class Pizza {
  // ... CODE FROM PART 1 ...

  // setSize now includes data validation
  // size only gets assigned if one of the conditions is true; else undefined
  set size(size) {
    if (size === "s" || size === "m" || size === "l") {
      this._size = size;
    }
  }

  get price() {
    const basePrice = 10;
    const toppingPrice = 2;
    return basePrice + this.toppings.length * toppingPrice;
  }
}

// DRIVER CODE
const pizza = new Pizza();
pizza.size = "s";
pizza.addTopping("pepperoni");
pizza.addTopping("pepper");
console.log(pizza);
console.log(pizza.price);
```

### **OPP Best Practices**

- In JS, properties cannot be made private
  - Simply add `_` to the start of a property name
    - Letting other developers know that the property should not be accessed directly (outside the class)
    - ```js
      class Pizza {
        constructor() {
          this._toppings = [];
        }
        addTopping(topping) {
          this._toppings.push(topping);
        }
      }
      let pizza = new Pizza();
      pizza.addTopping("cheese");
      pizza.addTopping("mushrooms");
      ```
- Each class should be responsible for a single part of the functionality
- Inheritance