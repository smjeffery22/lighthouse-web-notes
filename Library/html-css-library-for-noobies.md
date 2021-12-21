# **HTML-CSS Library for Noobies**

## **HTML**
**Basic Elements**

`<html>` represents the root of an HTML document

`<head>` provides general information (metadata) about the document
* `<title>` defines the title of the document, shown in a browser's title bar
* `<link>` specifies relationships between the current document and an external resource

`<body>` represents the content of an HTML document

`<h1>, <h2>, ..., <h6>` Heading elements implement six levels of document headings

`<p>` represents a paragraph of text

`<div>` Division Element, generic container for flow content

`<ol>, <ul>` list of items with, or without numerical ordering
* `<li>` represents an item in a list

`<a>` anchor element; defines a hyperlink to a location or page on the Web

`<table>` display a data table. Note: not to be used for layout
* `<tr>` a table row
* `<td>` a cell in a table row


## **CSS**

`float:`

`line-height:'

```js
  /* Smartphones: minimum width of 320px to maximum width of around 420px */
  @media only screen and (min-width: 320px) and (max-width: 420px) {
    /* Write smartphone only styles here */
  }

  /* Another smartphone breakpoint is maximum width of around 420px */
  @media only screen and (max-width: 420px) {
    /* Write smartphone only styles here */
  }

  /* Tablet: minimum width of 768px to maximum width of 1024px */
  @media only screen and (min-width: 768px) and (max-width: 1024px) {
    /* Write Tablet only CSS here */
  }

  /* Another tablet breakpoint is maximum width of 1024px */
  @media only screen and (max-width: 1024px) {
    /* Write CSS rules that target Tablets screen sizes downwards - including smartphones */
  }

  /* Another tablet breakpoint is minimum width of 768px */
  @media only screen and (min-width: 768px) {
    /* Write CSS rules that target Tablets screen sizes upwards - including desktops */
  }

  /* Laptops / Desktops: minimum width of 1024px */
  @media only screen and (min-width: 1024px) {
    /* Write CSS rules that target Laptop/Desktop screen sizes and beyond */
  }

  /* Laptops / Desktops: minimum width of 960px */
  @media only screen and (min-width: 960px) {
    /* Write CSS rules that target small laptop screen sizes and beyond */
  }
  ```

## **jQuery**
**Methods**

`.bind:` 

`.blur:` 

`.click:` 

`.css():` To set a specified CSS property
```js
$("p").css({"background-color": "yellow", "font-size": "200%"});
```


`.find():` Get the descendants of each element in the current set of matched elements, filtered by a selector, jQuery object, or element.


`.first():` The first() method returns the first element of the selected elements.
  * Tip: To return the last element, use the last() method.


`.on:`


`.originalEvent:` Event objects contains originalEvent, which is the event object that the browser itself created. Can be accessed by `event.originalEvent`


`.preventDefault:` To cancel default action


`.empty():`
  * Remove all child nodes of the set of matched elements from the DOM
  * Remove any text within the set of matched elements


`.serialize():` Encode a set of form elements as a string for submission. Creates a text string in standard URL-encoded notation
  * Act on a jQuery object that has selected individual form controls
    * `<input>, <textarea> and <select>`


`.stopPropagation:` To prevent the event from bubbling up the DOM tree so the parent elements aren't notified of its occurrence


`.text():`
  * When this method is used to **return content**, it **returns the text content** of all matched elements (HTML markup will be removed).
  * When this method is used to **set content**, it **overwrites the content** of ALL matched elements.
  * The .text() method cannot be used on form inputs or scripts. To set or get the text value of input or textarea elements, use the .val() method. To get the value of a script element, use the .html() method.


`.trigger():` Triggers the specified event and the default behavior of an event (like form submission) for the selected elements
```js
$(textarea.trigger('reset')) // Reset the textarea field
```


`.val():` Get the current value of the first element in the set of matched elements or set the value of every matched element.
```js
$(textarea).val();    // Get the value from textarea field
$(textarea).val('');  // Clear the textarea field
```


## **HTML DOM**
