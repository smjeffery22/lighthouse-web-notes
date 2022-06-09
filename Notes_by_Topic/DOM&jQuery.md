# DOM & jQuery - (LHL W4)

### jQuery
* Events/actions constantly occur on a webpage
* Only notified of events if listening
  * Waiting for the browser to communicate that a specific event has occurred
    * Then tell the browser how to react
* **Event handler:** To specify what to do when an event occurs using function

### HTTP POST - USE FOR SUBMITTING WEB FORMS

- `Content-Type: application/x-www-form-urlencoded` for form submission
  - Default value when a web browser sends a POST request from a web form element
  - Format for encoding key-value pairs
    - Each key-value pair is separated by an `&`
    - Each key is separated from its value by an `=`
    - Keys and values are both escaped by replacing spaces with `+`
      - Ex. field1=value1&field2=value2&field3=value3...
- jQuery `.serialize()` function turns a set of form data into a query string
  - Serialized data should be sent to the server in the data field of the Ajax POST request

## **DAY 2 LECTURE NOTES**

- To target ID, put #
- To target class, put .
- HTML elements (h1, p, etc.) don't need to put . or # in CSS file

- `navigator` in DevTools <=> `process` in Node

- `document` in DevTools

  - `console.log(document)` vs. `console.dir(document)`

- Scripts that are brought in after can use the variables from the previous scripts
  - No need to 'require'

### jQuery

- jQuery is a framework built with JS
  - Add extra funcionalities to websites
  - Traverse and manipulate HTML DOM tree
  - Simplifies event handling, CS animation and Ajax
- CDN (Content Delivery Network)
  - GET request to CDN
  - CDNs are scattered around the planet
  - `cdnjs.com` libraries
    - Use the latest version
    - Copy script tag and paste inside head class
    - Always bring in before our own so it reads jQuery first

```js
jQuery()
jQuery() === $

// Load when document is ready
$(document).ready(function() {

});
// same as '$(() => {})'

//element selection (finding things in the DOM)
// jQuery()
document.getElementByID('main-list');
$('#main-list)

// create things for the DOM
$('<h1>'); // creates h1
$('h1'); // finds h1
$('p'); // finds p

// create an li, give it the text 'water'
const myLi = $('<li>');
myLi.text('water'); // <li>water</li>
$('#main-list').append(myLi);

// above two first lines same as:
const myLi = $('<li>water</li>');

// above three lines same as:
$('<li>water</li>').appendTo('#main-list');

// parent.append(child)
// child.appendTo(parent)

// document.addEventListener('click', () => {});
$('h1').on('click', () => { // when click event occurs, bring the callback
  alert('h1 was clicked');
});

$('h1').click(() => {});

// grab the input field
const myInput = $('#my-input');

// get the value the user typed in
const newText = myInput.val();

// create a new li with the text from the user
const myNewLi = $('<li>').text(newText);

// add to the DOM
$(#'main-list').append(myNewLi);

// clear the input field
myInput.val('');

// give the input field focus
myInput.focus();

// to load the page first before scripts run
$(document).ready(() => {});
```

## **DAY 2 COMPASS NOTES**

- HTML deals with expressing the structure of the DOM
  - Adds **context** to the content of the page
- CSS deals with element styling, positioning and basic animations
  - Determines the **appearance** of the content
- JS handles behaviour, logic, dynamic content and user interaction
  - Defines the **behaviour** of the content

### DOM EVENTS

- Event listeners can be used to make page interactive

  1. Add an event listener to a DOM node
  2. Specify which event it should listen for
  3. Add a function that runs when that even happens

- `addEveneListener:` a method available to any element/DOM node

  - Specify the type of event and a callback function that triggers when that event happens

  ```js
  // creates an event listener for the 'document' node
  // event is triggered when you click anywhere on the page, because the root (document) node is specified
  document.addEventListener("click", () => {
    console.log("You just clicked somewhere on this page.");
  });

  // specify the DOM node to reference using the document.getElementById method and put that reference in a variable
  const div1 = document.getElementById("div-one");
  // when div1 is clicked, run the function
  div1.addEventListener("click", () => {
    console.log("You clicked on div 1.");
  });

  // create a function
  const printMessage = () => {
    console.log("You clicked on div 2.");
  });
  // put a reference to the "div-two" element in a variable
  const div2 = document.getElementById("div-two");
  // when div2 is clicked, run the function
  div2.addEventListener('click', printMessage);
  ```

- `keydown` event listener: when key is for pressing down and not produce an output
  - Ex. shift, ctrl, tab, etc.
  - delete/backspace counts as keydown
- 'keypress' event listener: when pressing a key produces an output
  - Ex. a, 1, 5, p, etc.
    - 'keydown' also triggers
- If two identical event listeners are added, output twice

!['Graphical representation of an event dispatched in a DOM tree using the DOM event flow'](https://www.w3.org/TR/DOM-Level-3-Events/images/eventflow.svg)

### DOM EVENTS

- `blur:` To catch when the user leaves a form field
- `change:` Fired for 'input', 'select' and 'textarea' elements when an alteration to the element's value is committed by the user
- `click:` Emitted when a pointing device button has been pressed and released on an element
- `drag:` Emitted when an element or text selection is being dragged
- `focus:` To catch when a user enters a form field
- `input:`
- `keydown:` Emitted when a keyboard key is pressed down
- `keypress:`
- `mouseenter:` Trigerred whenever the mouse is hovered over the field
- `mouseleave:` Trigger any time the mouse stopped hovering over the field
- `mouseover:` Triggered when the cursor moves above an element
- `select:` Triggered when text is highlighted

## **DAY 3 LECTURE NOTES**

### AJAX

- AJAX (Asynchronous JavaScript and XML)

```xml
<user>
  <name>James</name>
  <password>1234</password>
</user>
```

```json
{
	"name": "James",
	"password": "1234"
}
```

```js
$(() => {
	$.ajax({
		url: '/api/blogs',
		method: 'GET',
		dataType: 'json', // optional
		success: (data) => {
			// callback function to execute when data comes back
			console.log('data', data);
		},
		error: (err) => {
			console.log(`error: ${err}`);
		},
	});
});
```

## **DAY 3 COMPASS NOTES**

### AJAX

- Ajax (Asynchronous JavaScript and XML)
  - Ajax HTTP requests don't interrupt a user's interaction with the current web page
  - HTTP resposne is passed to a JS function
    - JS function is responsible for determining what to do with it
      - Often modifies the DOM to reflect the response from the server
  - Allows users to continue using webpage while the request-response cycle is done in the background
- Ajax requests are normal HTTP requests sent to a web server by some JS on a webpage

