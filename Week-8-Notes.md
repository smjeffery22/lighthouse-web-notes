# **Jeffery Park's LHL Week 8 Notes**

## **Table of Contents**

- [DAY 1 LECTURE NOTES](#day1lec)
- [DAY 2 LECTURE NOTES](#day2lec)
- [DAY 2 COMPASS NOTES](#day2comp)
- [DAY 3 LECTURE NOTES](#day3lec)
- [DAY 3 COMPASS NOTES](#day3comp)
- [DAY 4 LECTURE NOTES](#day4lec)
- [DAY 4 COMPASS NOTES](#day4comp)
- [DAY 5 LECTURE NOTES](#day5lec)
- [DAY 5 COMPASS NOTES](#day5comp)

<a id="day1lec"></a>
## **DAY 1 LECTURE NOTES**

### CORS

  - Allows to fetch data from the port different than the one being used

### MIDDLEWARE

  - Code that runs between Request and Response

<a id="day2lec"></a>
## **DAY 2 LECTURE NOTES**

### WHY TESTING

  - Confidence
  - Automation
  - Satisfy with our code
  - Find bugs
  - Maturing the code, without re-doing the tests all over again
  - Profit

### KIND OF TESTING

  - Mocha/Chai/Jest Unit Tests
  - Integration
  - End-to-End
  - Static Tests

### JEST

  - Already integrated into React App library
  - `__tests__` directory
    - Extension `.test.js`
      - i.e. `file_name.test.js`
  
  - **Test code structure**
    - a describe block
    - inside of describe block, test/it blocks
    - inside test/it blocks, checks
  
  - **Jest Cheatsheet**
    - https://devhints.io/jest

#### UNIT TESTING

  ```js
  import sum from '';

  describe('Basic Tests', () => {
    it('checks if 2 + 2 is squal to 4', () => {
      const answer = 2 + 2;
      expect(answer).toBe(4);
    });

    it('does a sum of 4 + 4 and short return 8', () => {
      expect(sum(4, 4).toBe(8));
    });
  });
  ```

#### INTEGRATION TESTING

  - We want to see if our component renders
  - Jest alone cannot perform integration testing
    - Need a help of some extra libraries
    - *testing-library*
      - import *{ render }*
    - *jest-dom*

```js
import React from 'react';
import App from '';
import { render, prettyDOM } from '@testing-library/react';

describe('App Component', () => {
  it('renders', () => {
    // const a = render(<App />); // the library will render the entire page
    // console.log(a) // can see it's HTML - shows different functions that can be used
    // console.log(a.debug()) // shows the entire randering of the app (i.e. whatever is inside the App component)
    
    // just testing rendering
    const { getByText } = render(<App />);
    const header = a.getByText('ToDo List');
    console.log(prettyDOM(header)); //

    // testing by text is fragile

    const { getByTestId } = render(<App />);
    const header = getByTestId('header'); // add an attribute of data-testid="header"
    console.log(prettyDOM(header)); //

  });
})
```

```js
import React from 'react';
imprt { render } from '@testing-library/react`;
import '@testing-library/jest-dom`;
import Item from '';

describe('Item Tests', () => {
  it ('renders the item componet on the screen', () => {
    render(<Item item="Buy Milk"/>);
  });

  it('renders the item component and checks if item has class todo-item', () => {
    const { getByTestId } = render(<Item item="buy milk" />);
    const itemHTML = getByTestId('item');
    expect(itemHTML).toHaveClass('todo-item');
  });
});
```

```js
import React from 'react';
imprt { render, fireEvent, prettyDOM } from '@testing-library/react`;
import '@testing-library/jest-dom`;
import Item from '';

describe("Form Tests", () => {
  // first test is usually checking render
  it("renders form", () => {
    const { debug } = render(<Form />);
    console.log(debug());
  });

  it("tries to click 'Add' button to submit into form", () => {
    const { getByText, debug } = render(<Form />);
    const button = getByText("Add");
    fireEvent.click(button); // fireEvent for testing events
    console.log(debug()); // to check what happened after click
    const err = getByText("Cannot be Blank"); // to see if error returns after click
  });
});

  it("writes a task in the input field and presses submit", () => {
    // const foo = () => {console.log("testing")}; // for testing click event - pass down as props in Form component
    const addItemMock = jest.fn(); // mocking function
    const {getByText, getByPlaceholderText, getByTestId } = render(<Form addItem={addItemMock} />);
    const button = getByText("Add");
    // const input = getByTestId("form-input");
    const input = getByPlaceholderText("enter todo");
    // console.log(prettyDOM(input)); // since input is HTML element, prettyDOM shows as DOM

    fireEvent.change(input, {target: {value: "buy milk"}}); // mimics typing
    // console.log(prettyDOM(input)); // shows changes value

    fireEvent.click(button); // tests clicking

    expect(addItemMock).toHaveBeenCalled();
  });

```

<a id="day2comp"></a>
## **DAY 2 COMPASS NOTES**

### JEST

#### FOLDER STRUCTURE

  - Jest will find files that match the following paths:
    - src/components/__tests__/Button.js
      - tests in __tests__ folder do not need to have term / spec in file name
    - src/components/Button.test.js
    - src/components/Button.spec.js

  - Jest will find tests with any of the following extensions:
    - .js / .jsx
    - .ts / .tsx
  
#### TEST ERRORS VS. CODE ERRORS

  - Two sources of error:
    1. Code does not work => throws error
    2. Test does not work => not able to confirm expected behaviour

### PROP-TYPES

  - Validate component props
  - Allows to set the type of props so that error message is shown when wrong types of props are passed down

### REACT-TESTING-LIBRARY

  - Useful tests for React require integrating multiple units
  - A component and all of its children are considered a unit
  - **react-testing-library**
    - imported as *@testing-library/react*

#### STRUCTURE

  - **Three Phases of a Unit Test**
    1. Initialize the component that we would like to test
    2. Trigger the change that executes the unit
    3. Verify that the unit produced the expected result

  - Test can be declared using the `it` function provided by Jest
    - *First argument:* descriptive name for the test
    - *Second argument:* a function that contains the test code
    ```js
    it("renders without crashing", () => {
      render(<Button />);
    });

    it.only("renders its `children` prop as text", () => {
      const { getByText } = render(<Button>Default</Button>);
      expect(getByText("Default")).toBeInTheDocument();
      console.log(getByText())
    });
    ```
      - `render` function is provided by the react-testing-library
        - verification test to ensure the component renders
          - if not, the rest of the tests will fail
      - `expect` function is injectde into the global scope by Jest
      - `getByTest` query function is returned by the render function
        - part of the dom-testing-library
      - `toBeInTheDocument` function is a matcher provided through Jest by the jest-dom library
  

#### QUERIES
  - https://testing-library.com/docs/queries/about/

  - Queries are the methods that Testing Librrary gives to *find elements* on the page
  - **Types of Queries:**
    - *getBy...:* returns the *matching node* for a query
      - if non-existence/more than one found => *throws error*

    - *queryBy...:* returns the *matching node* for a query
      - useful for asserting an element that is not present
      - if non-existence, *returns null*

    - *findBy...:* returns a Promise which resolves when an element is found which matches the given query

  - After selecting an element, use *Events API* or *user-event*
    - To fire events and simulate user interactions with the page

### JEST

  - A testing framework
    - Provides default matchers
      - Ex. toBe(), toHaveLength(), toHaveProperty(), toBeGreaterThan()
    - `Expect` function can be used a few timesin the same test to verify more than one behaviour within a single test

### JEST-DOM

  - A library that provides the *DOM specific matchers*
    - Ex. toBeInDocument(), toHaveClass(), toHaveValue()
    - these matchers help verify expected behaviour

### REACT-TESTING-LIBRARY

  - Provides React specific helper functions, including the render function
  - *Render function* => access to functions that help *interact with the DOM*
  - Gives access to a variety of queries provided by the dom-testing-library

### DOM-TESTING-LIBRARY

  - Queries come from the dom-testing-library
  - A query is a combination of a *query variant and a query type*
    - Variant: getBy / queryBy / findBy ...
    - Type: ByRole / ByText / ByPlaceholderText / ByLabelTest ...
  
  - *Guide to Choosing Queries*
    - https://testing-library.com/docs/queries/about/#priority

    1. Queries Accessible to Everyone
        - getByRole
        - getByLabelText
        - getByPlaceholderText
        - getByText
        - getByDisplayValue

    2. Semantic Queries
        - getByAltText
        - getByTitle

    3. Test IDs
        - getByTestId

### MOCK FUNCTIONS

  - Mock functions are a part of the Jest framework and are also known as "spies"
  - A basic mock can be created in any test by calling the `jest.fn()` function
    - Used to gather information for the verification phase of the test

  ```js
  it("doesn't call the function", () => {
    const fn = jest.fn();
    expect(fn).toHaveBeenCalledTimes(0);
  });

  it("calls the function", () => {
  const fn = jest.fn();
  fn();
  expect(fn).toHaveBeenCalledTimes(1);
  });

  it("calls the function with specific arguments", () => {
  const fn = jest.fn();
  fn(10);
  expect(fn).toHaveBeenCalledWith(10);
  });
  ```

<a id="day3lec"></a>
## **DAY 3 LECTURE NOTES**

### CYPRESS

  - `npm install cypress`
  - `integratio` directory
    - `file_name.spec.js`

```js
describe("Weather Form + Buttons Interactions", () => {
  it("loads the page properly", () => {
    cy.visit("/") // can create a property called baseUrl: "..." in cypress.json and .visit() will grab it
  });

  it("can type in the form", () => {
    cy.get("input").type("Montreal");
    cy.get("input").should("have.value", "Montreal");
  });

  it("adds a button for the city that was typed", () => {
    cy.get("input").type("{enter}"); // {enter} is pressing enter key
    cy.get("section div > button").should("have.length", 1);
  });

  it("clears the name of the city that was searched", () => {
    cy.get("input").should("have.value", "");
  });
});

describe("Buttons Duplicates", () => {
  it("loads the page properly", () => {
    cy.visit("/") // can create a property called baseUrl: "..." in cypress.json and .visit() will grab it
  });

  it("can type in the form", () => {
    cy.get("input").type("Montreal");
    cy.get("input").should("have.value", "Montreal");
  });

  it("adds a button for the city that was typed", () => {
    cy.get("input").type("{enter}"); // {enter} is pressing enter key
    cy.get("section div > button").should("have.length", 1);
  });

  it("clears the name of the city that was searched", () => {
    const button = cy.get("section div > button");

    button.click();

    cy.get("section div > button").should("have.length", 1) // using button.should will grab old button (i.e. before clicked)
  });
});

describe("Form Duplicates", () => {
  it("loads the page properly", () => {
    cy.visit("/") // can create a property called baseUrl: "..." in cypress.json and .visit() will grab it
  });

  it("can add a button", () => {
    cy.get("input").type("Montreal");
    cy.get("input").should("have.value", "Montreal");
    cy.get("input").type("{enter}");
    cy.get("section div > button").should("have.length", 1);
  });

  it("should not add a second button", () => {
    cy.get("input").type("Montreal");
    cy.get("input").should("have.value", "Montreal");
    cy.get("input").type("{enter}");
    cy.get("section div > button").should("have.length", 1);
  });
});

describe("Search for city, then another and revisit first city", () => {
  it("loads the page properly", () => {
    cy.visit("/");
  });

  it("should not show the history of cities", () => {
    cy.get('[data-testid="cityHistoryList"] > h1').should("not.exist");
  });

  it("should show weather info for city when searched", () => {
    cy.get("input").type("Montreal{enter}");
    cy.get("div.CurrentWeather > h1").should("have.text", "Current Weather");
  });

  it("should show the history of cities", () => {
    cy.get("input").type("Ottawa{enter}");
    cy.get('[data-testid="cityHistoryList"] > h1').should("exist");
  });
});

```
<a id="day3comp"></a>
## **DAY 3 COMPASS NOTES**

### ENT-TO-END TESTING - CYPRESS

  - To test the full stack integration of the client and the server in a real browser environments
  - Jest is fast because it does not have to render anything
    - Only has to create a representation of the DOM
  
### CYPRESS

  - `npm i -g cypress`
  - Create `cypress.json` file in the root of the project directory
    - Can include baseUrl and viewport size
      ```json
      {
        "baseUrl": "http://localhost:8000",
        "viewportWidth": 1280,
        "viewportHeight": 720
      }
      ```

#### Structures

  - *Arrange* - set up initial app state
    - visit a web page
    - query for an element

  - *Act* - take an asction
    - interact with that element

  - *Assert* - make an assertion
    - make an assertion about page content

#### CYPRESS QUERYING

  - **Selecting Elements**
    - *Anti-Pettern:* using highly brittle selectors that are subject to change
    
    - *Best Practice:* Use `data-*` attributes to provide context to your selectors and isolate them from CSS or JS changes
      1. Do not target elements based on CSS attributes (i.e. id, class, tag)
      2. Do not target elements that may change their textContent
      3. Add `data-*` attributes to make it easier to target elements
          - `data-cy` / `data-test` / `data-testid`

  - `cy.visit():` visit the url with prefix baseUrl
    - include baseUrl in cypress.json
      ```js
      cy.visit('/');
      ```

  - `cy.contains():` get the DOM element *containing the text*
    ```js
    cy.contains('apples')
    cy.get('.nav').contains('About')
    cy.get('form').contains('submit the form!').click()
    ```

  - `cy.get():` get one or more DOM elements *by selector or alias*
    - can be chained with other commands
    - to grab an attribute, use `"[attribute]"`
    - to grab by class name, use `".className"`

      ```js
      cy.get('textarea.post-body').type('This is an excellent post.')
      cy.("li").contains("Tuesday").click();
      cy.get(':checkbox').should('be.disabled')
      ```

  - `cy.should():` create an assertion 
    - Assertions are automatically retried until they pass or time out

    ```js
    cy.get(':checkbox').should('be.disabled')
    cy.get('form').should('have.class', 'form-horizontal')
    cy.get('form').should('have.css', 'background-color', 'rgb(242, 242, 242)')
    cy.get('input').should('not.have.value', 'US')
    cy.contains("Deleting").should("exist");
    cy.contains("Deleting").should("not.exist");
    ```

  - `cy.type():` type into a DOM element
    - Can include special character (i.e. {enter})

    ```js
    cy.get('input').type('Hello, World')
    cy.get("input").type("Montreal{enter}")
    ```
  
  - `cy.request():` make an HTTP request
    
    ```js
    cy.request("GET", "/api/debug/reset");
    ```

  - `cy.clear():` lear the value of an input or textarea

#### CYPRESS DEFAULT ASSERTIONS

  - All DOM based commands automatically wait for their elements to exist in the DOM
    - *cy.visit()* expects the page to send text/html content with a 200 status code.
    - *cy.request()* expects the remote server to exist and provide a response.
    - *cy.contains()* expects the element with content to eventually exist in the DOM.
    - *cy.get()* expects the element to eventually exist in the DOM.
    - *.find()* also expects the element to eventually exist in the DOM.
    - *.type()* expects the element to eventually be in a typeable state.
    - *.click()* expects the element to eventually be in an actionable state.
    - *.its()* expects to eventually find a property on the current subject.

  - **Reversing the default assertion**
    - Add `.should('not.exist')`
      ```js
      // now Cypress will wait until this
      // <button> is not in the DOM after the click
      cy.get('button.close').click().should('not.exist')

      // and now make sure this #modal does not exist in the DOM
      // and automatically wait until it's gone!
      cy.get('#modal').should('not.exist')
      ```

#### CYPRESS COMMANDS ARE AYNCHRONOUS

#### CYPRESS COMMANDS RUN SERIALLY
  
  - Cypress ensures the state of the application matches what the commands expect about it

  ```js
  it('changes the URL when "awesome" is clicked', () => {
  cy.visit('/my/resource/path') // 1.

  cy.get('.awesome-selector') // 2.
    .click() // 3.

  cy.url() // 4.
    .should('include', '/my/resource/path#awesomeness') // 5.
  })
  ```
  - Visit a URL *and wait for the page load event to fire after all external resources have loaded*
  - Find an element by its selector *and retry until it is found in the DOM*
  - Perform a click action on that element *after we wait for the element to reach an actionable state*
  - Grab the URL and...
  - Assert the URL to include a specific string *and retry until the assertion passes*

#### CYPRESS-MOCHA HOOKS

  - Cypress has adopted Mocha's bdd syntax
  - Mocha provies the following hooks:
    - *before()*
    - *after()*
    - *beforeEach()*
    - *afterEach()*
  - Hooks are used to set up preconditions and clean up after tests

    ```js
    describe('hooks', function() {
      before(function() {
        // runs once before the first test in this block
      });

      after(function() {
        // runs once after the last test in this block
      });

      beforeEach(function() {
        // runs before each test in this block
      });

      afterEach(function() {
        // runs after each test in this block
      });

      // test cases
      it("...", () => {
        ...
      });
    });
    ```

<a id="day4lec"></a>
## **DAY 4 LECTURE NOTES**

### CLASS REVIEW

```js
class Rectangle {
  //takes parameters when a variable is created using class
  constructor(width, length) {
    this.width = width;
    this.length = length;
  };

  // methods (similar to functions)
  calculateArea() {
    return this.width * this.length;
  }
};

// creates an object using class Rectangle
const rectangle = new Rectangle(5, 4);
console.log(rectangle); // { width: 5, length 4 }
console.log(rectangle.calculateArea()); // 20

// 'extends' keeps the contents of Rectangle
class RectangularPrism extends Rectangle {
  constructor(width, length, height) {
    super(width, length) // calls the super class and brings in the values
    this.height = height;
  }

  calculateVolume() {
    // return this.width * this.length * this.height;
    return this.calculateArea() * this.height;
  }
};

const prism = new RectangularPrism(6, 7, 5);
console.log(prism); // {width: 6, length: 7, height: 5}
console.log(prism.calculateVolume()); // 210
```

### REACT CLASS

```jsx
// App.js
import ClassCompoennt from '';

function App() {
  return (
    <div className="App">
      <h1>Class-based!!!!</h1>
      <ClassComponent someProps={"I am an awesome prop"} />
    </div>
  );
}


// ClassComponent.jsx
import { Component } from 'react';

const ClassComponent extends Component {
  // Component contains properties such as props, state, super(), etc.
  // Hooks cannot be called in class based Component because they are already there
  //  Hooks are used to "hook" things from class based Component

  constructor(props) {
    super(props);
    this.state = {
      counter: 0
    }

    this.increment = this.increment.bind(this); // need to bind this because this falls out of the scope
  };

  increment() {
    this.setState({counter: this.state.counter + 1})
  }

  render() {
    console.log(this) // this refers to ClassComponent
    // const { someProp } = this.props;
    return (
      <section>
        <h2>The Class Components</h2>
        <p>{someProp}</p>
        <p>{this.props.someProp}</p>
        <p>The counter is currently at {this.state.counter}!</p>
        <button onClick={this.increment}> increment</button>
      </section>
    );
  };
  
};

export default ClassComponent;
```

```jsx
// App.js
import { BrowserRouter as Router, Link, Rote, Routes } from 'react-router-dom';
import LifeCycle from '';

function App() {
  return (
    <div className="App">
      <h1>Class-based!!!!</h1>
      <Router>
        <nav>
          <Link to="/class">class component</Link> // goes to localhost:3000/class
          <br />
          <Link to="/lifecycle">lifecycle component</Link> // goes to localhost:3000/lifecycle
        </nav>

        <Routes>
          <Route path="/class" element={<ClassComponent someProp="very cool"}/>
          <Route path="/lifecycle" element={<LifeCycle />} />
        </Routes>
      </Router>
      <LifeCycle />
    </div>
  );
}

// LifeCycle.jsx
import { Component } from 'react';

class LifeCycle extends Component {
  constructor(props) {
    super(props);
    this.state() {
      searchTerm: "",
      interval: null
    }
    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(e) {
    this.setState({searchTerm: e.target.value});
  }

  componentDidMount() {
    console.log('this component is mounted');

    const interval = setInterval(() => {
      console.log(`I'm the interval that was running`)
    }, 2000);

    this.setState({interval: interval});
    // axios.get('')
    //   .then((res) => {this.setState({data: res.data})})
  }

  componentDidUpdate(prevProps, prevState) {
    // console.log(prevState);
    console.log('the component had an update');

    // if (prevProps.user !== this.props.user) {
    //   axios.get(`/api/user/${user}`)
    // }
  }

  componentWillUnmount() {
    console.log('I am about to unmount!');
    clearInterval(this.state.interval);
  }

  render() {
    return (
      <section>
        <h2>Lifecycle Component</h2>
        <p>the search term is {this.state.searchTerm}</p>
        <input
          value={this.state.searchTerm}
          onChange={this.handleChange}
        />
      </section>
    );
  }
}
```

### REACT-ROUTER-DOM

<a id="day4comp"></a>
## **DAY 4 COMPASS NOTES**

### REACT CLASS COMPONENTS

#### CLASSES

```jsx
import React, { Component } from "react";

  class Application extends Component {
  render() {
    return <div></div>;
  }
  } 
```

  1. All class-based React components must *extend* the *React.Component* class
      - Access to some of the common component API functions
  2. All class-based React components must overried the *render* method of the *React.Component* superclass that they *extend*
      - *render* method in a class returns the React elements

#### CONSTRUCTOR

```jsx
import React, { Component } from "react";

class Application extends Component {
 constructor(props) {
  /* If we add a constructor to our class, we must pass props to the super class */
  super(props);
 }

 render() {
  return <div></div>;
 }
}
```

  - If a *constructor* is added to the class, *props* must be passed to the *super class*
    - A constructor must call the *super(prop)* method
  
#### COMPONENT INSTANCES

```jsx
class Counter extends Component {
 render() {
  return <button onClick={this.props.onClick}>{this.props.count}</button>;
 }
}

class Application extends Component {
 state = {
  count: 0
 };

 increment = event => {
  this.setState(previousState => ({
   count: previousState.count + 1
  }));
 };

 render() {
  return <Counter onClick={this.increment} count={this.state.count} />;
 }
}
```

  - *React.Component* class definitin provides common methods and properties used to access props and manage state
    - Every component that is created as a class inherits:
      - *this.props*
      - *this.state*
      - *this.setState*

  - *Counter* component accepts two props: *this.props.onClick* and *this.props.count*
  - *Application* component sets the initial state using a class property
  - In the render method of the Application component, the *increment* instance method can be accessed using *this*
  - *State* can be stored in an object called state, which can be changed using the *setState* method

#### SETTING STATE

  1. Never set state directly
      - use *setState* method to change state

  2. State updates are merged
      ```jsx
      class App extends React.Component {
        state = {
          unchanged: true,
          visible: false
        };

        show = event => {
          this.setState({
            visible: true
          });
        };
      }
      ```
      - Only the value of *visible* property is updated
      - The value of *unchanged* will remain unaffected
      - *setState* does not overwrite the whole state object
        - With Hooks, we would have to use:
          - `setState({...state, show: visible})` to retain the unchanged state

  3. State updates are asynchronous

#### Lifecycle

  - With class-based components, *lifecycle* methods are the API used to perform *side effects*
    - Side effects like data fetching or connecting to a WebSocket whent he component mounts to the DOM
  - Lifecycle methods inform when a component updates or when React is about to remove one from the DOM


### COMPONENT LIFECYCLE

  - Components declared as classes provide the option to override certain "lifecycle methods"
    - React library calls these methods when certain events occur while app is running
  
#### FIRST PHASE - MOUNT

  - Occurs when a component is created
  - 3 most important lifecycle methods:
    1. *constructor*
    2. *render*
    3. *componentDidMount*

#### SECOND PHASE - UPDATE

  - A component that is mounted can be updated
  - Two ways to udate components:
    1. Pass them props when a parent renders
    2. Update the internal state
  - Each time the component is updated, React calls the update lifecycle methods
    1. *render*
    2. *componentDidUpdate*
      - has access to the props and state from the previous update
      - compare them to the existing state

#### THIRD PHASE - UNMOUNT

  - Only happens once and the only lifecycle method that React will call during this phase:
    - *componentWillUnmount*

```jsx
class Dashboard extends Component {
  state = { /* do not replace your initial state */ };

  componentDidMount() {
    const focused = JSON.parse(localStorage.getItem("focused"));

    if (focused) {
      this.setState({ focused });
    }
  }

  componentDidUpdate(previousProps, previousState) {
    if (previousState.focused !== this.state.focused) {
      localStorage.setItem("focused", JSON.stringify(this.state.focused));
    }
  }

  render() { /* do not replace your render method */ }
}
```

![React Component Lifecycle Diagram](https://i1.wp.com/programmingwithmosh.com/wp-content/uploads/2018/10/Screen-Shot-2018-10-31-at-1.44.28-PM.png?resize=1024%2C567&ssl=1)

### RUBY

#### RUBY VERSION MANAGEMENT (RVM)

```
// check Ruby version
ruby -v
ruby --version

// check currently install Ruby versions
rvm
rvm ls
```

#### irb - THE RUBY SHELL

  - Similar to Node CLI, `irb` command can be used to launch a REPL

```
irb
puts "Hello, what's your name?" // asks for input - name
name = gets.chomp // user-input
putputs "Welcome to \"Ruby land\", #{name}. Hope you enjoy your stay (and never leave!)" // prints with name assigned
```

#### GEMS (PACKAGES)

  - 3rd party libraries similar to npm
    - i.e. Rails

```
gem
gem list
```

<a id="day5lec"></a>
## **DAY 5 LECTURE NOTES**

### RUBY

  - **Data Types**
    - Booleans
    - Symbols (used a lot unlike JS)
    - Integers
    - Floats
    - Strings
    - Arrays
    - Hashes (objects)

  - No need to include const, let for declaring variables
  
```ruby
greeting = "Hello team!"
empty_str = ""

# string interpolation
# "" and '' are different
puts "Greeting: #{greeting}" # Greeting: Hello team!
puts 'Greeting: #{greeting}' # Greeting: #{greeting}

# include ? for boolean
puts greeting.empty? #false
puts empty_str.empty? #true
```

#### ARRAYS

```ruby
players = ['LeBron', 'Jordan', 'Curry', 'Durant']

puts players.first
puts players.last
puts players.last(2) # Curry Durant

result = players.shuffle # shuffles the order of the array
result = players.rotate # push array by 1
puts result.inspect # print array as is - if not included , each element in array printed in new line

result = players.map { |plaeyer| player.upcase }
puts result.inspect

numbers = [1,2,3,4,5,6]

puts numbers.reduce(0) { |sum, num| sum + num }
```

```ruby
scrabble_words = ["QUARTZY", "OXAZEPAM", "QUIZZIFY", "OXYPHENBUTAZONE", "QUIXOTRY"]

scrabble_words.each do |word|
  puts "Word: #{word}"
end

scrabble_words.each_with_index do |word, index|
  puts "Word: #{word.reverse} index: #{index}"
end

# do ... end is a block
scrabble_words.each_with_index do |word, index|
  if (word.length == 8) # == is equivalent to === in JS
    puts "Word: #{word.reverse} index: #{index}"
end
```

#### ITERATORS

  - *do* and *end* replace {}

```ruby
10.times do |n|
  puts n
end

# prints from 5 to 10
5.upto(10) do |n|
  puts n
end

# prints every 10 from 0 to 100
(0..100).step(10) do |n|
  puts n
end
```

#### BLOCKS

  - Ruby blocks are annonymous functions that can be passed to methods
  - Ruby blocks are the equivalent of JS callbacks

```ruby
def multiple(limit)

  multipleArr = []

  1.upto(limit) do |n|
    #do something
    multipleArr.push(yield n) # yield n calls { |n| n * 3 } 
  end
  multipleArr # no need to include return - the last line in the function is the implicit return
end

result = multiple(5) { |n| n * 3 } # what's in {} is like a callback (n) => { n * 3 }
puts results
```

#### HASHES (OBJECTS)

  - To access hash/object:  
    - JS => either .key or ["key"]
    - Ruby => only [:key]

```ruby
famous_painter = {
  first_name: "Pablo",
  last_name: "Picasso",
  date_of_birth: 1881,
  date_of_death: 1973
}

# puts famous_painter.date_of_birth will not work because Ruby will think of .date_of_birth as a method
puts famous_painter[:date_of_birth]

famous_painter.each do |key, val|

  puts "Key: #{key} Value: #{value}"

end
```

```ruby
famous_painters = [
  {
  first_name: "Pablo",
  last_name: "Picasso",
  date_of_birth: 1881,
  date_of_death: 1973
  },
  {
  first_name: "Pierre Auguste",
  last_name: "Renoir",
  date_of_birth: 1841,
  date_of_death: 1919
  }
]

puts famous_painters.first[:date_of_birth] # 1881

famous_painter.each do |painter|

  painter.each do |key, val|
    puts "Key: #{key} Value: #{value}"
  end

end
```

#### HASH VS. OBJECT

  - Dot notation to access properties cannot be used with hases
  - Dot notation to access properties can be used with objects
  