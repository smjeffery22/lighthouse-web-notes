# ASYNCHRONOUS (LHL W2)

## **Day 1 Compass Notes**

**Asynchronous programming** is when a unit of work is run separately from the main thread of the program and notifies the program of its completion.

### setTimeout

**setTimeout** is used to delay the execution of some code to later. We specify the code via a callback and the delay in ms.

- setTimeout(callback, delay)

Almost all web applications (websites) in like to schedule something to occur a bit later on their webpage(s) and therefore use **setTimeout**

- Show a notice to the user and then automatically hide it after a few seconds
- Try to reconnect after # seconds
- Open an in-browser chat buttom after a few seconds
- Website asking to disable Adblocker after a few seconds

## **Day 2 Lecture Notes**

### **fs library**

`fs` (file system) is a library in node.js

`fs.readFile(filename, encoding, callback_function)`

`const fs = require("fs")`

Example:

```js
fs.readFile("/Users/joe/test.txt", "utf8", (err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});
```

### Promise

- Promise is a JS object that will (hopefully) resolve to a value in the future
  - Used in anything asynchronous
    - Anything that takes non-zero amount of time
- Pending
  - Sitting in the pending state until it is resolved
- Fulfilled/Resolved
- Failed/Rejected
- `.then(() => {}):` Get the value back from promise as soon as it is resolved

```js
myPromise.then((value) => {
  console.log(value);
});
```

- `.catch(() => {}):`

```js
myPromise.catch((err) => {
  console.log(err);
});
```

- `Promise.all():` Grab all promises together and turn them into one promise
  - Only works if all promises are resolved

### **Promise**

- A promise represents the **eventual result** of an asynchronous operation

  - Promise is an **object**

- Similar to callbacks, promise is a way of dealing with asynchronous codes:

  - When we don't know when things are going to happen in what order
  - More powerful than callbacks because they compose

- A promise needs two callback functions
  - one for success (resolve)
  - one for failure (reject)

```js
Promise((resolve, reject) => {});
```

**Benefits of Using Promise**

- Error handling becomes much simpler
- Asynchronous code becomes easier to unit test

**`.then`**

- Primary way of interaction with a promise
- Registers callbacks to receive either a promise's eventual value or the reason why the promise cannot be fulfilled

### **Promise**

- Promise is a try-catch wrapper around code that will finish at an unpredictable time
- Four keywords related to promise
  - **Fulfilled (Resolved):** It worked
  - **Rejected:** It did not work
  - **Pending:** Promise has not fulfilled or rejected
  - **Settled:** Promise has fulfilled or rejected
- What will happen when asynchronous task settles
- Promise can only settle once

```js
new Promise(function (resolve, reject) {
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

- Resolve leads to the next .then
- Reject leads to the next .catch

