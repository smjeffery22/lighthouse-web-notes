# NEWER JS FEATURES

`Default Parameters`
* When argument is not passed in, default value can be assigned in the parameter

```js
// If the argument is left empty when the function is called, it uses the default value of 6
function rollDie(numSides = 6) {
  return Math.floor(Math.random() * numSides) + 1;
}

// When there are multiple parameters, default param(s) should not be the first parameter
function greet(person, msg = 'Hello, there') {
  console.log(`${msg}, ${person}`);
}
```


`Spread (...spread)`

```js
const nums = [1, 2, 3, 4, 5, 6, 7];
Math.max(...nums); // goes through the array and returns the max number (7)
console.log(...nums); // each element in the array is pass in as separate arguments (1 2 3 4 5 6 7)
// ...nums spreads the array into separate arguments

// React - adding state to existing array
// Initial history => [initial]
const [history, setHistory] = useState([initial]);
// Updated with setHistory => [initial, newMode]
setHistory(prev => [...prev, newMode]);

```

**In Array Literals:** Create a new array using an exsiting array. Spreads the elemtns from one array into a new array.

```js
const numSetOne = [1, 2, 3, 4, 5];
const numSetTwo = [6, 7, 8, 9, 10];

const numSet = [...numSetOne, ...numSetTwo] //combines the two arrays
const numSetNew = [0, ...numSetOne, ...numSetTwo, 11]
```

**In Object Lieterals:** Copies properties from one object into another object 

```js
const feline = { legs: 4, family: 'Felidae' };
const canine = { isFurry: true, family: 'Caninae' }

const newObjectOne = {...feline, color: 'black'} // creates a new object with feline object and the new property (3 key-value pairs)
const newObjectTwo = {...feline, ...canine} // creates a new object with the two objects; since family key overlaps, the latter one overwrites => order matters
```


`Rest Params`
* Collects all remaining arguments into an actual array

```js
// Arguments are collected into nums array
function sum(...nums) {
  return nums.reduce((total, el) => total + el);
}

sum(1, 2, 3, 4);

// The first two arguments are stored in the first two parameters
// The rest of the arguments are collected and stored in the third parameter
function (raceResults(gold, silver, ...everyoneElse) {
  console.log(gold);
  console.log(silver);
  console.log(everyoneElse);
}

raceResults('Tammy', 'Todd', 'Tina', 'Trevor', 'Travis');
```


`Destructuring`
* A short, clean syntax to 'unpack' the following into distinct variables 
  * Values from arrays
  * Properties from objects

**Array Destructuring**
```js
const score = [100, 95, 88, 60, 50];
const [first, second, third, ...everyoneElse] = score;
// first = 100; second = 95; third = 88; everyoneElse = 60, 50; 
```

**Object Destructuring**
```js
const user = {
  id: 1,
  firstName: 'Jeffery',
  lastName: 'Park',
  email: 'parkjon8@gmail.com'
}

// Makes each property a variable
const {id, firstName, lastName, email} = user;

// Creates a new variable 'userId' using user.id (variable 'id' becomes 'userId')
const { id: userId } = user;
```

**Params Destructuring**
```js
// Destructuring can be done in function parameter
function fullName({ firstname, lastName }) {
  return `${firstName} ${lastName}`;
}
```