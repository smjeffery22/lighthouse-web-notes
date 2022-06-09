# Async

## Call Stack

* Can think of it as a "todo list" of function invocations
  * First invoked function at the bottom of the stack
  * Most recently invoked function at the top of the stack
  * Stack is processed from the top to bottom

* Mechanism the JS interpreter uses to keep track of its place in a script that calls multiple functions

* How JS knows what function is currently being run and what functions are called from within that function, etc.

* When a script calls a function, the interpreter adds it to the call back
  * Starts carrying out the function
    * Any functions that are called by that function are added to the call stack further up
      * Once the current function is finished, the interpreter takes it off the stack
        * Resumes execution where it left off in the last code listing

## JS is Single Threaded

* At any given point in time, that single JS thread is running at most one line of JS code
  * Running at most one line at a time
    * No multitasking

* The Browser runs the code while JS runs other codes one line at a time
  * The Browser can do certain tasks that JS cannot do
    * Browsers come with **Web APIs** => able to handle certain tasks **in the background**
      * Tasks such as making requests or setTimeout
      * The call stack in JS recognizes such Web API functions and pass them to the Browser
        * Added back to the call stack one they are finished

## Promise

* An object representing the eventual completion or failure of an synchronous operation
  * Returned object to which you attach callbacks, instead of passing callbacks into a function 
  
* Promise is in one of these states:
  1. *pending:* initial state, neither fulfilled nor rejected
  2. *fulfilled:* meaning that the operation completed successfully
  3. *rejected:* meaning that the operation failed

### Basic Promise Syntax
  ```js
  const fakeRequestPromise = (url) => {
    return new Promise((resolve, reject) => {
        const delay = Math.floor(Math.random() * (4500)) + 500;
        setTimeout(() => {
            if (delay > 4000) {
                reject('Connection Timeout :(')
            } else {
                resolve(`Here is your fake data from ${url}`)
            }
        }, delay)
    })
  }

  // function continues on only if fulfilled
  // if rejected, falls to catch
  // data comes from the function
  //  resolve(`Here is your fake data from ${url}`)
  //  reject('Connection Timeout :(')
  fakeRequestPromise('yelp.com/api/coffee/page1')
    .then((data) => {
        console.log('It worked!! (1st)');
        console.log(data);
        return fakeRequestPromise('yelow.com/api/coffee/page2')
    })
    .then((data) => {
        console.log('It worked!! (2nd)');
        console.log(data);
        return fakeRequestPromise('yelow.com/api/coffee/page3')
    })
    .then((data) => {
        console.log('It worked!! (3rd)');
        console.log(data);
    })
    .catch((data) => {
        console.log('Error!!');
        console.log(data);
    })
  ```

  ### Creating New Promise
  ```js
  // starts with 'new Promise' followed by a callback function with two parameters
  //  resolve: resolves the promise
  //  reject: reject the promise
  const fakeRequest = (url) => {
    return new Promise((resolve, reject) => {
        const rand = Math.random();
        setTimeout(() => {
            if (rand < 0.7) {
                resolve('Here is your fake data!');
            }
            reject('Fake request error!');
        }, 1000)
    })
  };
  ```

## Async Functions
* Newer and cleaner syntax for working with async code
  * Made on top of promises

`**Async**`
* Async functions *always return promise*
  * If the function returns a value:
    * Promise resolved with that value
      * **return ...**
  * If the function throws an exception:
    * Promise will be rejected
      * **throw new Error(...)**
      * **throw ...**

```js
const login = async (username, password) => {
    if (!username || !password) throw 'Missing Credentials'
    if (password === 'corgifeetarecute') return 'Welcome!'
    throw 'Invalid Password';
}

login('smjeffery', 'corgifeetarecute')
    .then(msg => {
        console.log('Logged In!');
        console.log(msg);
    })
    .catch(err => {
        console.log('Error!');
        console.log(err);
    })
```
    
`**Await**`
* Allows to writer async code that looks like sync
* Pause the execution of async function and *wait for promise to be resolved*

```js
// waits for each function to be executed before proceeding with the next one
async function rainbow() {
    await delayedColorChange('red', 1000);
    await delayedColorChange('orange', 1000);
    await delayedColorChange('yellow', 1000);
    await delayedColorChange('green', 1000);
    await delayedColorChange('blue', 1000);
    return 'Done!';
}

// function returns promise
//  function executes then the next one gets executed
rainbow().then((data) => console.log('End of Rainbow', data));

async function printRainbow() {
    await rainbow();
    console.log('End of Rainbow');
}

// wait for rainbow function to be executed first then console-logs
printRainbow();
```

`**Handling Error**`
* Using **try** and **catch** within async function

```js
const fakeRequest = (url) => {
    return new Promise((resolve, reject) => {
        const delay = Math.floor(Math.random() * (4500)) + 500;
        setTimeout(() => {
            if (delay > 4000) {
                reject('Connection Timeout :(')
            } else {
                resolve(`Here is your fake data from ${url}`)
            }
        }, delay)
    })
}

async function makeTwoRequests() {
    try {
        let data1 = await fakeRequest('/page1');
        console.log(data1);
        let data2 = await fakeRequest('/page2');
        console.log(data2);
    } catch (e) {
        console.log('Caught error:', e);
    }
}

makeTwoRequests();
```