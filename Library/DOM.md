# DOCUMENT OBJECT MODEL (DOM)

- JS objects that represent a webpage
- HTML + CSS => JS objects
- Objects have relationships => tree structure

`window` special object that is always available in the browser

`document`

  - contains representations of all the content on a page
  - also contains methods and properties
  - top level folder for the webpage
  - **console.dir(document)**

## SELECTING

`.getElementById()` returns the whole DOM object of the id

  - **document.getElementById('idName');**
    - invalid parameter returns null since only one kind of id can exist

`.getElementsByTagName()` returns an HTMLCollection of elements with the given tag name *contained in an array*

  - **document.getElementsByTagName('tagName')**
    - Add [] at the end to grab specific DOM object
    - invalide parameter returns empty HTMLCollection

`.getElementsByClassName()` returns an HTMLCollection of elements with the given class name *contained in an array*

  - **document.getElementsByClassName('className')**
    - Add [] at the end to grab specific DOM object
    - invalid parameter returns empty HTMLCollection

`.querySelector()` returns the *first matching DOM element*

  - **document.querySelector('html_tag').optional_attribute**
    - Can change the value by = '...'
    - ('a') | ('#id') | ('.class') | ('a[title='Java']')
      - can combine to select more specific element

`.querySelectorAll()` returns all matching DOM element in an array

  - **document.querySelectorAll('html_tag').optional_attribute**
    - Can choose parent-child

`.getAttribute()` returns the attribute's value (id, class, title, href, etc.)

  - **variable_using_querySelector.getAttribute('attribute_name');**
    - Assign DOM element first using a variable
  - Grabs the texts from the attribute
    - Whereas accessing the property directly (i.e. using .href) goes through JS object (computed value)
      - most of the time, there is no difference

`.setAttribute()` changes the value of attribute (id, class, title, href, etc.)

  - **variable_using_querySelector.setAttribute('attribute_name', 'new_attribute_value');**
    - Assign DOM element first using a variable

## Manipulating

- In order to manipulate DOM object, need to select the object first

`.innerText` does not show hidden items

  - When trying to manipulate using HTML tags (i.e. <strong></strong>), it's set as text
  - **targetElement.innerText = 'value';**
    - Inserts text to the targetElement

`.textContent` shows everything in the text including hidden items

  - When trying to manipulate using HTML tags (i.e. <strong></strong>), it's set as text

`.innerHTML` shows everything including HTML tags

  - Can update using HTML tags

`.style` shows **inline** style, not the current styles (i.e. from css stylesheet)

  - Want to avoid inline style
    - Rather, define a class and apply style in JS file
  - **h1.style.color = 'green';**
  - **h1.style.fontSize = '3em';**
  - **h1.style.border = '2px solid pink';**

`.classList` shows the list of class

  - **variable_using_querySelector.classList**

`.classList.add` adds a class to the existing class (similar to array.push)

  - **variable_using_querySelector.classList.add('class_value')**

`.classList.remove` removes a class from the existing class

  - **variable_using_querySelector.classList.remove('class_value')**

`.classList.contains` checks if a class exists

  - **variable_using_querySelector.classList.contain('class_value')**

`.classList.toggle` toggle the class value (on/off)

  - **variable_using_querySelector.classList.toggle('class_value')**
    - if the class_value does not exist, it adds
      - if exists, it removes

`.createElement` creates new element

  - **document.createElement('new_element/tag_name');**

`.appendChild` adds an element as the last child

  - **document.parent_element.appendChild('new_element/tag_name');**

`.append` adds string/nodes to the inside of an element at the end

  - **element.append('string/node');**

`.prepend` adds string/nodes to the inside of an element at the beginning

  - **element.prepend('string/node');**

`.insertAdjacentElement` adds adjacent to an element

  - **targetElement.insertAdjacenetElement(position, new_element);**
    - _position:_
      - 'beforebegin': before the targetElement itself.
      - 'afterbegin': just inside the targetElement, before its first child.
      - 'beforeend': just inside the targetElement, after its last child.
      - 'afterend': after the targetElement itself.

`.after` adds after an element

  - **targetElement.after(new_element);**

`.remove()` removes the object from the tree it belongs to

  - **targetElement.remove()**

## Traversing

`.parentElement` moves up to the parent element from the current element

- **variable_using_querySelector.parentElement**

`.children` moves down to the child element from the current element

- **variable_using_querySelector.children[i]**
  - [i] to move to the specific child if there are more than one
  - **.childElementCount** for the total number of children

`.previousElementSibling` & `.nextElementSibling` move to the previous/next sibling element

- **variable_using_querySelector.previousElementSibling**
- **variable_using_querySelector.nextElementSibling**

## Events ([Event List MDN](https://developer.mozilla.org/en-US/docs/Web/Events))

`.addEventListener`

- **targetElement.addEventListener(event, callback)**
- Allows to add multiple functions to an event
- Include a parameter inside the callback function to capture **event object**
  - contains properties, information about the event
- event:
  - _click:_
  - _submit:_
  - _change:_ triggers when => access input field - change input field - leave input field
  - _input:_ triggers when => every time input field is updated

**Keyboard Event**

- keydown | keypress | keyup
- Within event object:
  - .key: output in the webpage
  - .code: what was actually pressed on the keyboard

**Form Event**

- **<form action="/shelter">**
  - By default, when the form is submitted, the data is submitted to the link specified in action attribute
    - Webpage will end up in that link

`.preventDefault()` prevents the default behaviour of the form after certain action (i.e. submission)

- **evt.preventDefault()**
- Ex. stay on the same page after submission

`.stopPropagation()` stops event bubbling

- **evt.stopPropagation()**

`input.value` returns the value inside the input field

- Can be saved in a variable and added to an element
- To reset after the form submission:
  - 'input.value = ""'
- Alternative is to use `form.elements.name_value.value`, where:
  - 'form' is the form object (or 'this')
  - 'name_value' is the value of the input tag's name attribute
    - 'name' becomes the property name of the element

**Event Delegation**

- After an event occurs, the 'target' property inside the event object shows which property the event occurred on
  - **evt.target** => (i.e. <li>...</li>) => returns the **whole li element**
    - **evt.target.nodeName** => (i.e. LI) => returns only the **tag name** only