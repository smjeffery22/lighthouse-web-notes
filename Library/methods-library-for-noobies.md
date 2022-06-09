# **Methods Library for Noobies**

## **ARRAY**
* When comparing arrays, the reference in memory is being compared
  * Each array is assigned its own reference in memory
    * Two arrays cannot be equal

**`Array.concat()`** Merge arrays
  ```js
  const array1 = ['a', 'b', 'c'];
  const array2 = ['d', 'e', 'f'];
  const array3 = array1.concat(array2);

  console.log(array3);
  // expected output: Array ["a", "b", "c", "d", "e", "f"]
  ```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)


**`Array.every()`** *Returns Boolean value* after testing whether *all the elements in the array pass the test* in the callback function
  * checks the array, if all elements return true, entire result returns true

  ```js
  const isBelowThreshold = (currentValue) => currentValue < 40;

  const array1 = [1, 30, 39, 29, 10, 13];

  console.log(array1.every(isBelowThreshold));
  // expected output: true
  ```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)


**`Array.filter()`** *Creates a new array* with all elements that pass the test implemented by the provided function
  * Element *added* to new array it the callback function *returns true*
  * Can be grouped with '.map()' method to filter first then getting values from the filtered array
  ```js
  const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

  const result = words.filter(word => word.length > 6);

  console.log(result);
  // expected output: Array ["exuberant", "destruction", "present"]
  ```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)


**`Array.find()`** *Returns the value of the first element* in the provided array that satisfies that provided testing function
  * callback will return a boolean
  * finds and returns the first element that is true
  ```js
  const array1 = [5, 12, 8, 130, 44];

  const found = array1.find(element => element > 10);

  console.log(found);
  // expected output: 12
  ```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)


**`Array.findIndex()`** Returns the *index of the first element* in the array that satisfies the provided testing function. Otherwise, it returns -1, indicating that no element passed the test.
  ```js
  const array1 = [5, 12, 8, 130, 44];

  const isLargeNumber = (element) => element > 13;

  console.log(array1.findIndex(isLargeNumber));
  // expected output: 3
  ```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)


**`Array.forEach()`** Accepts a callback function and *calls the function once per element in the array*
  * 'for...of' used more often now
  * foreach does not need to return anything
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)


**`Array.from()`**


**`Array.includes()`** *Look for a value* in an array; *returns boolean value*
  ```js
  const pets = ['cat', 'dog', 'bat'];

  console.log(pets.includes('cat'));
  // expected output: true

  console.log(pets.includes('at'));
  // expected output: false
  ```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)

**`Array.indexOf()`**
  ```js
  const beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];

  console.log(beasts.indexOf('bison'));
  // expected output: 1

  // start from index 2
  console.log(beasts.indexOf('bison', 2));
  // expected output: 4

  console.log(beasts.indexOf('giraffe'));
  // expected output: -1
  ```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)

**`Array.join()`** Create a string from an array


**`Array.map()`** **Creates a new array** with the results of calling a callback on every element in the array
  * returns a new array that matches the provided code in the callback function
  * map expects a return / output
  ```js
  const array1 = [1, 4, 9, 16];

  // pass a function to map
  const map1 = array1.map(x => x * 2);

  console.log(map1);
  // expected output: Array [2, 8, 18, 32]
  ```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)


**`Array.reduce()`** Executes a user-supplied "reducer" callback function on each element of the array, in order, passing in the return value from the calculation on the preceding element. The final result of running the reducer across all elements of the array is a single value
  * Taking a list of values and reducing them down to a single value
  * Second argument can be added to set the initial value
  * First parameter: accumulator/total; what we are reducing down to
  * Second parameter: each individual element in the array

  1. Runs a function on every single element
    * First parameter: whatever the previous iteration returned
    * Second parameter: current element in the array
  2. First parameter will start with the first iteration with whatever is passed as the second parameter of .reduce method

  ```js
  // To sum the total in the array
  //  on the first iteration, accumulator = 3 and currentValue = 5
  //  the return value carries on to the next iteration and becomes the accumulator
  [3, 5, 7, 9, 11].reduce((accumulator, currentValue) => {
    return accumulator + currentValue;
  })

  // To find the minimum value in the array
  [3, 5, 7, 9, 11].reduce((min, currentValue) => {
    return (currentValue < min) ? currentValue : min;
  })
  ```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)


**`Array.reverse()`** Reverse an array
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)


**`Array.slice(startIndex, endIndex)`** Copy a portion on an array, including startindex and excluding endIndex
  * New array

  ```js
  const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

  console.log(animals.slice(2));
  // expected output: Array ["camel", "duck", "elephant"]

  console.log(animals.slice(2, 4));
  // expected output: Array ["camel", "duck"]

  console.log(animals.slice(1, 5));
  // expected output: Array ["bison", "camel", "duck", "elephant"]

  console.log(animals.slice(-2));
  // expected output: Array ["duck", "elephant"]

  console.log(animals.slice(2, -1));
  // expected output: Array ["camel", "duck"]
  ```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)


**`Array.some()`** *Returns Boolean value* after testing whether *at least one element* in the array passes the test in the callback function
  * checks the array, if at least one element returns true, entire result returns true
  ```js
  const array = [1, 2, 3, 4, 5];

  // checks whether an element is even
  const even = (element) => element % 2 === 0;

  console.log(array.some(even));
  // expected output: true
  ```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)


**`Array.splice(index, deleteCount, itemNames)`** Remove/replace elements
  * Original array is mutated
  
  ```js
  const months = ['Jan', 'March', 'April', 'June'];
  months.splice(1, 0, 'Feb');
  // inserts at index 1
  console.log(months);
  // expected output: Array ["Jan", "Feb", "March", "April", "June"]

  months.splice(4, 1, 'May');
  // replaces 1 element at index 4
  console.log(months);
  // expected output: Array ["Jan", "Feb", "March", "April", "May"]

  ```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)


**`Array.shift()`** Remove the element from the start of the array

**`Array.sort()`** Sort an array
  | compareFunction(a, b) | sort order                                    |
  |-----------------------|-----------------------------------------------|
  |          > 0          | sort b before a                               |
  |          < 0          | sort a before b                               |
  |         === 0         | keep original order of a and bsort b before a |
  ```js
  // to sort numerically in ascending order
  function compareNumbers(a, b) {
    return a - b;
  }

  // to sort alphabetically in ascending order
  items.sort(function(a, b) {
    var nameA = a.name.toUpperCase(); // ignore upper and lowercase
    var nameB = b.name.toUpperCase(); // ignore upper and lowercase
    if (nameA < nameB) {
      return -1;
    }
    if (nameA > nameB) {
      return 1;
    }
  ```
  * [link to MDN](hhttps://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)


**`Array.pop()`** Remove an element from the end of the array
  * *Return a value*, not an array
    * i.e. returns the removed element


**`Array.push()`** Add an element to the end of the array




**`Array.unshift()`** Add one or more element(s) from the start of the array



**`Array.splice()`** Remove/replace elements
  ```js
  const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

  // bad
  const arr = Array.prototype.slice.call(arrLike);

  // good
  const arr = Array.from(arrLike);
  ```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)


**`Spread syntax (...)`**


## **OBJECT**
* Object keys are converted to strings

**`Object.keys()`**


**`Object.values()`**


## **STRING**
**`String.substring()`**
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring)

**`.replace(a, b)`**

**`.trim():`** trims white space at the beginning and end of a string

## **MATH**
**`Math.toFixed():`** Round to certain decimal places
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed)

**`Math.pow(base, power):`** Returns the base to the exponent power, as in base^exponent

```js
console.log(Math.pow(2, 3));
// expected output: 8
```
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/pow)

**`Math.random()`**
  * [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random)


## **EXPRESS**
**`app.get()`**:

**`app.json()`**:

**`app.post()`**:

**`app.render('ejs file', ??)`**:
  * Answer to what it will do in response to get request
    1. Express will look in the veiw folders for a file name asked
    2. Express will compile that page, run any JS statmeent it finds, then output the final HTML code
    3. Send back the full HTML code to the browser and render the HTML to the user
  * ??: what we want the ejs file to have access to (only keynames)

**`app.redirect()`**:

**`app.send()`**:


## **EXPRESS**
**`res.cookie()`**:
* Setting cookies

**`req.cookies()`**:
* Reading cookies

## **CHAI**
**`assert.strictEqual`**: for strictly comparing values\
**`assert.deepEqual`**: for strictly comparing arrays\xdcgbhnhj


## **FILE SYSTEM (fs)**
Must include `const fs = require('fs');` in the code

**`fs.fileRead(path[, options], callback)`**\
*Asynchronously reads* the *entire contents* of a file.

```js
fs.readFile(`../data/index.txt`, 'utf8', (error, data) => {
  // ISSUE: Returning from *inner* callback function, not breedDetailsFromFile.
  if (!error) {
    breedData(data);
  } else {
    breedData(data);
  }
});
```

* data is the contents of the file

**`fs.fileWrite(file, data[, options], callback)`**\
*Asynchronously writes* data to a file, *replacing* the file if it already exists.

```js
const content = "Testing writeFile";
fs.writeFile('./index.html', content, err => {
  if (err) {
    console.log(err);
    return
  } else {
    console.log("writeFile success!");
  }
})
```

* index.html file will be created/replaced and the content will be saved within index.html file
* if the file path is invalid, err

**`fs.existSync()`**


## **JSON (JaveScript Object Notation)**

**`JSON.parse():`** Parse a string as JSON, optionally transform the produced value and its properties, and return the value
  * Deserialization

**`JSON.stringify():`** Return a JSON string corresponding to the specified value, optionally including only certain properties or replacing property values in a user-defined manner
  * Serialization

``` js
const jsonString = '{"a": 1, "b": 2, "foo": "bar"}';
const obj = JSON.parse(jsonString);
  // obj = { a: 1, b: 2, foo: "bar"}
const obj2 = JSON.stringify(obj);
  // obj2 = '{"a": 1, "b": 2, "foo": "bar"}'
```

## **General Methods**

**parseInt():** converts string into an integer

**String.padStart():** pads the current string with another string (multiple times, if needed) until the resulting string reaches the given length

```js
const str1 = '5';

console.log(str1.padStart(2, '0'));
// expected output: "05"

const fullNumber = '2034399002125581';
const last4Digits = fullNumber.slice(-4);
const maskedNumber = last4Digits.padStart(fullNumber.length, '*');

console.log(maskedNumber);
// expected output: "************5581"
```

**String.padEnd()**

```js
const str1 = 'Breaded Mushrooms';

console.log(str1.padEnd(25, '.'));
// expected output: "Breaded Mushrooms........"

const str2 = '200';

console.log(str2.padEnd(5));
// expected output: "200  "
```

## **in Operator**

  - `in` operator is used to check if a specified *property* exists in an objects or in its inherited properties
  - Returns `true` if the specified property exists

  - For array, verifies if an *index/key* exists on an array

```js
// OBJECT
class Car {
  constructor(make, model, year) {
    this.make = make;
    this.model = model;
    this.year = year;
  }
  start() {
    console.log(`Starting ${this.make} ${this.model}, ${this.year}`);
  }
}

const toyota = new Car('Toyota', 'Camry', '2018');

'start' in toyota;
/* Returns true as toyota is an instance of the Car object constructor. The toyota object therefore inherits all properties of the Car constructor. */

'toString' in toyota;
/* Returns true. toString is a method property of the Object type, of which the Car constructor is an instance of. */

'make' in car // Returns true.
'Toyota' in car // Returns false. 'Toyota' is not a property name, but a value.
```

```js
// ARRAY
const number = [2, 3, 4, 5];

3 in number // Returns true.
2 in number // Returns true.

5 in number // Returns false because 5 is not an existing index on the array but a value;

'filter' in number
/* Returns true because filter is a method property on the Array type of which the number array is an instance of. The number array inherits the filter property.*/
```