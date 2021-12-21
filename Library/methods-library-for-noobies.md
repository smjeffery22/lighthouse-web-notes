# **Methods Library for Noobies**

## **ARRAY**
**`Array.concat()`**

**`Array.filter()`**

**`Array.forEach()`**
* [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

**`Array.from()`**

```js
const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

// bad
const arr = Array.prototype.slice.call(arrLike);

// good
const arr = Array.from(arrLike);
```

* [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)

**`Array.includes()`**
* [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)

**`Array.indexOf()`**
* [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)

**`Array.map()`**

**`Array.reverse()`**
* [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)

**`Array.slice()`**

**`Array.splice()`**

**`Array.sort()`**

**`Spread syntax (...)`**


## **OBJECT**
**`Object.keys()`**

**`Object.values()`**

## **STRING**
**`String.substring()`**
* [link to MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring)


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