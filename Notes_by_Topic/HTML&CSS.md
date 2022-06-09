# HTML & CSS - (LHL W3-W4)

## **WE Compass Notes**

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
  * Target elements by id using a selector with a **hashtag prefix** `#buy-now-main-btn`
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
* Transforms **HTML text** into a complete **object structure**
* Allows JS to access the text content and elements of the website document as objects
* Difference between DOM and HTML source code:
  * DOM is modified by client-side JS
  * Browser automatically fixes errors in the source code

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
  * If 'p' is clicked, onclick runs on 'p' -> 'div' -> 'form'
  * This process is called **bubbling**
    * Events "bubble" from the inner element up through parents like a bubble in the water

`event.target`
* The most deeply nested element that caused the event is called a **target** element
  * Accessible as `event.target`
    * `event.target:` 'target' element that initiated the event
    * `this:` 'current' element

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
  * When you hae two or more elements that have very similar styles, you could style one and use it as the basis for the other element
* **Mixins**
  * Like a function that returns a group of styles
  * Can be included in any other style by using `@include`
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