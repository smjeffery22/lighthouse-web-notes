# **Jeffery Park's LHL Week 3 Notes**

## **Day 1 Lecture Notes**


## **Day 1 Compass Notes**

**List of HTTP Status Codes**
* Status codes are issued by a server in response to a client's request made to the server
  * The first digit of the status code specifies one of five standard classes of responses
* **1xx informational response:** the request was received, continuing process
* **2xx successful:** the request was successfully received, understood, and accepted
* **3xx redirection:** further action needs to be taken in order to complete the request
* **4xx client error:** the request contains bad syntax or cannot be fulfilled
* **5xx server error:** the server failed to fulfil an apparently valid request

### **Express**
* Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications
* Express is one of the most used web frameworks in the Node community

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
  * Route parameters are named URL segments that are used to capture the values specifed at their position in the URL
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
* Use `views` direcoty for template files
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
  * When 'template + variables' are specified in 'res.render', the variables are intepreted into the template
    * The template returns html, which is then sent to the browser
      * Call this server side rendering
        * Took a template and rendered out a string of html from it
  * EJS automatically knows to look inside the 'views' directory for any template files (.ejs)
* When sending variabls to an EJS template, they need to be inside an object
  * `res.render('urls_index', templateVars);'
    * passing templateVars to the templated called 'urls.index.ejs' file
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

### **CRUD**
* Four different actions that can be performed on data

| CRUD Action   | HTTP Method   | Description                      | JavaScript                                                 |
|---------------|---------------|----------------------------------|------------------------------------------------------------|
| Create        | POST          | Add a new record                 | users["5315"] = {first_name: "John", last_name: "Smith"}   |
| Read          | GET           | Retrieve the value of a record   | users["5315"]                                              |
| Update        | PUT           | Update a record's value          | users["5315"].first_name = "Jane"                          |
| Delete        | DELETE        | Delete a record                  | delete users["5315"]                                       |

* **Safe Methods**
  * A request method is safe if a request with that method has no intended effect on the server
    * GET, HEAD, OPTIONS, TRACE
  * Safe methods are intended to be read-only
    * Do not exclude side effects
  * Non-safe methods may modify the state of the server or have other effects
    * POST, PUT, DELETE, CONNECT, PATCH

* **Idempotent Methods**
  * A request method is idempotent if multiple identical requests with that method have the same intended effect as a single such request
    * PUT, DELETE and safe methods are idempotent
    * POST, CONNECT and PATCH are not idempotent
      * Multiples requests can be sent


### **body-parser**
* POST request has a body and when browser submits a POST request, the data in the request body is sent as a Buffer
  * This data type is not readable for humans
  * `body-parser` middleware is used to make this data readable
* The `body-parser` library will convert the request body from a Buffer into string that can we can read
  * Then add the data to the req (request) object under the key `body`
  * Saved in `req.body` object

* Middleware is a piece of software that sits in between the request and the response



## **Day 2 Lecture Notes**


## **Day 2 Compass Notes**

### **Nodemon**
* NPM package that monitors for any changes in the source and automatically restart server
* `npm install --save-dev nodemon`
* Add `"start": "./node_modules/.bin/nodemon -L express_server.js",` in `package.json` file
  * Run `npm start`

### **Cookies**
* An HTTP server can tell a client to remember certian keys-values ("cookies") using the `Set-Cookie` header in an HTTP response
* In all subsequent HTTP requests from the client to the server, these keys-values are included in the Cookie header
* HTTP cookies are small blocks of data created by a web sserver while a user is browsing a website
  * Placed on the suer's computer or other device by the user's web browser
  * Cookies are placed on the device used to access a website
* A cookie consits of the following components:
    1. Name
    2. Value
    3. Zero or more attributes (name-value pairs)
      * Attributes store information such as the cookie's:
        * expiration
        * domain
        * flags (such as Secure and HttpOnly)

### **cookie-parser**
* Serves as Express middleware that faciliates working with cookies
  * Helps read the values from the cookies
*`res.cookie(name, value [,options]):` set cookie name to value
  * value parameter may be a string or object converted to JSON

### **Git Branch**
* Source code can be sectioned off into their own versions
  * Make many different changes to the source, which can later be reviewed before being merged into the master version
  * Work on the code without effecting the master branch




## **Day 3 Lecture Notes**


## **Day 3 Compass Notes**





## **Day 4 Lecture Notes**
* Enryption can be decrypted
* Hashing cannot be reversed/shown

### **cookie-session**
* for encrypting
  * need to modify res.cookie
* 'res.cookie` => `req.session['user_id'] = user.id`
* `req.cookies` => `req.session`
* `req.clearCookie('user_id)` => `req.session['user_id'] = null`
  * doesn't clear the cookie and still there with different value (null)
  * to clear, `req.session = null`



### **morgan middleware**


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
* Passwords should not be encrypted, they should is **hashed**
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
      2. sotring an id in an encrypted cookie with a session store on the server-side
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

### **REST**
* REST is a set of conventions and practices in web development that deals with accessing and manipulating resources over HTTP
  * Resources can be an absraction of an object or data
    * Referenced using a URL (Uniform Resource Locator)
* https://www.restapitutorial.com/lessons/httpmethods.html
* In REST, Read is split into Browse and Read


| Action   | Application   | Description                         | HTTP Method        |
|----------|---------------|-------------------------------------|--------------------|
| Browse   | Collection    | brow the collection                 | GET                |
| Read     | Member        | read a member of the collection     | GET                |
| Edit     | Member        | edit a member of the collection     | PUT / PATCH        |
| Add      | Collection    | add a new member of the collection  | POST               |
| Delete   | Member        | delete a member of the collection   | DELETE             |



## **Day 5 Lecture Notes**


## **Day 5 Compass Notes**

### **DATA**
* Programming revolves around the data and we write software to retrieve, modify and display data
* The way data is stored and structured is very important
  * Determines how easily and efficiently retrieve, modify and display data

### **DATA STRUCTURE**
**Trees in Computer Science**
* Trees are a great data structure to use when data has hierarchical relationships

*Tree Structure*
![Tree](https://i.imgur.com/0DLZ1jI.png)

*Tree Structure - Root Node & Leaf Nodes*
![Tree-Root-Leaf](https://i.imgur.com/8vBfxBl.png)

*Tree Structure - Root Parent & Children Nodes*
![Tree-Root-Leaf](https://i.imgur.com/ZP7DACU.png)

*Tree Structure - Sibling Nodes*
![Tree-Root-Leaf](https://i.imgur.com/dldP3RM.png)

* Each circle in the tree is called a **node**
* Node represents a key entity and contains data about that entity
  * Node: employee - Data: employee's name
  * All the connections between the nodes are called **edges**
* Types of Node
  * **Root Node:** node at the *top*
  * **Leaf Nodes:** Nodes on the *very bottom*
  * **Parent Node:** nodes under Root Node
  * **Children Nodes:** Every node that is not a leaf node
  * **Sibling Nodes:** All chidlren nodes with the same parent

**Tree Treversal**
* To access a specific node within the tree

* **Breadth First Traversal:** Cheks the nodes closest to the root not before checking the noes that are further away
![Breadth-First-Traversal](https://i.imgur.com/eW8w8as.png)
  * Checks through each node, row by row, until found
  * Checks 1 first (root)
    * Then checkes 2 through 4 in order (root's children)
      * Then checks 5 through 12 in order (above nodes' children)
        * ...

* **Depth First Traversal:** Same concept as Breadth First Traversal, but try to visit the left nodes first
![Depth-First-Traversal](https://i.imgur.com/mY1NJKJ.png)


## **WE Compass Notes**

### **Stack**
* Stack oftern refers to the collection of technologies used in a given system
  * Web Server: Node.js
  * Middleware: Express
  * Template Engine: EJS
  * Database: None, just an "In-Memory Object"
* MEAN stack is a common stack nowadays
  * MongoDB
  * Express
  * Angular.js
  * Node.js
* Full-stack: Developers who are comfortable working with both back-end and front-end technologies
  * Front-end: What users see and interact with
    * HTML/CSS/JS
    * All the associated considerations on client-side (or in the browser)
  * Back-end: Server-side technologies
    * Web servers (Node.js)
    * Databases

### **HTML & CSS**
**HTML**
* Language of the web
* Has its own specific syntax-rules
* **Tag:** Basic language of HTML
  * Browser turns HTML tags into elements that form a tree
    * Through **Document Object Model (DOM)**
      * Standard convention for representing and interacting with elements in HTML
  * Each HTML tag creates an element in the DOM that the browser uses to display the page
    * Element is created from the starting tag to the ending tag
    * Each tag has a name or type that defines what kind of element will be created
      * Paragraph, image, document division
* Document written in HTML defines the **structure and content of the page**

```js
<tag>
  content
</tag>
```

**CSS**
* CSS is used to define the style
  * Uses specific syntax to change how elements look on the page
    * Color, position, fonts, etc.

```js
<h1 class='article'>

</h1>
```

* Three ways to add CSS rules to a page
  1. Directly to an element
      * `<p style="color: red"></p>`
  2. Inline with HTML using a `<style>` tag
      * `<style>` tag usually go inside the `<head>` tag
      * `<style> p { color: red; } </style>`
  3. **Linking to a CSS file using a `<link>` tag**
      * `<link rel="stylesheet" href="style.css">`

### IDs vs. Classes
* **ID:** Used to identify unique elements on a page
  * Target elements by id using a selector with a hashtag prefix `#buy-now-main-btn`
  * Either 0 or 1 elements that match this selector
  * An element can only have one ID
  * Ex. header, about
* **class:** Used to identify elements of the same type
  * Target elements by class using a selector with a period/dot prefix `.nav-item`
  * 0 to n elements that match this selector
  * These elements can occur anywhere
  * Classes imply **stylistic** or **behavioral** properties about an element
  * Ex. comment (when there are multiple comments)
* As a general rule, classes should be used much more frequently than IDs
  * IDs may be used for a unique element
    * Ex. An element that is styled and/or behaves very differently than other elements on a page or website
  * Classes for something reusable
  * However, do not use classes frequently if not necessary
* Phone's Barcode (class) vs. Serial Number (ID)
  * Same type of phone in the store has the same barcode
  * Each phone has its unique serial number

### DOM (Document Object Model)
* When a webpage is loaded, the browser runs a process that creates a DOM in memory
  * DOM represents all of the HTML code on that page
  * Node/DOM Node: each HTML element
* Transforms HTML text into a complete object structure

### Event Propagation
* The standard DOM Events describes 3 phases of event propagation:
  1. Capturing Phase: the event goes down to the element
  2. Target Phase: the event reached the target element
  3. Bubbling Phase: the event bubbles up from the element
  
**Bubbling**
* In nested elements, when an event happens on an element:
  * It first runs the handlers on it
  * Then on its parent
  * Then all the way up on other ancestors

```js
<form onclick="alert('form')">FORM
  <div onclick="alert('div')">DIV
    <p onclick="alert('p')">P</p>
  </div>
</form>
```
  * If 'p' is clicked, onclicks runs on 'p' -> 'div' -> 'form'
  * This process is called **bubbling**

`event.target`
* The most deeply nested element that caused the event is called a **target** element
  * Accessible as `event.target`
    * `event.target:` 'target' element that initiated the event
    * `this:` 'current' element

`event.stopPropagation()`
* Stops the move upwards, but on the current element, all other handlers will run

`event.stopImmediatePropagation()`
* Stop the bubbling and prevent handlers on the current element from running as well


### jQuery
* Events/actions constantly occur on a webpage
* Only notified of events if listening
  * Waiting for the browser to communicate that a specific event has occurred
    * Then tell the borwser how to react
* **Event handler:** To specify what to do when an event occurs using function
