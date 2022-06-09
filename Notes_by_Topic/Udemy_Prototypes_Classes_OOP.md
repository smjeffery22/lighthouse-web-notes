# Prototypes / Classes / OOP

## Prototypes

- Object that contains common methods/properties 
  - Ex. Object/Array/String methods

- Prototypes are template objects that typically contain a bunch of methods
  - Multiple objects can be created that share the same prototype
    - All have access to the same methods without having to have their own copy
      - Ex. Array.prototype, String.prototype

## Object Oriented Programming (OOP)

## Class

- Constructor function runs automatically when a new instance of the class is instantiated
  - Whatever is inside the constructor get assigned as the properties within the object

- Methods are added to the prototype automatically
  - Methods can be included in the constructor

- 'this' refers to the instance of the class, the individual object

```js
class Color {
  constructor(r, g, b, name) {
    // console.log('INSIDE CONSTRUCTOR!');
    // console.log(r, g, b);

    this.r = r;
    this.b = b;
    this.g = g;
    this.name = name;
  }
  innerRGB() {
    const { r, g, b } = this;
    return `${r}, ${g}, ${b}`;
  }
  rgb() {
    return `rgb(${this.innerRGB()})`;
  }
  rgba(a = 1.0) {
    return `rgba(${this.innerRGB()}, ${a})`;
  }
}

const c1 = new Color(255, 67, 89, 'tomato');
```

### Extends and Super

- `extends` class that extends from the base class

- `super` is the reference to the superclass
  - reference to what it is extending from

```js
class Pet {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  eat() {
    return `${this.name} is eating!`;
  }
}

class Cat extends Pet {
  constructor(name, age, livesLeft = 9) {
    super(name, age);
    this.livesLeft = livesLeft;
  }
  meow() {
    return 'MEOWWW!';
  }
}

class Dog extends Pet {
  bark() {
    return 'WOOFFF!';
  }
  eat() {
    return `${this.name} scarfs his food!`;
  }
}
```
