# **Jeffery Park's LHL Week 2 Notes**

## **Day 1 Lecture Notes**
`module.exports` is a variable/empty object so to export multiple functions in one file, the functions need to be stored in object/array format.\
When requiring a file, the whole file is brought in so any `console.log`s will get printed.\

`npmjs.com` is like Amazon of npm where you can download codes that other people posted!\

## NPM
* `npm init`
  * to initialize npm in the directory
  * creates package.json file
  * enter through for default or `npm init -y`
  * now can add other people's codes
* don't recommend installing globally
  * npm install --global mocha
* instead, install directly in the project
  * npm install --save-dev mocha
    * development dependency: only used for development purpose
* installing mocha installs not only mocha, but also other codes that mocha depends on (dependencides)
  * dev-dependencies don't get installed (optional)
    * ex. chai

### Mocha
* test to see if your code passed or not
* `describe()` and `it()` are built-in functions in mocha
* `describe()` describes the test (optional)
  * `describe("description", () => {})`
* `it()` is the test
  * `it("what it should do", () => {})`
  
  `throw new Error("error message")`

### Chai
* **assertion library** for mocha
* `const chai = require('chai'); && const assert = chai.assert;` === `const assert = require('chai').assert`

### Ignoring Files/Folders
* we don't want to add node_modules folder into our git since it's too large and unnecessary
* `touch .gitignore`
  * go into the file and include node_modules
  * `git status` will exlude node_modules

### TDD (Test Driven Development)
* we write the tests first
* then we code
* Red: all tests are failing
* Green: write the minimum amount of code to make the test pass

## **Day 1 Compass Notes**
**Asynchronous programming** is when a unit of work is run separately from the main thread of the program and notifies the program of its completion.

### setTimeout
**setTimeout** is used to delay the execution of some code to later. We specify the code via a callback and the delay in ms.
* setTimeout(callback, delay)

Almost all web applications (websites) in like to schedule something to occur a bit later on their webpage(s) and therefore use **setTimeout**
* Show a notice to the user and then automatically hide it after a few seconds
* Try to reconnect after # seconds
* Open an in-browser chat buttom after a few seconds
* Website asking to disable Adblocker after a few seconds

## **Day 2 Lecture Notes**
### **fs library**
`fs` (file system) is a library in node.js

`fs.readFile(filename, encoding, callback_function)`

`const fs = require("fs")`

Example:
```js
fs.readFile('/Users/joe/test.txt', 'utf8' , (err, data) => {
  if (err) {
    console.error(err)
    return
  }
  console.log(data)
})
```
* 

### **request library**
Request brings in a website

`npm install request`

`const request = require("request");`

`request("URL", function(error, response, body) => {})`

## **Day 2 Compass Notes**
`setTimeout(() => {}, delay in ms)`
* Even if the delay is set to 0, still gets put into background thread first then get executed
  * Other codes (non-delayed ones) get executed first

`setInterval(() => {}, delay in ms)`


`process.stdout`
* *stdout* is for "standard output"
* `process.stdout.write()`: print in one line
  * as opposed to console.log, which prints each console.log in new line)

`process.stdin`
* *stdin* is for "standard input"
* `process.stdin.on()`
  * `on` method is used on `stdin` to register a callback
    * Run any time the user provides input to the program
    * Commonly used for registering callbacks to handle events

Example:
```js 
process.stdin.on('data', (key) => {
  process.stdout.write('.');
});
```
* Callback function is called each time there is new user input data and "." is printed to the screen

## **Day 3 Lecture Notes**

### SERVER
Back-end server\
`port:` anything above 1024 is temporary (don't need admin)

`const server = net.createServer()`
* `.createServer()` is a factory function
* Created a server

`server.listen(port, function() {})`
* Have the server listen to a particular port for incoming connections

`server.on('connection', function(client) {})`
* `.on` is a function that sets up an event listener
  * "on connection, do callback function"
* `'connection'` is an event
* callback function runs whenever connection event occurs in the server
* `client` is an object

### CLIENT
Front-end
```js
const client = net.createConnection({
  host: 'localhost',
  port: port
})
```
* `.createConnection()` is a factory function
* Connecting to a certain port number (port) on a certain computer (host)

`client.on('connect', function() {})`
* `connect` is an event; callback function runs when the event occurs

`client.on('data', function() {})`
* `data` is an event; callback function runs when the event occurs
* How the client received data from the server

`client.setEncoding('utf8')`
* Variable-width character encoding used for electronic communication

## **Day 3 Compass Notes**

### **HTTP**
* *HyperText* is text which contains link to other text
* **HTTP** (HyperText Transfer Protocol) is a protocol used to read and write resources (data) in a simple text-based manner
  * Request-reponse based protocol
    * Client makes a request to an HTTP server, sending a message asking for a specific reousrce
    * Server sends down as a response
      * Server cannot send a response if there is no request

### **HTTP Messages**
There are two types of HTTP messages, requests and responses, each with its own format

**Requests**
![alt text](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview/http_request.png)
* *Method (verb):*
  * What method it would like to perform
  * GET: used to "get" some data from the server
  * POST: usually used to create some new data
  * PUT: generally used for editing existing data on the server
  * DELETE: used to delete some existing data
* *Path*
  * What resource the client wants to act on
  * The path of the resource to fetch
    * The URL of the resource stripped from elements that are obvious from the context

**Responses**
![alt text](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview/http_response.png)
* *Status code*
  * A three-digit number that the server puts in the response to let the client know whether or not the operation was successful
    * 200: "Everything went great!"
    * 201: "The request has succeeded and a new resource has been created as a result."
    * 404: "Resource was not found."
    * 500: "The server had an error."
* *Body*
  * The response will usually contain some data, such as the data the client originally requested
    * This data is stored in a part of the response (body)


### **URL**
**URL** (Uniform Resource Locator) is the mechanism used by browsers to retrieve any published resource on the web.
* The address of a given unique resource on the Web
* Each valid URL points to a unique resource
  * HTML pag, CSS document, image, etc.
  
![alt text](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL/mdn-url-all.png)
![alt text](https://raw.githubusercontent.com/DominicTremblay/w2d3-lecture/demo-east-nov23-2020/url.png)
* URL <=> postal mail address
  * domain name <=> city/town
  * port <=> zip code
  * path <=> building
  * parameters <=> extra info
  * anchor <=> person to whom mail is addressed to

* **API** (Application Programming Interface) is a software intermediary that allows two applications to talk to each other

## **Day 4 Lecture Notes**

### Promise
* Promise is a JS object that will (hopefully) resolve to a value in the future
  * Used in anything asynchronous
    * Anything that takes non-zero amount of time
* Pending
  * Sitting in the pending state until it is resolved
* Fulfilled/Resolved
* Failed/Rejected
* `.then(() => {}):` Get the value back from promise as soon as it is resolved 

```js
myPromise
  .then((value) => {
    console.log(value);
  });
```

* `.catch(() => {}):`

```js
myPromise
  .catch((err) => {
    console.log(err);
  });
```
* `Promise.all():` Grab all promises together and turn them into one promise
  * Only works if all promises are resolved

## **Day 4 Compass Notes**

### JSON
JSON (JavaScript Object Notation) is a data format that underpins many modern web services and it a subset of the JS language.
JSON is built on two strcuctures:
* A collection of name:value pairs
* An ordered list of values

``` js
{
  "name": "New York City",
  "boroughs": [
    "Manhattan",
    "Queens",
    "Brooklyn",
    "The Bronx",
    "Staten Island"],
  "population": 8491079,
  "area_codes": [212, 347, 646, 718, 917, 929],
  "position": { "lat": 40.7127, "lng": -74.0059 }
}
```
* Keys are always double-quoted "strings"
* Values can be numbers, strings, objects, arrays, booleans and null

**Serialization**
The process of serialization coverts objects (or data structures) into a format that can be stored or transmitted between computers (typically as a string of text)
* Opposite is deserialization (string -> object)

`JSON.parse():` Parse a string as JSON, optionally transform the produced value and its properties, and return the value.

`JSON.stringify():` Return a JSON string corresponding to the specified value, optionally including only certain properties or replacing property values in a user-defined manner.

``` js
const jsonString = '{"a": 1, "b": 2, "foo": "bar"}';
const obj = JSON.parse(jsonString);
  // obj = { a: 1, b: 2, foo: "bar"}
const obj2 = JSON.stringify(obj);
  // obj2 = '{"a": 1, "b": 2, "foo": "bar"}'
```

### **Promise**
* A promise represents the **eventual result** of an asynchronous operation
  * Promise is an **object**

* Similar to callbacks, promise is a way of dealing with asynchronous codes:
  * When we don't know when things are going to happen in what order
  * More powerful than callbacks because they compose

* A promise needs two callback functions
  * one for success (resolve)
  * one for failure (reject)

```js
Promise((resolve, reject) => {});
```

**Benefits of Using Promise**
* Error handling becomes much simpler
* Asynchronous code becomes easier to unit test

**`.then`**
* Primary way of interaction with a promise
* Registers callbacks to receive either a promise's eventual value or the reason why the promise cannot be fulfilled

## **Day 5 Compass Notes**

### **Object Oriented Programming (OPP)**
* Probably the biggest concept in software development philosophy
* Object Orientation is a way of writing code that:
  * encourages **modularity**
  * **reduces duplication** through the use of objects
* `Object` is a collection of **key-value pairs** known as **properties**
  * Each key-value pair is a **state**
  * When a property's value is a **function**, it is called a **method**
  * Method is also known as the object's **behaviour**
* `this` is used inside an object whenever a method is accessing a prperty or another method on the same object

```js
const dog = {
  sound: "woof",
  speak: function() {
    console.log(this.sound);
  },
  teachMeSomething: function() {
    if (dog === this) {
      console.log('dog === this');
    }
    this.speak();
  }
};

dog.teachMeSomething();
```

### **OOP Part 1: Classes & Instances**
* **Classes** is a way to perform Object Orientation
* JS's object system is based on another pattern known as *prototypes*
  * Classes were added to JS in ES6
* In OPP, classes are blueprints (templates) that we use to create instances of objects
  * Class describes what the object is going to be
  * New object can be created using the class

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
};
let pizza1 = new Pizza("large", "cheese");
let pizza2 = new Pizza();
```

* To declare a class, use `class` keyword along with its name
  * Class name should be a noun
  * First letter of the class name should be capitalized
* New objects can be created from a class using `new` keyword
  * pizza1 and pizza2 are **instances** of the Pizza class
* `constructor` and `addTopping` are *methods*
  * `constructor` gets executed when an object instance is created from a class
    * Default values for an object
    * Since it's a method, values can be passed into it
* `toppings` is a *property*

### **OOP Part 2: Inheritance**
* Classes can share multiple of the same properties
* The duplication can be moved to another class
* `Interitance` techqnique allows to build a new class based on an existing class

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

* *Student* and *Mentor* inherit behaviour and state information from *Person* using the keyword `extends`
  * Person is the **superclass**
  * Student and Mentor are **subclasses** of the Person class
    * They are *extensions* of Person class

### **OOP Part 3: Super**
* `super` keyword allows subclasses to have a reference on the parent class
  * **method overring:** when a subclass implements a method that already exsits in the superclass
  * Avoid repeating code that is already present in the superclass

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

const bob = new Mentor('Bob Ross', 'I like mountains way too much');
console.log(bob.bio());
```

### **OPP Part 4: Getters and Setters**
* `Getters:` a method used to get the value of a property
* `Setters:` a method used to set the value of a property
* Benefits of using getters and setters
  * **Validating** data before assigning it to a property
  * **Computing** a value on the fly instead of simply pulling it out of a property

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
    return basePrice + (this.toppings.length * toppingPrice);
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
* In JS, properties cannot be made private
  * Simply add `_` to the start of a property name
    * Letting other developers know that the property should not be accessed directly (outside the class)
    * ```js
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
* Each class should be responsible for a single part of the functionality
* Inheritance


## **WE Compass Notes**

### **Promise**
* Promise is a try-catch wrapper around code that will finish at an unpredictable time
* Four keywords related to promise
  * **Fulfilled (Resolved):** It worked
  * **Rejected:** It did not work
  * **Pending:** Promise has not fulfilled or rejected
  * **Settled:** Promise has fulfilled or rejected
* What will happen when asynchronous task settles
* Promise can only settle once

```js
new Promise(function(resolve, reject) {
  resolve("hi"); // works
  resolve("bye"); // can't happen a second time
});
```

```js
new Promise(function(resolve, reject) {
  let value = doSomething():
  if(thingWorked) {
    resolve(value); // Resolved => value gets passed to .then
  } else if (somethingWentWrong) {
    reject(); // Rejected => .catch executed
  }
}).then(function(value) {
  return nextThing(value);
}).catch(rejectFunction);
```
* Resolve leads to the next .then
* Reject leads to the next .catch

### **Command Line cURL**
* cURL is a command line utility that is used to make HTTP requests to a given URL and it outputs the response
  * Allows to see the URL

**[15 Practical Linux cURL Command Examples (cURL Download Examples)](https://www.thegeekstuff.com/2012/04/curl-examples/)**
1. Download a Single File
    * `curl http://www.centos.org`
      * Content of the URL will be displayed in the terminal
    * `curl http://www.centos.org > centos-org.html`
      * Store the output in a file (centos-org.html)

2. Save the cURL Output to a File
    * Save the result of the curl command to a file by using -o/-O options
      * -o (lowercase o) the result will be saved in the filename provided in the command line
      * -O (uppercase O) the filename in the URL will be taken and it will be used as the filename to store the result
    * `curl -o mygettext.html http://www.gnu.org/software/gettext/manual/gettext.html`
      * The page will be saved in the file(mygettext.html)
    * `curl -O http://www.gnu.org/software/gettext/manual/gettext.html`
      * The page will be saved in the file (gettext.html)

3. Fetch Multiple Files at a Time
    * `curl -O http://www.gnu.org/software/gettext/manual/html_node/index.html -O http://www.gnu.org/software/gettext/manual/gettext.html`
      * `curl -O URL1 -O URL2`
      * Download index.html and gettext.html

4. Follow HTTP Location Headers with -L Option

5. Continue/Resume a Previous Download
    * `curl -C - -O http://www.gnu.org/software/gettext/manual/gettext.html`
      * '-C -' will find from where to start resuming the download
      * 'Ctrl + C' stops the download

6. Limit the Rate of Data Transfer

7. Download a File Only If It Is Modified before/After the Given Time
    * `curl -z 21-Dec-11 http://www.example.com/yy.html`
      * Download if modified later than the given date/time
    * `curl -z -21-Dec-11 http://www.example.com/yy.html`
      * Download if modified befoe the given date/time

8. Pass HTTP Authentication in cURL

9. Download Files from FTP Server
    * `curl -u ftpuser:ftppass -O ftp://ftp_server/public_html/xss.php`
      * Download xss.php from the ftp server
    * `curl -u ftpuser:ftppass -O ftp://ftp_server/public_html/`
      * List all the files and directories under the URL

10. List/Download Using Ranges
    * `curl ftp://ftp.uk.debian.org/debian/pool/main/[a-z]/`
      * List all the packages from a-z ranges

11. Upload Files to FTP Server
    * `curl -u ftpuser:ftppass -T myfile.txt ftp://ftp.testserver.com`
    * `curl -u ftpuser:ftppass -T "{file1,file2}" ftp://ftp.testserver.com`
      * '-T' is used to upload files to the FTP server
      * Upload a file or multiple files to the FTP server

12. More Information using Verbose and Trace Option

13. Get Definition of a Word using DICT Protocol

14. Use Proxy to Download a File

15. Send Mail using SMTP Protocol


### **Character Encoding**
* Character encoding provides a key to unlock the code


### **DNS (Domain Name System)**
* DNS is used to translate human-memorable domain names (example.com) and hostnames into the corresponding IP addresses
* Without DNS, internet will collapse

#### **Record Types**
* `A:` Most common, map a hostnames to IP address (IPv4, 32-bit address)
* `NS:` Name Server that is responsible for a DNS zone
* `MX:` Mail Exchange record specified where email gets sent to
* `CNAME:` Canonical Name, an alias for another hostname
* `AAAA:` Similar to A, but uses IPv6, 128-bit address

#### **Dig - DNS Lookup Utility
* `dig +trace google.com` in the command line
  * Returns four request-response stages
  1. Root Name Servers - (*.root-servers.net)
      * Name server for the root zone of the DNS of the Internet
      * Answers requests for records in the root zone
      * Answers other requests by returning a list of the authoritative name servers (ANS) for the appropriate TLD
    * First step in resolving human-readable host names into IP addresses that are used in communication between Internet hosts 
  2. .com Top Level Domain (TLD) - (*.gtld-servers.net)
      * TLD names are installed in the root zone of the name sapce
      * TLD for 'www.example.com' is '.com'
  3. google.com Name Servers (NS) - (ns*.google.com)
      * Server component of the DNS
      * NS record delegates a DNS zone to use the given authoritative name servers
  4. Address Records (A) - (address)
      * IP addresses listed in the address records are servers hosing the domain

### **Express**
* Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications
* Express is one of the most used web frameworks in the Node community

