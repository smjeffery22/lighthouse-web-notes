# EXPRESS (LHL W3)

- Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications
- Express is one of the most used web frameworks in the Node community

**Routing**
* Routing refers to determining how an application responds to a client request to a particular endpoint, which is a URI (or path) and a specific HTTP request method (GET, POST, etc.)
  * ![alt text](https://www.researchgate.net/profile/Harri-Valkonen-2/publication/346585530/figure/fig4/AS:987488491417601@1612447011264/The-illustration-of-the-URL-URN-and-URI-26.png)
* `app.method(path, handler)`
  * **method:** HTTP request method
  * **path:** path on the server
  * **handler:** function executed when the route is matched

  ```js
      app.get('/', function (req, res) {
        res.send('Hello World!')
      })

      app.post('/', function (req, res) {
        res.send('Got a POST request')
      })
  ```

* **Route Parameters**
  * Route parameters are named URL segments that are used to capture the values specified at their position in the URL
  * Captured values are populated in the `req.params` object
    * Route parameters as keys

  ``` js
  Route path: /users/:userId/books/:bookId
  Request URL: http://localhost:3000/users/34/books/8989
  req.params: { "userId": "34", "bookId": "8989" }

  app.get('/users/:userId/books/:bookId', function (req, res) {
    res.send(req.params)
  })
  ```

* **Response Methods**
  * Methods on the response object (res) can send a response to the client, and terminate the request-response cycle

| Method           | Description         
|------------------|--------------------------------------------------------------------------------------|
| res.download()   | Prompt a file to be downloaded                                                       |
| res.end()        | End the response process                                                             |
| res.json()       | Send a JSON response                                                                 |
| res.jsonp()      | Send a JSON response with JSONP support                                              |
| res.redirect()   | Redirect a request                                                                   |
| res.render()     | Render a view template                                                               |
| res.send()       | Send a response of various types                                                     |
| res.sendFile()   | Send a file as an octet stream                                                       |
| res.sendStatus() | Set the response status code and send its string representation as the response body |

### **Template**
* **Templates** are files that define the presentation of a web app's data separately from the server logic
* Keep server logic (i.e. JS) separate from markup (HTML)
  * Easier to modify/debug one without affecting the other
* Separate different parts of an HTML document into different files
  * Keep the length of HTML files short and manageable
* **Template engine** is also needed in order to use template files
  * Replaces variables in a template file with actual data
  * Transforms the template into an HTML file sent to the client
  * i.e. Embedded JavaScript (EJS) templates

### **Embedded JavaScript (EJS)**
* EJS is a template engine for Express
* Use `views` directory for template files
* To set EJS as the view engine for Express:

```js  
// set the view engine to ejs
app.set('view engine', 'ejs');

// use res.render to load up an ejs view file

// index page
app.get('/', function(req, res) {
  // look in a 'views' folder for the view (equivalent to 'views/pages/index')
  res.render('pages/index');
});
```

* `res.render`
  * When 'template + variables' are specified in 'res.render', the variables are interpreted into the template
    * The template returns html, which is then sent to the browser
      * Call this server side rendering
        * Took a template and rendered out a string of html from it
  * EJS automatically knows to look inside the 'views' directory for any template files (.ejs)
* When sending variables to an EJS template, they need to be inside an object
  * `res.render('urls_index', templateVars);'
    * passing templateVars to the template called 'urls.index.ejs' file
    * Values stored in the templateVars object can be displayed in' urls.index.ejs' file
      * `<%= %>` syntax: to show the result of a code on the page (i.e. value of object)
      * `<% %>` syntax: to run code without displaying on the page (i.e. conditionals, loops)
* **Partials** are reused codes
* EJS partials can be embedded in another file using `<%- ... %>`
  * `<%- include('relative/path/to/file'); %>`
  * Relative to the current file
* A single variable can be echoed using `<%= ... %>`
  * `<%= tagline %>` Display the 'tagline' value on the page
* EJS partial has access to all the same data as the parent view
  * However, if a variable is referenced in a partial, it needs to be defined in every view that uses the partial

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <%- include('../partials/head'); %>
</head>
<body class="container">

<header>
  <%- include('../partials/header'); %>
</header>

<main>
  <div class="jumbotron">
    <h1>This is great</h1>
    <p>Welcome to templating using EJS</p>

    <h2>Variable</h2>
    <p><%= tagline %></p>
  </div>
</main>

<footer>
  <%- include('../partials/footer'); %>
</footer>

</body>
</html>
```

### **body-parser**
* POST request has a body and when browser submits a POST request, the data in the request body is sent as a Buffer
  * This data type is not readable for humans
  * `body-parser` middleware is used to make this data readable
* The `body-parser` library will convert the request body from a Buffer into string that can we can read
  * Then add the data to the req (request) object under the key `body`
  * Saved in `req.body` object

* Middleware is a piece of software that sits in between the request and the response

### **cookie-parser**
* Serves as Express middleware that facilitates working with cookies
  * Helps read the values from the cookies
*`res.cookie(name, value [,options]):` sets cookie name to value on every request
  * A cookie with name-value pair added to Inspect-Application-Cookies
  * value parameter may be a string or object converted to JSON
* Cookies can found in `req.cookies`
  * All cookies parsed and turned into an object
* *Signing:* to make sure the original data we sent to the client is the same data being sent back to the server
  * Included in `cookieParser('sign')`
  * `res.cookie('fruit', 'grape', { signed: true })`
    * Value is created with unique characters (signed)
    * `fruit-grape` cookie can only be read using `req.signedCookies`
    * If the value is changed manually, cannot be verified by cookie parser

```js
const express = require('express');
const cookieParser = require('cookie-parser');
const app = express();

app.use(cookieParser());

app.get('/greet', (req, res) => {
  // prints cookies in an object with name-value pairs
  console.log('---------',req.cookies);
  res.send('Hey!');
})

// sets cookies with name-value pairs
app.get('/setname', (req, res) => {
  res.cookie('name', 'bori');
  res.cookie('animal', 'dog');
  res.send('Sent you a cookie');
})

app.listen(3000, () => {
  console.log('Serving on Port 3000');
})
```

### **cookie-session**
* in every route, session property available on every request
* cookie session id is created using `app.use(session())`
  - default *store* is MemoryStore
    - not for production
  - *resave* typically set to false
  - *saveUninitialized* 
* for encrypting
  * need to modify res.cookie
* 'res.cookie` => `req.session['user_id'] = user.id`
* `req.cookies` => `req.session`
* `req.clearCookie('user_id)` => `req.session['user_id'] = null`
  * doesn't clear the cookie and still there with different value (null)
  * to clear, `req.session = null`
    * `req.session.destroy()`

```js
const sessionConfig = {
	secret: 'thisissecret',
	resave: false,
	saveUninitialized: true,
}
app.use(session(sessionConfig))
```

### **uuid**
* randomly generate string code (i.e. abcde-fghij-klmnop)

### **bcryptjs**
* for hashing
  * salt adds extra password to it
    * `const salt = brycpt.genSaltSync(10)`
* should use async version because sync version take a long time
  * for simplicity, use sync version
    * bcrypt.hashSync('entered password', salt)
* `bcrypt.compare`
  * to compare password

## **Day 4 Compass Notes**

### **Storing Passwords Securely**
* Passwords should not be encrypted, they should be **hashed**
* **Encryption** is a **reversible process**
  * When passwords are encrypted, the secret key will be on the server
  * Passwords can be encrypted if the server is compromised
* **Hashing** is a one-way process
  * Password can be converted to some string, but **never be reversed**
  * Log-in password can be checked against the stored hash for checking
  * **bcryptjs** for hash algorithm

**bcryptjs**
* `npm install bcryptjs`

```js
const bcrypt = require('bcryptjs');
const password = "purple-monkey-dinosaur";
const hashedPassword = bcrypt.hashSync(password, 10); // hashes the password
```

### **Switching to Encrypted Cookies**
* **Session** in web development:
  * *Session Cookies:* cookies that expire after a browser is closed
  * *User Session:* 
    * login/logout features on a site
    * the event of a user using an application
  * *Session:* 
    * encrypted cookies
    * abstraction that refers to user data, can be tracked in various ways:
      1. storing data in an encrypted cookie
      2. storing an id in an encrypted cookie with a session store on the server-side
* Encrypting cookie is one way to make the data in the cookie safe
  * *AES.encrypt* -> Encrypt the value using the AES cipher and some *secret key*
    * Set the result as the cookie (*digest*)
  * *AES.decrypt* -> Process can be reversed
    * Digest + Secret => Original

| Original   | + | Secret            | => | Digest                                                             |
|------------|---|-------------------|----|--------------------------------------------------------------------|
| '20125'    |   | 'some-long-secret |    | 'TsilV4GR5EPE9UfDcoGxSnktN6cbu8tosao856vXMz3Z9bH6CENpw/Y0asyS/BBr' |          

**cookie-session Middleware**
* `npm install cookie-session`

```js
const cookieSession = require('cookie-session')

app.use(cookieSession({
  name: 'session',
  keys: ['key1', 'key2']

  // Cookie Options
  maxAge: 24 * 60 * 60 * 1000 // 24 hours
}));
```