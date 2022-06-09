# REST

`GET`
* Used to retrieve information
* Data is sent via query string
* Information is plainly visible in the URL
* Limited amount of data can be sent

`POST`
* Used to post data to the server
* Data is sent via request body, not a query string
* Can send any sort of data (JSON)


* *form* element: 
  * *type* can be set to URL
  * *method* can be set to GET / POST

* *input* element: *name* used as the key in query string in URL

`REpresentational State Transfer (REST)`
* Set of guidelines for *how client and server should communicate with one another* and perform CRUD operations on a given resource

* Main idea is to treat data on the server-side as resources than can be CRUDed
  * **Resources:** some entities that are exposed/provided access to via HTTP

* Formatting the URLs and HTTP verbs in applications

* **CRUD**
  * *Create*
  * *Read*
  * *Undo*
  * *Delete*

`method-override`
* Only *GET* and *POST* requests can be sent from a form in the browser
* In order to send *PUT*, *PATCH* or other requests, **method-override** npm can be installed
* `**npm i method-override**

```js
// method-override using query string value
const express = require('express');
const methodOverride = require('method-override');
const app = express();

// '_method' query string 
//  whatever this is set to in the form, Express is going to treat it as that method
//   POST method treated as PATCH method
app.use(methodOverride('_method'));

// method override in HTML
<form method="POST" action="/resource?_method=PATCH">
```