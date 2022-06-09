# Difference Between Cookies, Sessions and Tokens

## Cookies (client side)
* Used to remember information about the user in order to show the saved information/settings
  * Adds statefulness to HTTP
* How servers can put data on the user's browser to remember things about the user
  1. Browser makes a request to the server
  2. Server responses with the data the user is looking for
    * Server can give the browser some cookies to save
    * Once the cookies are in the browser, every time the user goes to the website, the cookies are also sent with the request
* Cookies are limited by the domain
  * Ex. All the cookies that are given by YouTube are only going to be sent to YouTube
* Cookies have expiry date depending on the server
* Cookies are used to remember all sorts of things
  1. Change the language to a website
  2. Server gives a cookie that will remember the language
  3. Next time the user visits the page, the cookie will be sent to the server along with the request
  4. Server will give the user a page with the saved language
* Limitations:
  * Limited number of cookies that can be stored
  * Size of each cookie is limited (info it can store)

## Sessions (server side)
* Adding statefulness to HTTP
  * Save and share information from one request to the next
* HTTP, the protocol that we use to go to the website, is **stateless**
  * Meaning that every request that goes to the server is treated independently from the previous one
    * There is no link between requests and the server forgets everything after the request is finished
      * Need to remind the server and one way to do this is by using **session**
* After the user inputs ID/Password, the server creates a record in session database (session DB) for the user
  * The session will have a unique ID
* The session ID will be sent back to the browser using cookies
  * Cookies are sort of transportation method to carry session ID
  * Cookies only exist in browser
* Server will see that cookies are coming in with session ID
  * Server will check the session DB to check for the session ID
    * Server does not know who the user is until this check is done
* All the information about the user is on the server side in the DB
  * User only has the session ID
* Server has to use the DB resources to keep track of all the users that are logged in
  * For every request that comes in, the server has to receive the cookies, look at the session ID and search for the session ID for the user
  * More users => more DB the server needs

## Tokens (JWT)
* JWT is a token format
  * If JWT is used to authenticate users, there is no need to have session's DB in the server
    * Server does not need to work that hard to authenticate the user
* Tokens are strings that are received from the server and sent on every request (server remembers tokens)
* Instead of creating a session DB, the server will take the ID of the user and sign it using signature algorithm
  * Server will send a signed information as a string (a very long string)
* Tokens/signed information are sent to the server with requests
  * Server verifies if the signature is valid (i.e. not modified)
    * If valid, the server can identify the user
* JWT is signed, but not encrypted
  * Not used for secret information
  * The point is to sign the token and verify that no one has modified it

## Sessions vs. Tokens (JWT)
`Sessions`
  * Server keeps track of all the users that are logged in in the session DB
  * Allows to create new features since the server is keeping track of who is logged in (have session DB)
    * Force log out (delete session ID from DB)
    * Keeping track of all the devices that the user logged in from
    * Limit the amount of people who are logged in
  * However, to do the above, need to have DB and more DB will be needed as users grow
    * Higher cost and maintenance

`Tokens (JWT)`
  * All the server knows is if the token is valid or not
  * No need to have a DB, but cannot have features like sessions
    * Tokens are valid as long as they have not expired
  * Sign data => give data to the user => verify if data has been modified or not when receiving back
    * All without DB
    * Ex. Checking in using QR code (i.e. ID checking)
  
