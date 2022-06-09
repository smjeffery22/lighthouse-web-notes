# CRUD (LHL W3)

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

