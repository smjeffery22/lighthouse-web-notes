# **Jeffery Park's LHL Week 4 Notes**

## **DAY 1 LECTURE NOTES**


## **DAY 1 COMPASS NOTES**

### DISPLAY
* Browser applied default styles to HTML elements
* Display is one of the default styles

**Block**
* Block element takes up the entire space of its parent element
  * Can contain other block elements or inline elements
* Examples of block elements:
  * headings `(<h1>, <h2>, <h3>,<h4>,<h5>,<h6>)`
  * div `(<div>)`
  * section `(<section>)`
  * footer `(<footer>)`
  * article `(<article>)`
  * paragraph `(<p>)`
  * lists `(<ul>, <ol>)`
  * nav `(<nav>)`

**Inline**
* Inline elements do not start a new line when rendered in the browser
  * Take up as much space as the content needs
  * Contain only data and other inline elements
  * Cannot add width/height/padding/margin
* Examples of inline elements:
  * anchor `(<a>)`
  * em `(<em>)`
  * strong `(<strong>)`
  * span `(<span>)`

**Inline-Block**
* Inline-block element has properties of both inline and block
  * Does not create a new line in the browser
  * Can have margin/padding/height/width
* Only two HTML tags that have a default inline-block display property are:
  * image tags `<img>`
  * buttons `<button>`

**Flex**
* **Flexbox** is a layout module in CSS
  * Allows to specify how elements on the page should appear
  * **Adapt to different screen sizes and display devices**
* To start using Flexbox, add the following to the **parent** element (**container** element)

```js
// CSS
.parent {
  display: flex;
}

//HTML
<section class="parent">
  <div class="a">A</div>
  <div class="b">B</div>
  <div class="c">C</div>
  <div class="d">D</div>
</section>
```

* **Parent Properties**
  * **flex-direction**
    * Defines the direction that the children (a.k.a flex items) will appear in
      * row / row-reverse
      * column / column-reverse
    * Determines the *main axis* for the flex container
      * row: horizontal
      * column: vertical
  * **justify-content**
    * Aligns flex items along the main axis
      * flex-start / flex-end
      * center
      * space-between / space-evenly / space-around
  * **align-items**
    * Aligns flex items along the cross axis
    * How flex items as a whole are aligned within the flex container
      * stretch
      * flex-start / flex- end
      * center
  * **flex-wrap**
    * Specifies whether flex items are forced on a single line or can be wrapped on multiple lines
      * nowrap (default)
      * wrap / wrap-reverse
  * **flex-flow**
    * Shorthand property for 'flex-direction' and 'flex-wrap;
      * Ex. `flex-flow: row wrap`
  * **align-content**
    * Aligns a flex container's lines within the flex container when there is extra space on the cross-axis
    * Set how multiple lines are spaced apart from each other
      * stretch
      * flex-start / flex-end
      * center
      * space-between / space-around

* **Child Properties**
  * **order**
    * Controls the order elementd appear
    * Default value is 0
  * **align-self**
    * Aligns flex items along the cross axis, overriding the 'align-items' value
      * stretch
      * flex-start / flex-end
      * center
      * baseline
  * **flex-grow**
    * Dictates how much space a flex item should take up
  * **flex-shrink**
    * 


### CSS FUNDAMENTALS
* CSS codes are made of static rules
  * Each rule takes one or more selectors and gives spㄷcific values to a number of visual properties
  * Properties are then applied to the page elements indicated by the selectors

* **Selectors**
  * Selector is used to target an element on a page

  ```js
  // To target an element
  selector { property: value;}

  // To target classes or ID
  .class1 { };
  .class1.class { };
  #anID {};

  // To target by name
  div { };

  // Combine different selectors
  div.some-class[attr$='ue'] { };
  ```


* **Precedence or Cascade**
  * An element may be targeted by multiple selectors and may have a property set on it in more than once
  * Rules with more specific selector take prescedence over a less specific one
    * Rule occurring later in the stylesheet overwrites a previous one

* **Specificity**
  * Specificity determines which CSS rule is applied by the browsers
  * If two selectors apply to the same element, the one with higher specificity wins
  * Categories which define the specificity level of a given selector (hierarchy):
    * inline styles
    * IDs
    * classes
    * attributed
    * elements
  * Selectors with equal specificity value
    * The latest rule counts
  * Selectors with equal specificity value
    * The more specific rule counts
  * **Measuring Specificity**
    * (#,#,#,#)
      * 1000 for style attribute
      * 100 for each ID
      * 10 for each attribute/ class or pseudo-class
      * 1 for each element name or pseudo-element


### WEB COLOURS
* Web colours are colours that are used in displaying web pages
  * Colours may be specified as an **RGB** triplet or in **hexadecimal** format
* Converting RGB to Hexadecimal

**Hex Triplet**
* Hex triplet is a six-digit, three-byte hexadecimal number to represent colours
  * Bytes represent red, green and blue
  * One byte represents a number in the range of '00 to FF' or '0 to 255'
* Formed by concatenating three bytes in hexadecimal notation


### HTTP POST - USE FOR SUBMITTING WEB FORMS
* `Content-Type: application/x-www-form-urlencoded` for form submission
  * Default value when a web browser sends a POST request from a web form element
  * Format for encoding key-value pairs
    * Each key-value pair is separated by an `&`
    * Each key is separated from its value by an `=`
    * Keys and values are both escaped by replacing spaces with `+`
      * Ex. field1=value1&field2=value2&field3=value3...
* jQuery `.serialize()` function turns a set of form data into a query string
  * Serialized data should be sent to the server in the data field of the Ajax POST request


## **DAY 2 LECTURE NOTES**
* To target ID, put #
* To target class, put .
* HTML elements (h1, p, etc.) don't need to put . or # in CSS file

* `navigator` in DevTools <=> `process` in Node

* `document` in DevTools
  * `console.log(document)` vs. `console.dir(document)`

* Scripts that are brought in after can use the variables from the previous scripts
  * No need to 'require'


### jQuery
* jQuery is a framework built with JS
  * Add extra funcionalities to websites
  * Traverse and manipulate HTML DOM tree
  * Simplifies event handling, CS animation and Ajax
* CDN (Content Delivery Network)
  * GET request to CDN
  * CDNs are scattered around the planet
  * `cdnjs.com` libraries
    * Use the latest version
    * Copy script tag and paste inside head class
    * Always bring in before our own so it reads jQuery first



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
* HTML deals with expressing the structure of the DOM
  * Adds **context** to the content of the page
* CSS deals with element styling, positioning and basic animations
  * Determines the **appearance** of the content
* JS handles behaviour, logic, dynamic content and user interaction
  * Defines the **behaviour** of the content

### DOM EVENTS
* Event listeners can be used to make page interactive
  1. Add an event listener to a DOM node
  2. Specify which event it should listen for
  3. Add a function that runs when that even happens
* `addEveneListener:` a method available to any element/DOM node
  * Specify the type of event and a callback function that triggers when that event happens

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

* `keydown` event listener: when key is for pressing down and not produce an output
  * Ex. shift, ctrl, tab, etc.
  * delete/backspace counts as keydown
* 'keypress' event listener: when pressing a key produces an output
  * Ex. a, 1, 5, p, etc.
    * 'keydown' also triggers
* If two identical event listeners are added, output twice

!['Graphical representation of an event dispatched in a DOM tree using the DOM event flow'](https://www.w3.org/TR/DOM-Level-3-Events/images/eventflow.svg)


### DOM EVENTS
* `blur:` To catch when the user leaves a form field
* `change:` Fired for 'input', 'select' and 'textarea' elements when an alteration to the element's value is committed by the user
* `click:` Emitted when a pointing device button has been pressed and released on an element
* `drag:` Emitted when an element or text selection is being dragged
* `focus:` To catch when a user enters a form field
* `input:` 
* `keydown:` Emitted when a keyboard key is pressed down
* `keypress:` 
* `mouseenter:` Trigerred whenever the mouse is hovered over the field
* `mouseleave:` Trigger any time the mouse stopped hovering over the field
* `mouseover:` Triggered when the cursor moves above an element
* `select:` Triggered when text is highlighted


## **DAY 3 LECTURE NOTES**

### AJAX
* AJAX (Asynchronous JavaScript and XML)

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
    success: (data) => { // callback function to execute when data comes back
      console.log('data', data);
    },
    error: (err) => {
      console.log(`error: ${err}`);
    }
  })
})
```


## **DAY 3 COMPASS NOTES**

### AJAX
* Ajax (Asynchronous JavaScript and XML)
  * Ajax HTTP requests don't interrupt a user's interaction with the current web page
  * HTTP resposne is passed to a JS function
    * JS function is responsible for determining what to do with it
      * Often modifies the DOM to reflect the response from the server
  * Allows users to continue using webpage while the request-response cycle is done in the background
* Ajax requests are normal HTTP requests sent to a web server by some JS on a webpage


## **DAY 4 LECTURE NOTES**

* Devices come in many sizes => need to design accordingly

**`Responsive Design`**
* Web app adapts to any screen size
  * Good user-experience
* Same HTML code to all devices
* CSS to alter the rending of the page
* DevTools => Phone Icon (Command + Shift + M)
  * To view the webpage in responsively
* Webpage should be designed for the user, not the owner
* Design for **mobile-first**
  * Spacing is important
    * Apple webpage has a lot of empty space
    * mobile-friendly
  * Extend the layout for larger screen after
* **Responsive Design Tools*
  * Relative units
  * Media queries
    * Like ifs
      * ex. if width is this, adjust this
  * Responsive images
  * Font scale
    * Header and its text ratio is important
  * Flexible grid-based layout
* **Viewport**
  * Always include
* **Units - Relative Units**
  * em: size of the parent
  * rem size of the root element
    * html element (body element since header doesn't count)
  * vw: 1% of the viewport width
    * changes as the webpage size changes
  * vh: 1% of the viw port's height
    * changes as the webpage size changes
  * %: percentage of the *parent size* (width, height, font-size)
* **Media Queries**
  * Allows to use different CSS style rules according to various screen sizes
  * ex.
    ```js
    @media only screen and (max-width: 200px) {
      #bgimage {
        background-image: url('...');
      }
    }`
    ```

**`SASS`**
* Extension of CSS that allows us to bring the programming syntax in CSS
  * SCSS
* **Variables**
  * Create variables and use across different CSS files
  * ex.
    ```
    $font-color: lightblue;
    $font-size: 12rem;

    p {
      color: $font-color;
      font-size: $font-size;
    }
    ```
* **Nesting**
  * Nesting styles inside one another can help improve the readability and logical flow of code
  * `&` can be used as `this`
  * ex.
    ```
    .container {
      display: flex;
      p {
        color: magenta;
        text-decoration: underline;
      }
      &:hover {
        border: 1px solid black;
      }
      div {
        border: 1px solid black;
      }
    }
    ```
* **Partials and @import**
  * Partials to store small amounts of code
    * Naming convention for partials: underscore
      * '_variables'
  * `CHECK NOTES`
* **@extend**
  * Wehn you hae two or more elements that have very similar styles, you could style one and use it as the basis for the other element
* **Mixins**
  * Like a function that returns a group of styles
  * Can be included in any other stlye by using `@include`
* **Variables and Imports are very useful**


## **DAY 4 COMPASS NOTES**

### RESPONSIVE WEB DESIGN PATTERNS

To disable viewport zooming, add the following to  every single web page created
* **`<meta name='viewport' content='width=device-width, initial-scale=1.0, maximum-scale=1.0' />`**


`Mostly Fluid`
* Fluid grid
* On smaller screens, the main content reflows
  * Columns are stacked vertically
* Usually only requires one breakpoint between small screens and large screens

!['fluid grid'](https://developers.google.com/web/fundamentals/design-and-ux/responsive/imgs/mostly-fluid.svg)

`Column Drop`
* Stacks the columns vertically as the window width becomes too narrow for the content
* Breakpoint depends on design

!['column drop'](https://developers.google.com/web/fundamentals/design-and-ux/responsive/imgs/column-drop.svg)

`Layout Shifter`
* The most responsive pattern with multiple breakpoints across several screen widths

!['layout shifter'](https://developers.google.com/web/fundamentals/design-and-ux/responsive/imgs/layout-shifter.svg)

`Tiny Tweaks`
* Small changes to the layout such as adjusting font size, resizing images or moving content around in very minor ways

!['tiny tweaks'](https://developers.google.com/web/fundamentals/design-and-ux/responsive/imgs/tiny-tweaks.svg)

`Off Canvas`
* Places less frequently used content, such as navigation or app menus, off screen in smaller screen size

!['off canvas'](https://developers.google.com/web/fundamentals/design-and-ux/responsive/imgs/off-canvas.svg)


## **DAY 5 COMPASS NOTES**

### ALGORITHMS
* An algorithm is a set of instructions or steps for accomplishing a specific task
* In computer science, it is any piece of **code that performs a certain task or solves a particular problem**

`Algorithm Complexity`
* How fast or slow a particular algorithm is
* Speed of a particular algorithm can be measured by **counting the number of elementary operations**
  * Each of the following is elementary operations:
    * let number 0;
    * number += 2;
    * console.log(number);
  * If an algorithm performs 'n' elementary operations, the running time is 'n'

`Elementary Operations`
* Any operation that takes a fixed amount of time to perform

**Example 1.**
* Below algorithm is performing 4 different operations
  * Running time is 4 even if there are more number of variables
  ```js
  let result = 0;
  result += number1;
  result += number2;
  console.log(result);
  ```

**Example 2.**
* In below example, for loop runs n times depending on the array length
  * Second statement runs 'n + 1' times for extra check at the end
  * Running time is '4n + 4'
```js
let result = 0; // 1
for (
  let i = 0; // 1
  i < array.length; // n + 1
  i++ // n
) {
  let number = array[i]; // n
  result += number; // n
}
console.log(result); // 1
```

`Linear vs. Logarithmic Algorithms`
* **Binary Search** is a very common algorithm used to search for something in a set of *ordered data*
  * Guessing a number from 1 to 15, start guessing from the middle and halving until the number is found
    * Total iteration to find a number:
      * 'log2(total-array-size) = x' <=> '2^x = total-array-size'
        * **'x + 1' times**
    * Everytime a number is checked, the remaining numbers are cut in half
      * Loop will run **log2 n** times instead of n times, where n is the size of array
  * **Linear Search** is searching from the beginning in order (i.e. from 1 to 15 until the number is found)
* When an algorithm's complexity grows logarithmically
  * Input may get very large
    * Number of elementary operations remains relatively small
    * Much more efficient

!['Linear vs. Logarithmic Algorithms'](https://i.imgur.com/qU0Euzx.png)

`Quadratic`
* Quadratic algorithms have a much slower running time than linear algorithms
  * n vs n^2
* Quadratic algorithms can be created by nesting loops
  * Common when comparing every item in an array to every other item in that array

!['Linear vs. Qaudratice'](https://i.imgur.com/HCFQmST.png)

### BIG O NOTATION
* When determinig the efficiency of an algorithm, how the algorithm's run time scales as a whole is more of a concern
  * As opposed to the total number of individual steps
  * **Big O Notation**
* Big O notation describes how the number of steps in an **algorithm scales relative to its input**
  * Written as `0()`
* 3 main things to remember when evaluating an algorithm using Big O notation:
  1. Arbitrarily large input
  2. Drop the non-dominant terms
      * Only care about 'n^2' in '(n^2 + n) / 2'
  3. Drop constant terms
      * 'n^3' determines the main curve in '(n^3) / 2' or '(n^3) * 2'
      * **Not** interested in **exact running time** of an algorithm
  * Above can be written in Big O notation
    * `O(n^2)` and `O(n^3)`
      * 'O n squared' and 'O n cubed'
  * Non-dominant and constant terms do not affect the overall shape of the graph
* **Constant O(1)**
  * **Constant Time:** An algorithm that will always take the same amount of time to execute
  * Constant time algorithms run in `O(1)`
* **Linear O(n)**
  * **Linear Time:** Number of operations an algorithm has to perform grows linearly relative to its input
  * Linaer algorithms run in `O(n)`
  * Each loop's running time is linear
* **Quadratic O(n^2)**
  * *Quadratic Time:** Number of operations that an algorithm has to perform is directly proportional to the square of the size of the input
  * Quadratic algorithms run in `O(n^2)`
  * Every time a loop gets added to nested loop, running time grows exponentially
    * 2 loops => n^2
    * 3 loops => n^3
    * 4 loops => n^4
* **Logarithmic O(log n)**
  * **Logarithmic Time:** Number of operations that an algorithm has to do is directly proportional to the logarithm of the size of the input
  * Logarithmic algorithms run in `O(log n)`
* Above are **time complexity**


## **DAY WE COMPASS NOTES**

### RAELATIONAL DATABASE
* Data is stored in database in an organized way in tables
  * **Search** data and **retrieve** when needed
  * Data can be created, retrieved, updated and deleted (CRUD) from a table
* Rational databse is a type of database that organizes data into tables and links them based on defined relationships
  * Allows to retrieve and combine data from one or more talbes with a single query

* Repetitive data is problematic and makes the CRUS operations more challenging
  * Longer to go through data
  * Remove repetitive data across columns (**first normal form (1NF)**)
  * Remove repetitive data across rows (**second normal form (2NF)**)
* With separated tables, data can be retrieved by drawing meaningful links between the tables
  * Give each row a unique identifier (**primary key**)
    * Entire process is called **normalization**
      * Rows will appear in the database only once, which makes CRUD operations easier
* **Relational Database Management Systems (RDBMS)**
  * Software used to create and use relational databases (i.e. MySQL, SQLite and PostgreSQL)
    * SQLite: iOS and Android let developers manage their app's private databases
    * PostgreSQL: Useful for mapping applications
* **Structured Query Language (SQL)**
  * 

### ENTITY RELATIONSHIP DIAGRAM (ERD)
* Graphical representation of the data requirements for a database
  * **Entity**
    * Represents a person, palce or thing that you want tot rack in a database
    * Become a table in the database
    * Each occurrence of the entity is an 'entity instance'
      * Rows

  * **Attribute**
    * Describes various characteristics about an individual entity
      * Columns
      * Ex. First name

  * **Primary key**
    * An attribute or group of attributes that uniquely identifies an instance of the entity
      * No two rows have the same value
        * Ex. Student ID

  * **Relationship**
    * Describes how one or more entities interact with each other
    * A verb is often used to describe the relationship

  * **Cardinality**
    * The count of instances that are allowed or are necessary between entity relationships

* Crow's Foot Notation
!['Crow's Foot Notation Diagram'](https://res.cloudinary.com/practicaldev/image/fetch/s--Sf6yoYk6--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://i.ibb.co/qjw6dMn/Crow-Notation-Chart.png)

