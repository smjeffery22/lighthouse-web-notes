# **HTML-CSS Library for Noobies**

## **HTML**

**Basic Elements**

`<html>` represents the root of an HTML document

`<head>` provides general information (metadata) about the document

- `<title>` defines the title of the document, shown in a browser's title bar
- `<link>` specifies relationships between the current document and an external resource

`<body>` represents the content of an HTML document

`<h1>, <h2>, ..., <h6>` Heading elements implement six levels of document headings

`<main>` Dominant content of the body of a document and should be unique to the document (not repeated)

`<article>` Self-contained composition, which is intended to be independently distributable or reusable

- Should include headings
- Ex. forum post, article, blog

`<aside>` Represents a portion of a document whose content is only indirectly related to the document's main content

- Ex. sidebars, call-out boxes

`<header>` Introductory content, typically a group of introductory or navigational aids

`<footer>` A footer for its nearest sectioning content or sectioning root element

`<section>` Standalone section, which doesn't have a more specific semantic element to represent it

`<nav>` To provide navigation links, either with the current document or to other documents

- Ex. menues, TOC, indexes

`<p>` represents a paragraph of text

`<div>` Division Element, generic container for flow content

`<span>` Generic element, but inline element unlike div

`<ol>, <ul>` list of items with, or without numerical ordering

- `<li>` represents an item in a list

`<a>` anchor element; defines a hyperlink to a location or page on the Web

`<table>` display a data table. Note: not to be used for layout

- `<thead>` Set of rows defining the head of the columns of the table
  - encloses th tags
- `<tr>` a table row
- `<th>` header of a group of table cells
  - used for cells in head row
- `<td>` a cell in a table row
- `<tbody>` Encapsulates tr elements indicating the body of the table (encloses tr tag)
- `<tfoot>`
- `<rowspan="#">` To make more than one row space in heading (attribute in th tag)
- `<colspan="#">` To make more than one column space in heading (attribute in th tag)

`<form>` A shell/container that has no visual impact; it contains interactive controls for submitting information

- **Action** attribute specifies where the format data should be sent

- **Method** attribute specifies which HTTP method should be used

- `<input>` To create a variety of different form controls

  - Commonly used attributes:

    - `type=""` text, email, password, color, number, url, tel, etc.
      - **checkbox:** 'checked' attribute at the end to default the checkbox to be checked off
      - **radio:** similar to checkbox, but only allow to select one
        - give the _same names_ to allow only one to be clicked
        - value: what will be sent to the server (shown in URL)
      - **range:** creates a range bar
        - can assign min/max/step/value
    - `placeholder=""` preview of what input is needed
    - `name=""` name used to send data to the server (shown in URL)
      - should be included in all input elements
      - <input name="username">
        - *'/tacos?username=smjeffery'* in URL upon submitting the form
    - `value=""` to set pre-assigned value in the input field

  - **required** at the end of the input element to require the field to be filled before submission

  - **minlength** and **maxlength** to set the min/max length required for input (text)

  - **min** and **max** to set the min/max values required for input (number, range, date, etc.)

- `<label>` A caption for an item in a user interface

  - Allows the label to be clickable (ex. for checkbox)
  - Use `for=""` attribute to link with input elements's `id`
    - When linked, the label can be clicked to access the input

- `<button>`

- `<select>` A control that provides a menu of options

  - `<option>` options to choose from within select element
  - `selected` attribute to pre-select an option as default

- `<textarea>` Textbox where texts can be written
  - use 'cols' and 'rows' to control the size of the textarea

`<figcaption>` Self-contained content to caption an image

`<hr>` Thematic break between paragraph-level elements (a horizontal line across the page)

`<br>` Produces a line break (used in poem/address where division of lines is significant)

`<sup>` Superscript

`<sub>` Subscript

`HTML entities` Symbols used in HTML that will be rendered in the browser

- Entity Name or Entity Number
- '<': &lt; or &#60;
- '>': &gt; or &#62;

`Emmet` To produce tags with shortcut syntax

- 'ul>li\*2>span.hello$'
  - Creates an unordered list, 2 lists, span tag with hello class attributes (1 and 2)

`Semantic Markup`

- A way of writing and structuring HTML so that it reinforces the semantics, or meaning, of the content rather than its appearance
- Allows search engines and crawlers to better understand the content
- Use of elements such as header, nav, section, etc. instead of only using div and span

## **CSS**

### **Text Properties**

`text-align`

`font-weight`

`text-decoration`

- underline, line-through, etc.
- color, style (dotted, wavy, etc.)
- _none_ to remove decoration on text (ex. underline) such as underline in anchor tag

`letter-spacing`

`line-height`

`font-size`

`font-family`

`float`

### **Box Model**

`border-width`
`border-color`
`border-style`
`box-sizing` *border-box* to set the width to fixed
`border` width | style | color

### **Display**

`inline` Width & Height are ignored; Margin & Padding push elements away horizontally but not vertically

- Items are lined up horizontally, similar to span element
  - Inline elements do not push the surrounding elements away vertically, only horizontally
  - Width and Height are ignored

`block` Block elements break the flow of a document; Width, Height, Margin & Padding are respected

- Makes elements block-level elements

`inline-block` Behaved like an inline element except Width, Height, Margin & Padding are respected

`none` To hide elements on the browser

**Adjacenet Sibling Selector**
`elem1 + elem2` To select only the elem2's that are immediately preceded by elem1 (comes after elem1, but not descendent)\
_div + p { color: green; }_
!['CSS Adjacent Selector](https://img.techbrij.com/650/css%20selector%203.jpg)

**Direct Child**
`elem1 > elem2` To select only elem2's that are direct children of elem1\
_div#container > p { border: 1px solid black; }_
!['CSS Direct Child'](https://img.techbrij.com/650/css%20selector%202.JPG)

**General Sibling**
`elem1 ~ elem2` To select
_div ~ p{ background-color:blue; }_
!['CSS Adjacenet Sibling'](https://img.techbrij.com/650/css%20selector%204.jpg)

### **Pseudo Classes**

- Keyword added to a selector that specifies a special **state (entire)** of the selected elements(s)

`:hover` Changes properties when hovered over an item

`:focus` Triggered when the user clicks or taps on an element (i.e. form input)

`:active` Changes properties when clicked

`:checked` Changes properties when radio/checkbox is checked off

`:nth-of-type(n)`: Changes properties of every nth selector

- (2n) for every other and (3n) for every 3rd

### **Pseudo Elements**

- Keyword added to a selector that allows to style a **particular part (partial)** of selected element(s)

`::first-letter` Changes properties of the first letter

`::first-line` Changes properties of the first line

`::selection` Changes properties when selected/highlighted

### **The Cascade**

- The order the styles are declared in and linked to matters
  - Whatever comes after overwirtes previous rule(s)
  - CSS file linked after in HTML file overwrites previous rule(s)

### **Specificity**

- How the browser decides which rules to apply when there is conflict
  - More specific selector overwrites
    - **ID > CLASS / ATTRIBUTE / PSEUDO-CLASS/SELECTORS > ELEMENT**

### **Border**

`border:` width | style | color

`box-sizing`

- _border-box_ to make the width of the element go from border to border
  - width includes padding + margin

`border-radius`

### **CSS Units**

`Relative`

- **em**: Relative to parent; font-size and other properties

  - Font-size: _relative to parent_

    - 1em => same font-size as the parent
    - 2em => twice the font-size of the parent

  - Other properties: _relative font-size of the element itself_

    - 1em => equal to the computed font-size of the element itself
    - Overall size/shape changes together (scales together)

  - Problem with em arises in nested elements
    - Grows/shrinks as there are more elements

- **rem**: Relative to the root html element's font-size

  - If the root font-size is 20px
    - 1rem => 20px
    - 2rem => 40px

- **VH**

- **VW**

- **%**: Relative to some other value
  - Value from the parent or element itself
  - width: 50% => half the width of the parent
  - line-height 50% => half the font-size of the element itself

`Absolute`

- PX
- PT
- CM
- IN
- MM

### **Alpha & Opacity**

`Alpha`

- `rgba(#, #, #, #)` in background-color => the last number represents the _alpha (i.e. transparency) range from 0 to 1_
  - In hexadecimal, `#aabbcc'xx'` => the last two characters govern the transparency (00 to FF)

`Opacity`

- `opacity: #` sets on element which governs the transparency to the entire element including its content and descendents

### **position**

- Sets how an element is positioned in a document
- top, right, bottom and left properties determine the final location of positioned elements

- `static:` element is positioned according to the normal flow of the document
- `relative:` element is positioned according to the normal flow of the document then offset relative to itself
- `absolute:` element is removed from the normal documents flow and no space is created for the element in the page layout
- `fixed:` the element is removed from the normal document flow and no space is created for the element in the page layout
  - Positioned relative to the initial containing block established by the viewport
  - Ex. navbar fixed at the top of the browser
- `sticky:` similar to fixed, but not initially fixed
  - Ex. Has its own position but becomes fixed when scrolled down

### **transition:** property_name | duration | timing_function | delay

- Define the transition between two states of an element
- `property_name:` target property name
- `duration:` how long it takes for the transition to occur
- `timing_function:` how gradually the transition should occur
  - ease-in, ease-out, ease-in-out, etc.
  - https://easings.net/

### **transform:** rotate | scale | translate

- Rotate, scale, skew or translate an element
- `transform-origin` sets the origin for an element's transformations
  - top right, bottom right, 50px 50px, etc.
- `rotate(##deg)`
- `scale(#)` scales in both x and y
  - scaleX, scaleY, etc.
- `translate(x, y)`
- `skew(##deg, ##deg)`

### **animation:** animation-name | animation-duration | animation-timing-function | animation-iteration-count | animation-direction

- Need to use with **@keyframe** defined separately

  ```js
  // option_1
  animation: up-and-down 1s linear infinite alternate;

  // option_2
  animation: up-and-down 1s linear infinite;
  ```

### **@keyframes** animation-name

- Assign positions at different frames

  ```js
  // option_1
  @keyframes up-and-down {
    0% {
      transform: translateY(0%);
    }
    100% {
      transform: translateY(50%);
    }
  }

  // option_2
  @keyframes up-and-down {
    0%, 100% {
      transform: translateY(0%);
    }
    50% {
      transform: translateY(50%);
    }
  }
  ```

### **Background**

`-color`

`-image` insert background image

`-size` sets the size of the element's background image

- _cover_ to fit the image

`-repeat`

`-position`

### **Flex**

- **Flexbox** is a layout module in CSS
  - Allows to specify how elements on the page should appear
  - **Adapt to different screen sizes and display devices**
- To start using Flexbox, add the following to the **parent** element (**container** element)

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

- https://mastery.games/flexboxzombies/

- **Parent Properties**

  - **flex-direction**

    - Defines the direction that the children (a.k.a flex items) will appear in
    - Default is set to row
      - _row:_ left to right
      - _row-reverse:_ right to left
      - _column:_ top to bottom
      - _column-reverse:_ bottom to top
    - Determines the _main axis_ for the flex container
      - row: horizontal
      - column: vertical

  - **justify-content**

    - Aligns flex items _along the main axis_
    - Default is set to flex-start
      - _flex-start:_ positions at the start of the axis
      - _flex-end:_ positions at the end of the axis
      - _center:_ positions at the center of the axis
      - _space-between:_ spread out contents with even space between them
        - first and last content fixed at the beginning and the end of the axis
      - _space-around:_ even amount space around each contents
      - _space-evenly_

  - **align-items**

    - Aligns flex items _along the cross axis_
    - How flex items as a whole are aligned within the flex container
      - _flex-start:_ aligns items at the start of the cross axis
        - top for horizontal
        - left for vertical
      - _flex-end:_ aligns items at the end of the cross axis
      - _stretch:_ stretches the items along the cross axis
      - _center:_ center the items along the cross axis

  - **flex-wrap**

    - Specifies whether flex items are forced on a single line or can be wrapped on multiple lines
      - nowrap (default)
      - wrap / wrap-reverse

  - **flex-flow**

    - Shorthand property for 'flex-direction' and 'flex-wrap;
      - Ex. `flex-flow: row wrap`

  - **align-content**

    - Aligns a flex container's lines within the flex container when there is extra space on the cross-axis
    - Only applies when flex is wrapped and there are multiple lines
    - Set how multiple lines are spaced apart from each other
      - stretch
      - flex-start / flex-end
      - center
      - space-between / space-around

- **Child Properties**

  - **align-self**
    - _Overrides the 'align-items' value_
    - Aligns _individual flex items within the content_ along the cross axis (similar to align-items)
    - Need to _specify children element_
      - flex-start
      - flex-end
      - stretch
      - center
      - baseline
  - **flex-grow**

    - Dictates how much space a flex item should take up
    - _Overwrites Justify-content is ignored_
    - Setting flex-grow to _1_ makes items _grow to fill the available space_
      - In the _same direction_ along the _main-axis_
      - flex-grow of _0_ is default size
    - Using multiple flex-grow can set _ratio_
      - i.e. 2 : 1 ratio to fill the space
        - flex-grow: 2 and flex-grow: 1
    - _Tip_
      - Set flex-grow to 1 for all items
      - Set flex-grow to 0 for any items that do not need to grow

  - **flex-shrink**

    - Starts shrinking _once the containing space is too small_ to fit all the items
    - Uses _ratios_ to control how quickly each item shrinks
    - If all items are shrinking evenly, number does not matter
    - flex-shrink of 0 does not shrink the item

  - **flex-basis**

    - Sets the initial size of the flex item before growing/shrinking happens
      - _If the items runs out of space, items will shrink according to their flex-shrink ratio_
      - _If extra space, can expand to fill according to their flex-grow ratios_
    - Improved version of _width_ and _height_ depending on flex-direction
    - _Overwrites width and height_
    - _min-width_ acts as a _lower-limit_ of flex-basis
      - same applies for min-height
    - _max-width_ acts as an _upper-limit_ for flex-basis

      - same applies for min-height

      ```
      // flex-basis set to 300px
      flex-basis: 100px;
      min-width: 300px;

      // flex-basis set to 100px
      flex-basis: 400px;
      max-width: 100px;
      ```

    - Can also use _%_
    - Not setting flex-basis <=> flex-basis: auto
      - Uses the width

  - **order**
    - Controls the order elementd appear
    - Default value is 0

`-basis` initial size of an element before additional space is distributed\
`-grow` controls the amount of available space an element should take up (unitless)\
`-shrink` if items are larger than the container, they shrink according to flex-shrink (relative to other flex items)\
`flex` grow | shrink | basis

## **Media**

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

## **Boostrap**

- Helps to quickly build responsive websites
- Gives access to pre-built components that can be incorporated into websites
- Comes with grid system which helps with constructing custom, responsive layouts
- Include **CSS link** and **JS scripts** in .html file

`Grid`

- Every row in BS has 12 units of space

## **ejs**

**Tags**

- Whatever is put in the ejs tags will be treated as JS

- **<%** 'Scriptlet' tag, for control-flow, no output
  - Add at every line of JS line of code
- **<%\_** ‘Whitespace Slurping’ Scriptlet tag, strips all whitespace before it
- **<%=** Outputs the value into the template (HTML escaped)
  - Ex. to render strings into the webpage
- **<%-** Outputs the unescaped value into the template
- **<%#** Comment tag, no execution, no output
- **<%%** Outputs a literal '<%'
- **%>** Plain ending tag
- **-%>** Trim-mode ('newline slurp') tag, trims following newline
- **\_%>** ‘Whitespace Slurping’ ending tag, removes all whitespace after it

## **jQuery**

**Methods**

`.bind:`

`.blur:`

`.click:`

`.css():` To set a specified CSS property

```js
$('p').css({ 'background-color': 'yellow', 'font-size': '200%' });
```

`.find():` Get the descendants of each element in the current set of matched elements, filtered by a selector, jQuery object, or element.

`.first():` The first() method returns the first element of the selected elements.

- Tip: To return the last element, use the last() method.

`.on:`

`.originalEvent:` Event objects contains originalEvent, which is the event object that the browser itself created. Can be accessed by `event.originalEvent`

`.preventDefault:` To cancel default action

`.empty():`

- Remove all child nodes of the set of matched elements from the DOM
- Remove any text within the set of matched elements

`.serialize():` Encode a set of form elements as a string for submission. Creates a text string in standard URL-encoded notation

- Act on a jQuery object that has selected individual form controls
  - `<input>, <textarea> and <select>`

`.stopPropagation:` To prevent the event from bubbling up the DOM tree so the parent elements aren't notified of its occurrence

`.text():`

- When this method is used to **return content**, it **returns the text content** of all matched elements (HTML markup will be removed).
- When this method is used to **set content**, it **overwrites the content** of ALL matched elements.
- The .text() method cannot be used on form inputs or scripts. To set or get the text value of input or textarea elements, use the .val() method. To get the value of a script element, use the .html() method.

`.trigger():` Triggers the specified event and the default behavior of an event (like form submission) for the selected elements

```js
$(textarea.trigger('reset')); // Reset the textarea field
```

`.val():` Get the current value of the first element in the set of matched elements or set the value of every matched element.

```js
$(textarea).val(); // Get the value from textarea field
$(textarea).val(''); // Clear the textarea field
```


