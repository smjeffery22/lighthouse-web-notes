# Express

- Express is a framework for web development to *create servers using Node*
  - Start up a server to listen for requests
  - Parse incoming requests
  - Match those requests to particular routes
  - Craft http response and associated content

- On every incoming request, Express makes the two following objects:

  1. `req` object that represents the incoming request

     - **Express creates JS objects automatically by parsing the incoming HTTP request information and pass it in 'req' parameter**

     - When printed, it is a massive object with many properties
       - contains methods such as:
         - **req.app**
         - **req.params**
         - **req.body**
         - **req.query**

  2. `res` object that represents the outgoing response

     - **res.send()** sends the HTTP response

     - any time this is sent, the request is done
       - HTTP request cannot handle more than one response

     - **res.redirect(status, path)** redirects to the URL with specified status
       - if the path is not specified, it defaults to 302

- **Routing** refers to taking incoming requests and a path that is requested and matching that to some code in some response

- **app.use()** callback runs *every time there is incoming request*

- **app.get()** request and **res.send()** response

- Path parameter **/:pattern** used in app.get request is stored in **req.params**

  - Can have more than one path parameter in the request
    - Ex. **/:pattern/:patternTwo**

- Query **?key=value**, where *key=value* is query string and *?* is a separator
  - The key-value pair is saved in **req.query**

- **app.post()** sends request via request body (i.e. **req.body**)
  - req.body returns undefined and needs to be told how it should be parsed
    - Use Express built-in middleware:
      - **app.use(express.urlencoded({ extended: true}));**
        - Parses form-encoded information from the request body
      - **app.use(express.json());**
        - Parses incoming requests with JSON payloads

- **router.route()** to chain routes with the same path and different HTTP methods

```js
router.route('/:id')
	.get(catchAsync(campgrounds.showCampground))
	.put(isLoggedIn, isAuthor, validateCampground, catchAsync(campgrounds.editCampground))
	.delete(isLoggedIn, isAuthor, catchAsync(campgrounds.deleteCampground))
```

## Middleware

- Functions that **run** at some point during the **request/response lifecycle**
  - Runs between the time a request enters Express and by the time the response leaves and the code stops executing

- Each middleware has access to to the request/response objects
  - Can make changes to them
    - Ex. parsing form data and parsing JSON data with Express built-in middleware

- Middleware can **end the HTTP request** by sending back a response (i.. res.send())

- Middleware can be chained together, one after another by calling **next()**
  - **next()** is going to refer to the next middleware
    - It will be executing whatever the next matching middleware is

- Middleware can be included as the *second argument in route handler* to run it first
  - `app.post('/campgrounds', validateCampground, catchAsync(async (req, res, next) => {}`
  - Include *next()* in middleware to continue executing code after the middle is run

**express.static(root, [options]);**

- To serve static files such as images, CSS files and JS files
- Ex. **app.use(express.static('public'));**
  - To serve files in a directory named 'public'

**app.use(express.urlencoded({ extended: true}));**

- Parses incoming requests with *urlencoded (form-encoded) payloads* from the request body
  - Parses the req.body as urlencoded data

**app.use(express.json());**

- Parses incoming requests with *JSON payloads*

**morgan**

- Helps logging HTTP requests information to the terminal
  - Useful for debugging
  - Shows HTTP request methods, status, etc.

```js
const express = require('express');
const app = express();
const morgan = require('morgan');
const port = 3000;

app.use(morgan('tiny'));
```

### Writing Middleware

- Guide to writing middleware: https://expressjs.com/en/guide/writing-middleware.html

- **next()** executes the next middleware without executing the next line of code (code comes back to it)
  - If used with **return**, the next line of code does not get executed

- What is defined in the middleware can be used in other request methods coming after the middleware
  - Ex. req.requestTime to include date

- Setting up 404 error status
  - By putting app.use method at the end of the code
    - If none of the routes above this code are matched, this code will run

- Authentication screening prior to loading a page
  - Make a variable and pass it into as another callback function in app.get request
    - need to include `next()`
  - Router handler (i.e. app.get) can accept multiple callbacks

```js
app.use((req, res, next) => {
	console.log('This is my first middleware!!');
	next();
	console.log('This is my first middleware!! - After calling next()');
});

app.use((req, res, next) => {
	console.log('This is my second middleware!!');
	next();
	return next();
	console.log('This is my second middleware!! - After calling next()');
});

app.use((req, res, next) => {
	req.requestTime = Date.now();
	// console.log(req.method, req.path);
	next();
});

app.use((req, res) => {
	res.status(404).send('NOT FOUND!');
});

const verifyPassword = (req, res, next) => {
	const { password } = req.query;

	if (password === 'chicken') {
		next();
	}

	res.send('You need password!');
};
```

## Error Handling

- By default, Express comes with a built-in error handler that takes care of any errors that might be encountered in the app
  - This default error-handling middleware function is addded at the end of the middleware function stack

- **throw new Error()** to set a specific error message

- **app.use((err, req, res, new) => {})** to handle error
  - **error handling middleware**

- When an error is written, the _res.statusCode_ is set from _err.status (or err.statusCode)_
  - Ranges from 4xx to 5xx

# Templating (ejs)

- Templating allows to define a **preset "pattern"** for a webpage that can be dynamically modified

`Embedded Jave Script (ejs)`

- Need to install npm package 'ejs'
  - Set in Express using **app.set('view engine', 'ejs');**

- Need a directory called **views** in the project folder
  - Express assumes the ejs files are saved in this folder by default
  - Create **.ejs** files in this folder
    - HTML template

- **res.render('ejs_file_name')** Renders a view and sends the rendered HTML string to the cliet
  - No need to include the extension of the file
    - Pass as the second parameter (i.e. object) in **app.render('ejs_file_name', { variable_name (or key: value) });**
      - Whatever the _value_ is, it will be available in the template as _key_

- To set specific directory path for views folder:
  - **const path = require('path');**
  - **app.set('views', path.join(__dirname, '/views'))**
    - **__direname** is the current directory where the .js file is saved

- Whatever is put in the **ejs tags** will be treated as **JS**
  - Typically to use data from database in the template

- .ejs file should be kept as simple as possible (i.e. no complicated JS codes)
  - Write the code in .js file and use it in .ejs file
    - Pass as the second parameter (i.e. object) in **app.render('ejs_file_name', { variable_name (or key: value) });**
      - Whatever the _value_ is, it will be available in the template as _key_

`Partials`

- Way of including templates in other templates (duplicating codes)

```js
const express = require('express');
const app = express();
const port = 8080;

app.set('view engine', 'ejs');

// app.use((req, res) => {
//   console.log('Got a new request!');
//   res.send('Hello, this is the response!');
//   res.send({ color: 'red' });
//   res.send('<h1>This is my Webpage!</h1>');
// });

app.get('/', (req, res) => {
	res.render('home');
});

app.get('/rand', (req, res) => {
	const num = Math.floor(Math.random() * 10) + 1;
	res.render('random', { num });
});

app.get('/r/:subreddit/:postId', (req, res) => {
	const { subreddit, postId } = req.params;
	res.send(`<h1>Viewing ${postId} on the ${subreddit} subreddit!</h1>`);
});

app.get('/cats', (req, res) => {
	res.send('Meow!');
});

app.post('/cats', (req, res) => {
	res.send('Post request to /cats!');
});

app.get('/dogs', (req, res) => {
	res.send('Woof!');
});

app.get('/search', (req, res) => {
	const { q, color } = req.query;
	res.send(`Search results for: ${q}, ${color}`);
});

// default response to every other requests than the above
//  if placed in the beginning, this will run first and end since only one response at a time
app.get('*', (req, res) => {
	res.send('I do not know that path!');
});

// need to get a server going and listen
// need to have a port to listen on
app.listen(port, () => {
	console.log('Listening on Port 3000');
});
```
