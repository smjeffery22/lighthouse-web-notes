# HTTP & SERVER (LHL W2-W3)

## HTTP (HYPER TEXT TRANSFER PROTOCOL)
* Foundation of how the World Wide Web works
  * How we communicate and how we request and share resources or web pages
* Standardized sort of set of rules for how a form of communication should work

## CLIENT
* Computer that accesses a server
* Browser receives the response and renders the content for display
  * 'Right Click' - 'View Source Code'

## SERVER
* Computer that can satisfy requests on the Web
* Server receives requests and responds with instructions (i.e. code) that the browser can understand and display

1. Request from browser sent to the server
2. Request received by the server
3. Response sent from the server to the browser
4. Response received by the browser

## **Day 3 Compass Notes**

### **HTTP**

- _HyperText_ is text which contains link to other text
- **HTTP** (HyperText Transfer Protocol) is a protocol used to read and write resources (data) in a simple text-based manner
  - Request-response based protocol
    - Client makes a request to an HTTP server, sending a message asking for a specific resource
    - Server sends down as a response
      - Server cannot send a response if there is no request

### **HTTP Messages**

There are two types of HTTP messages, requests and responses, each with its own format

**Responses**
![alt text](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview/http_response.png)

- _Status code_
  - A three-digit number that the server puts in the response to let the client know whether or not the operation was successful
    - 200: "Everything went great!"
    - 201: "The request has succeeded and a new resource has been created as a result."
    - 404: "Resource was not found."
    - 500: "The server had an error."
- _Body_
  - The response will usually contain some data, such as the data the client originally requested
    - This data is stored in a part of the response (body)

### **URL**

**URL** (Uniform Resource Locator) is the mechanism used by browsers to retrieve any published resource on the web.

- The address of a given unique resource on the Web
- Each valid URL points to a unique resource
  - HTML pag, CSS document, image, etc.

![alt text](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL/mdn-url-all.png)
![alt text](https://raw.githubusercontent.com/DominicTremblay/w2d3-lecture/demo-east-nov23-2020/url.png)

- URL <=> postal mail address

  - domain name <=> city/town
  - port <=> zip code
  - path <=> building
  - parameters <=> extra info
  - anchor <=> person to whom mail is addressed to

- **API** (Application Programming Interface) is a software intermediary that allows two applications to talk to each other

## **Day 1 Compass Notes**

**List of HTTP Status Codes**
* Status codes are issued by a server in response to a client's request made to the server
  * The first digit of the status code specifies one of five standard classes of responses
* **1xx informational response:** the request was received, continuing process
* **2xx successful:** the request was successfully received, understood, and accepted
* **3xx redirection:** further action needs to be taken in order to complete the request
* **4xx client error:** the request contains bad syntax or cannot be fulfilled
* **5xx server error:** the server failed to fulfil an apparently valid request

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

### **Cookies**
* An HTTP server can tell a client to remember certain keys-values ("cookies") using the `Set-Cookie` header in an HTTP response
* In all subsequent HTTP requests from the client to the server, these keys-values are included in the Cookie header
* HTTP cookies are small blocks of data created by a web server while a user is browsing a website
  * Placed on the user's computer or other device by the user's web browser
  * Cookies are placed on the device used to access a website
* A cookie consists of the following components:
    1. Name
    2. Value
    3. Zero or more attributes (name-value pairs)
      * Attributes store information such as the cookie's:
        * expiration
        * domain
        * flags (such as Secure and HttpOnly)

### **cookie-parser**
* Serves as Express middleware that facilitates working with cookies
  * Helps read the values from the cookies
*`res.cookie(name, value [,options]):` set cookie name to value
  * value parameter may be a string or object converted to JSON