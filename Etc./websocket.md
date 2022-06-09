# WEBSOCKET

  - You may already be familiar with WebSockets, depending on previous stretch activities in the program. Even still, there's a lot to explore when it comes to building real-time web applications.
    - What are WebSockets and what are they used for?
    - What are some popular WS libraries? Experiment with one in order to feel comfortable with it
    - Look into popular paid + managed solutions such as Pusher, and try out their tutorials. What value proposition do they provide, compared to having your own servers?

## What is WebSocket?

  - WebSocket allows for *two-way event-driven communication* between a web browser and a WebSocket server
    - Ideal for *real-time application*
      - i.e. chat app, multi-player game, displaying live data
  
## Getting Started

  - Install WebSocket: `npm i ws`
  - Include ws module in the server file `const WebSocket = require('ws');`
  - Create a WebSocket server `const wss = new WebSocket.Server({ port: 8082 })`
    - this line of code will start up the WebSocket server

    ```js
    // index.js
    const WebSocket = require('ws');

    const wss = new WebSocket.Server({ port: 8082 })
    ```

  - `const ws = new WebSocket('ws://localhost:8082');`
    - *ws://* for development purpose
    - *wss://* for production (secure form of ws)

## Handshake

  - On initial connection to the server side, *http request* is sent
    - The request gets *upgraded* to *websocket connection*

  - Inspect DevTools - Network - WS - Headers
    - Under request and response headers, shows http request upgraded to websocket request
      - **handshake is complete**
  
  - Upon successful handshake, data can be sent between the client and the server

## Sending Data Between Client and Server

  - 
    
## HTTP VS WebSocket

### HTTP

  - HTTP is unidirectional
    - Client sends request => Server sends response
    - Each request is associated with a corresponding response
  - After sending the response, the connection gets closed
  - Each HTTP/HTTPS request establishes a new connection to the server every time
    - Connection terminated upon receiving the response
    - New connection established for every request-response


### WebSocket

  - WebSocket is bidirectional
  - Connection between client and server alive until it is terminated by either party
    - Connection terminated when a party closes the connection
  - Communication between the client and the server takes place using the same connection channel until is it terminated

#### When to Use WebSocket

  - If any real-time update or continuous streams of data is needed

  - Data is continuously pushed/transmitted into the same connection that is already open
    - i.e. stock trading website where the price is being displayed live
      - data continuously pushed by the server to the client
  
  - Data is continuously received by the server and the update takes effect
    - i.e. in game where UI gets automatically refreshed

#### When Not to Use Websocket

  - If fetching old data or need to get the data only once to process it
    - RESTful services are sufficient



https://www.geeksforgeeks.org/what-is-web-socket-and-how-it-is-different-from-the-http/
https://www.youtube.com/watch?v=FduLSXEHLng&ab_channel=dcode