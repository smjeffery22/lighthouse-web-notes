# AJAX and API's

## AJAX (Asynchronous Javascript And XML)

  * Making requests to load/send information behind the scenes interacting with a server

## API (Application Programming Interface)

  * Interface for one computer to interact/communicate with another piece of software

  * **Web APIs** are web (HTTP) based
    * Interface that occurs over HTTP
    * Requests are made to particular URLs (endpoints)

  * Can make requests to an API and get a response
    * Fetching BTC price from API

## JSON (Java Script Object Notation)

  * Format for sending data

  * Way of formatting data that is consistent and predictable

  * Similar to JS object, but:
    * key has to be in quotation
    * does not accept certain values such as undefined

  * Data received from API is a giant **string**
    * **JSON.parse()** to convert the string data to JS object
    * **JSON.stringify()** to convert the JS object to JSON string
      * to send to API
      * all instances of *undefined* are replaced with *null*

## Query Strings

  * Query strings are information that can be provided to any URL or as part of a URL that usually is going to impact what is returned
    * https://api.tvmaze.com/singlesearch/shows?q=girls
      * 'q=girls' is a query string
    * https://api.tvmaze.com/lookup/shows?imdb=tt0944947
      * 'imdb=tt0944947' is a query string

## Fetch API
* Provides an interface for fetching resources
  * Newer way of making requests via JS
  * Supports promises
* Fetch does not wait for all of the data requested before resolving promise
  * Not guaranteed to have the data

```js
fetch('https://api.cryptonator.com/api/ticker/btc-usd')
    .then(res => {
        console.log('Response, waiting to parse:', res);
        return res.json();
    })
    .then(data => {
        console.log('Data passed...', data);
        console.log(data.ticker.price);
    })
    .catch((err) => {
        console.log('Error:', err);
    });

// refactored
const fetchBTCPrice = async () => {
    try {
        const res = await fetch('https://api.cryptonator.com/api/ticker/btc-usd');
        const data = await res.json();
        console.log(data.ticker.price);
    } catch (err) {
        console.log('Error:', err);
    }
}
```