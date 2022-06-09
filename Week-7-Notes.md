# **Jeffery Park's LHL Week 7 Notes**

## **Table of Contents**
- [DAY 1 COMPASS NOTES](#day1comp)
- [DAY 2 LECTURE NOTES](#day2lec)
- [DAY 2 COMPASS NOTES](#day2comp)
- [DAY 3 LECTURE NOTES](#day3lec)
- [DAY 3 COMPASS NOTES](#day3comp)
- [DAY 4 LECTURE NOTES](#day4lec)
- [DAY 4 COMPASS NOTES](#day4comp)
- [DAY 5 LECTURE NOTES](#day5lec)
- [DAY 5 COMPASS NOTES](#day5comp)
- [DAY WE COMPASS NOTES](#dayWEcomp)


<a id="day1comp"></a>
## **DAY 1 COMPASS NOTES**

### REACT STATE

  - In CS, the state of a program is defined as its *condition regarding stored inputs*
    - *Current values or contents*
  - The state in React allows to *dynamically change* one or many elements at once based on *one variable*
    - Change based on *user input*
    - *Keep track of information* across multiple renders
  - `useState()` hook to store state
    - *Hooks* - a React feature
    - A method of the React object
  
  - **useState()**
    - Import the useState hook into the module
    - useState function receives an *optional argument* - *default value for the state*
    - *useState returns an array*
      - uses array destructuring syntax to return two different values
      - *first element:* a reference to get the current value of the state
        - to get a value (i.e. *getter*)
      - *second element:* a function that can update the state and re-render
        - to set a value (i.e. *setter function*)
    
      ```js
      import React, { useState } from "react";

      function Application(props) {
        // array destructuring for useState()
        const [count, setCount] = useState(0);

        return (
          <main>
            <Button onClick={(event) => setCount(count + 1)}>Increment</Button>
            <h1>Button was clicked {count} times.</h1>
          </main>
        );
      }
      ```
    - useState() hook can be used by calling it *inside components*
      - Must be called in a React function component and *top of the component function*
      - Hooks should *not be inside conditionals, looks or other functions*
    - *Naming Rule for Destructuring useState()*
      - `const [state, setState] = useState(0);`
        - first element can be set tp anything
        - second element must start with *set*
    - *Default value* for state can be specified as `useState(startingValue)`
      ```js
      // anger's default value set to 0
      const [ anger, setAnger ] = useState(0);
      // light's default value set to "off"
      const [light, setLight] = useState("off");
      ```
    - *setState* is a *function* that can *change the value of state*
      - Used to *assign a new value to the state*
        ```js
        function LightSwitchButton(props) {
          { light, setLight } = props
          // light on and off
          // const [light, setLight] = useState("off");

          const handleClick = () => setLight(light === "off" ? "on" : "off");

          return (
            <button onClick={handleClick} className="LightSwitchButton">
              {light === "on" && <span className="on"><i>💡</i> I'm on!</span>}
              {light === "off" && <span className="off"><i>💡</i> I'm off!</span>}
            </button>
          );
        }
        ```
    - **Sharing State**
      - Moving it up to the closest common ancestor of the components that need it
        - *"lifting state up"*
      - Functions can be passed down as props
        - Functions in the children will run with the context of the parents
      - Keep the logic that changes the state near the declaration
        - Declare state, prepare the logic and pass down pre-made function
        ```js
        function App() {
          const [light, setLight] = useState('off');
          const switchLight = () => setLight(light === "off" ? "on" : "off");
        }
        ```

### CONTROLLED COMPONENTS

  - `<form>` elements keep track of their own state
  - `<input>, <textarea> and <select>` elements keep track of their current value
  - Preferable to use *React to track the entire application's state*
    - Instead of using HTML's built-in state management
  - *Controlled Components:* creating components that override HTML form elements to let React control their state
    1. Setting a variable that is stored in state as the *value attribute* on the form element
    2. Using an *onChange* event that uses the setter of your state to set a new value when the input changes
      - Value of onChange event stored in `event.target.value`
    ```js
    function DisplayWord(props) {
      const [word, setWord] = useState("");
      return (
        <main>
          <input
            value={word}
            onChange={(event) => setWord(event.target.value)}
            placeholder="Please enter a word"
          />
          <h1>Your word is: {word}.</h1>
        </main>
      );
    }
    ```
      - input element becomes a controlled component when a value prop and an onChange event handler that can update the value are provided

### FRAGMENTS

  - Components can only return JSX with one root element
  - Unnecessary `<div>` tags can result in bugs related to CSS
    - Creates extra DOM node
  - `<Fragment>` from the React library can be used instead
    - Acts as a *"dummy root element"*
    - *Does not create exotra DOM node*
    - `<>` for shorthand for `<Fragment>`
      - Does not accept attributes (props)
    ```js
    // creating root element using div - creates extram DOM node and may create bugs
    return (
      <div>
        <h1>A heading</h1>
        <p>A paragraph</p>
      </div>
    )

    // creating root element using Fragment
    import React, { Fragment } from 'react';
    return (
      <Fragment>
        <h1>A heading</h1>
        <p>A paragraph</p>
      </Fragment>
    )
    ```

  - JSX supports conditional expression using ternary and short circuit operators
    - Ternary and short circuit operators must return "single value"
    ```js
    // results in error - each expression does not return "single value"
    const userLoggedIn = false;
    return (
      <Fragment>
        {userLoggedIn ? 
          <h1>Success!</h1>
          <p>You are logged in.</p>
        : 
          <h1>Warning!</h1>
          <p>You are not logged in</p>
        }
      </Fragment>
    )

    // works - each expression is wrapped in fragment, which wraps the elements and returns "one value"
    const userLoggedIn = false;
    return (
      <Fragment>
        {userLoggedIn ? 
        <>
          <h1>Success!</h1>
          <p>You are logged in.</p>
        </>
        :
        <>
          <h1>Warning!</h1>
          <p>You are not logged in</p>
        </>
        }
      </Fragment>
    )
    ```

### DEVELOPMENT ENVIRONMENTS FOR MODERN USER INTERFACE DEVELOPMENT

#### STORYBOOK

  - The Storybook environment is designed to speed up the develpment and *testing of individual components*
  - If you want to manually test your components in isolation

#### WEBPACK DEV SERVER

  - Provides a live development environment that *updates the browser when a file is saved*
  - For development only
  - If you want to run your entire application in development mode

#### JEST: TEST RUNNER

  - *JS testing framework* - not a React testing
    - Will be used instead of Mocha & Chai library
  - Allows to test the values produced by the codes
  - If you want to run unit or integration tests from the command line

#### CYPRESS: END-TO-END TESTING

  - If you want to run automated end-to-end tests in the browser

### BABEL: THE JAVASCRIPT COMPILER

  - Bebel is a tool used to conver ES2015+ JS into a backwards compatible version of JS
    - Ex. arrow function converted to the equivalent ES% compatible code
      ```js
      // Babel Input: ES2015 arrow function
      [1, 2, 3].map((n) => n + 1);

      // Babel Output: ES5 equivalent
      [1, 2, 3].map(function(n) {
        return n + 1;
      });

      // Babel Input: JSX
      const element = <h2 className="name">Name</h2>

      // Babel Output: ES5 equivalent
      const element = React.createElement("h2", {
        className: "name"
      }, "Name");
      ```

<a id="day2lec"></a>
## **DAY 2 LECTURE NOTES**

### REACT COMPONENTS RULES

  0. `import React from 'react';` - optional

  1. `Make a function` - preferably the same name as the file
      - To say this is a component
      ```js
      const Navbar = function () {

      }
      ```
  
  2. `Export the function` - equivalent to module.exports
      - Newer version
      - To use the function in the main page
      ```js
      export default Navbar;
      ```

  3. `Components must return something to render`
        ```js
      const Navbar = function () {
        return (
          <h1>Helo, World</h1>
        )
      }
      ```
  
  4. `Components must have one parent element wrapping everything`
     - Can't have multiple parent elements (i.e. multiple of only h1 tags)
      ```js
      const Navbar = function () {
        return (
          <>
            <h1>Helo, World</h1>
            <h1>Helo, World</h1>
            <h1>Helo, World</h1>
          </>
        )
      }
      ```

### PROPS

  - Passed down as an object
  - Can be used in components with {}
    - {props.name}

### STORYBOOK

  ```js
  import { storiesOf } from '@storybook/react';
  import Navbar from '../components/Navbar';

  // main category in storybook
  storiesOf('Test')
    // sub-categories - for different conditions
    .add('Default Navbar', () => <h2>Hello, World</h2>)
    .add('Default Navbar 1', () => <h2>Hello, World</h2>)
    .add('Default Navbar 2', () => <h2>Hello, World</h2>)

  storiesOf('Navbar')
    .add('Default Navbar', () => <Navbar />)
    .add('Navbar with a prop title', () => <Navbar title="Fake LinkedIn App>)
  ```

<a id="day2comp"></a>
## **DAY 2 COMPASS NOTES**

### STORYBOOK

  - Allows to test event handling in isolation
    - Installation: https://github.com/storybookjs/storybook/tree/master/addons/actions
    - `import { action } from "@storybook/addon-actions";`
  
  - **action()** from storybook add-on actions
    - Mechanism that logs user interactions and data
    - Higher-order function - a function that returns another function
      - When action() is called, a new function is returned
    - Allows to create a callback that apperas int he Storybook action panel when event happends

  - **To Add Stories**
    - *Import component* in the storybook .js file
    - Add *storiesOf("string", module)* function
      - *string:* label for the group of stories
      - *module:* webpack module, which is available on the global scope
    - Below storiesOf() function, include/chain *.addParameters()* function
      - Can pass an object of parameters (i.e. set background styling)
    - Add stories by chaining *add("string", function())* function
      - *string:* name of the story
      - *function():* function that returns a React component

### CLASSNAMES

  - JS utility for *conditionally joining classnames* together
  - `className()` function takes any number of arguments which can be a string or object
    - Value associated with a given key is only return is true
    - *Falsy values (i.e. null, false, 0) are ignored*
    ```js
    import classNames from "classnames";

    classNames('foo', 'bar') // => 'foo bar'
    //  returns bar if true
    classNames('foo', { bar: true }) // => 'foo bar'
    classNames('foo', { bar: false }) // => 'foo'

    // dynamic class names
    let buttonType = 'primary';
    classNames({ [`btn-${buttonType}`]: true });
    ```
  
  - **Usage with React.js**
    - Make dynamic and conditional classNames props
      ```js
      let btnClass = classNames({
        "button": true,
        "button--confirm": props.confirm,
        "button--danger": props.danger
      })
      ```

<a id="day3lec"></a>
## **DAY 3 LECTURE NOTES**

### NPX
  
  - Install => use its functionality => get rid of it
  - If installed with npm, stuck with the version installed at the time of installation

### WEBPACK & BABEL

  - Webpack maps the file dependencies
    - Figures out and inserts script tags automatically
  - Babel transfiles (i.e. converts JSX to older syntax of JS)

### PROPS

  - Props can be passed down from the parent to its children
    - Like function arguments
    - Similar to attributes; key-value pair
      - `<Header key={"value"} />`
    - Attribute name (i.e. key) can be anything
  - Props can be used by children by including in function parameter

### IMMUTABLE

  - Primitives (i.e. data that is not object - string, number, bigint, boolean, undefined, symbol, and null) are immutable
  - Objects (i.e. functions, arrays) are mutable
    - Can change their values
  - **Immutability**
    1. copy the original
    2. Change something in it
    3. Set the copy to the original
  ```js
  const burrito = {
    type: 'bowl',
    vegetarian: true,
    ingredients: ['lettuce', 'black beans']
  };

  const copy = burrito;
  copy.type = 'whole wheat tortilla';

  // buttiro object's type also changed to 'whole wheat tortilla' - mutating burrito object
  // because copy is **referencing** burrito object
  console.log(burrito);
  console.log(copy);

  // to make a new copy of burrito - use spread syntax
  const copy = {...burrito};

  // copy and mutate - changes type value
  const copy {...burrito, type: 'whole wheat tortilla'};

  // mutates the original object because the spread operator only copies the first layer
  copy.ingredients.push('guac');

  // also spread the array and pass in new value to avoid mutating the original object
  const copy {...burrito, type: 'whole wheat tortilla', ingredients: [...burrito.ingredients, 'guac']};
  ```


<a id="day3comp"></a>
## **DAY 3 COMPASS NOTES**

### PROP DRILLING (THREADING)

  - Process to go through to get data to parts of the React component tree
  - Try to reduce the number of props passed down

### CONTROLLED COMPONENTS / LISTS

  - **Controlled components** use *HTML form elements*
    - input, textarea, select
      - has *value* and *onchange* attributes
    - Use *React state* to store their current value and update them
  - **value**
    - set using a variable stored in state
  - **onChange**
    - event that fires the setter function
    - set a new value when input changes
  - *select* element has built-in functionality
    - Built-in value and onChange event handler
    - However, it manages *its own state*
  - *ul* and *li* are commonly used in React to create lists
    - Able to manage the state and easier to style
    - However, do not come with built-in value or an onChange event handler
      - Use React props to assign data
  
  - **Controlled lists**
    - Similar to using *value* and *onChange* keywords in input and selects elements, pass down *value* and *onChange* as props
    - Easy to tell that it is expecting user input (for other developers)
      ```js
      <ul>
        <DayList 
          days={days} 
          value={day} 
          onChange={setDay} 
        />
      </ul>
      <li>
        <DayListItem
          key={props.id} 
          name={props.name} 
          spots={props.spots} 
          selected={props.name === props.value}
          setDay={props.onChange}
        />
      </li>
      ```

<a id="day4lec"></a>
## **DAY 4 LECTURE NOTES**

### RULES FOR HOOKS

  - Must be called top-level (not called conditionally)
  - Must be called in a react function (functional component or custom hook)
  - Must start with *use*
    - i.e. useState, useEffect

### PURE FUNCTION

  - No side-effects
    - **side-effects:** when the function reaches outside of itself to do something
      - has an observable effect besides returning a value (the main effect)
      - i.e. making requests to an API server
      ```js
      const addThree = (n) => {
        const result = n + 3;
        console.log(result); // reaching outside the function to use console.log
        return result;
      }

      const additionVal = 4;
      const addFour = (n) => {
        return additionVal + n; // reaching outside the function to call additionVal
      }
      ```
  - Output is deterministic
    - output is predictable
      ```js
      const addTwo = (n) => n + 2;
      ```

### USEEFFECT HOOK

  - useEffect() hook to reach outside the function
    - runs the App
    - return runs first
      - DOM is painted with the html elements
    - useEffect() runs to update the title
      - callback runs after the return

```js
import { useEffect, useState } from 'react';

function App() {
  const [ counter, setCounter ] = useState(0);
  const [ searchTerm, setSearchTerm ] = useState();

  useEffect(() => {
    // setCounter(counter + 1) // counter increases infinitely because it re-renders the page and this useEffect() is run again
    
    setCounter((prev) => prev + 1); // prev is equal to the current counter value
  }, []) // [] if no change, doesn't run


  // updates the title after the return paints the DOM
  useEffect(() => {
    document.title = `${counter} Awesome App`;
  })

  // console.logs after the return
  useEffect(() => {
    // setTimeout(() => {
    //   console.log(`the counter is currently at ${counter}`)
    // }, 3000);

    // prints previous counter values as well
    // setInterval (() => {
    //   console.log(`the counter is currently at ${counter}`)
    // }, 3000);   

    const interval = setInterval (() => {
      console.log(`the counter is currently at ${counter}`)
    }, 3000);

    return () => {
      clearInterval(interval);
      console.log('interval has been cleared');
    }
  }, [counter]) // giving a condition to only clearInterval if counter value changes
                // in array because multiple values can be included and checked (i.e. [counter, searchTerm])

  return (
    <div className="App">
      <h1>the awesome app</h1>
      <button onClick={() => setCounter(counter + 1)}>increment counter</button>
      <div>
        <p>the current search term is {searchTerm}</p>
        <input
          value={searchTerm}
          onChange={(e) => setSearchTerm(e.target.value)}
        />
      </div>
    </div>
  )
}
```

#### USEEFFECT FLOW

  - Turns our jsx into html and renders it on the DOM
  - The browser responds and updates the UI
  - Run any clean up from our effects of the previous render
  - Then run our side-effects

### DATA

```js
import { useEffect, useState } from 'react';
import Appointments from '';
function App() {
  const [ counter, setCounter ] = useState(0);
  const [ searchTerm, setSearchTerm ] = useState();

  return (
    <div className="App">
      <h1>the awesome app</h1>
      <Appointments />

    </div>
  )
}

============================================================

import { useEffect, useState } from 'react'; // useEffect since we are grabbing data from outside the function
import axios from 'axios' // axios to just grab Ajax from jQuery - jQuery is too large to use if we only want to use Ajax
function Appointments() {
  const [ appointments, setAppointments ] = useState({});
  const [ selectedAppointment, setSelectedAppointment ] = useState(null);
  const [ appointmentId, setAppointmentId ] = useState('');

  useEffect(() => {
    axios.get('http://localhost:8001/api/appointments')
      .then((res) => {
        console.log(res.data); // prints the data fetched
        setAppointments(res.data); // re-renders every time this is run without [] as the second parameter
      })
  }, []) // prevents from re-rendering and telling to run useEffect() only once - empty to check if anything is changing - if not, stops

  useEffect(() => {
    const targetAppointment = appointments[appointmentId];
    console.log(targetAppointment);
    setSelectedAppointment(targetAppointment);
  }, [appointmentId, appointments])

  return (
    <section>
      <h1>the awesome app</h1>
      <p>you have {Object.keys(appointments).length} appointments</p>
      <div>
        <p>the selected appointment id is {appointmentsId}</p>
        <input 
          value={appointmentId}
          onChange={(e) => setAppointmentId(e.target.value)}
        />
      </div>
      {selectedAppointment && (
        <div>
          <h2>selected appointment</h2>
          <p>appointment id: {selectedAppointment.id}</p>
          <p>appointment time: {selectedAppointment.time}</p>
        </div>)
      }
    </section>
  );
}
```

<a id="day4comp"></a>
## **DAY 4 COMPASS NOTES**

### CORS (CROSS-ORIGIN RESOURCE SHARING)

  - Mechanism that allows a website from *one url to request data from another url*
  - Website freely request data from its own url (i.e. foo.com =GET> foo.com)
    - Blocks anything from an external url (i.e. foo.com =GET> bar.com)
      - Ex. Fail when fetching API from my website (i.e. localhost:5000 => localhost:3000)
      - Ex. Broken image when using an image on my website that is on another url
    - Fails because the *browser implements the same origin policy* as part of its security model
      - Allows requests (i.e. images/data) from its own url
      - Blocks requests from an external url unless certain conditions are met
  - When browser makes a request, it adds an *origin header* to the request message
    - If it goes to the server with the same origin, it passes
    - If it goes to a different url => *cross origin request*
      - CORS error and prevents response unless responding with proper header
  - Resolved by controlling the server and configuring it to response with a proper header
  - Avoid using CORS by proxy-ing requests to the API server

### PROXYING API REQUESTS IN DEVELOPMENT

  - The front-end React app is often served from the same host and port as their backend implementation
    ```js
    /             - static server returns index.html with React app
    /todos        - static server returns index.html with React app
    /api/todos    - server handles any /api/* requests using the backend implementation
    ```
  - To tell the development server to proxy any unknown requests to your API server in development
    - Add a proxy field to package.json file
      - Ex. "proxy": "http://localhost:4000"
    - This way, doing `fetch('/api/todos')` in development, the development server will recognize that it is not a static asset
      - Will proxy the request to `http://localhost:4000/api/todos` as a fallback
  
### USEFFFECT

  - A hook that allows to safely manage side effects within the component function calls
  - React *calls the function* provided to the useEffect method of a component *after render*
    1. React
        - Run all component functions to generate React element tree
        - Store effect functions for after paint
        - Apply changes to the DOM

    2. Render
        - Paint the required elements based on the current DOM

    3. Call function
        - Run all effect functions submitted uring render

  - **Dependencies**
    - To run useEffect only when the state changes
      - Pass an array as an optional second argument to useEffect()
        ```js
        useEffect(() => {
          if(results.length > 0) {
            console.log("Results Set");
          }
        }, [results]); // Only re-run the effect if results changes
        ```
  
#### RULES OF HOOKS

  1. DO NOT call Hooks inside loops, conditions or nested functions
      - Use the condition inside
        - useEffect is called every time, but the console.log is not
        ```js
        function LiveSearch(props) {
          const [term, setTerm] = useState("");
          const [results, setResults] = useState([]);

          // WRONG
          if(results.length > 0) {
            useEffect(() => console.log("Results Set"));
          }

          // CORRECT
          useEffect(() => {
            if(results.length > 0) {
              console.log("Results Set");
            }
          });

          return (
            <>
              <SearchBar value={term} onChange={setTerm} />
              <Results results={results} />
            </>
          );
        }
        ```
  
  2. Only call Hooks from inside React components (i.e. inside the function)

  3. The effect method that is passed to useEffect must either return undefined or a function

### AXIOS

  - Third party library for explicitly performing data fetching - HTTP requests (i.e. jQuery's built-in $.ajax function)
    - React does not have a built-in function for fetching data
  - `npm install axios`
  - **Four Common Methods**
    - axios.get(url[, config])
    - axios.post(url[, config])
    - axios.put(url[, config])
    - axios.delete(url[, config])
  - Making a GET request:
    - Axios library will provide a *response object* when the Promise resolves
    - Promise catch method to handle *errors*
    ```js
    import axios from "axios";

    axios.get("/api/appointments")
      .then((res) => {
        console.log(res);
      })
      .catch((error) => {
        console.log(error.response.status);
        console.log(error.response.headers);
        console.log(error.response.data);
      })
    ```
  - Send data to the server:
    - Need to provide a second argument
      - Object that contains the data for the record that is being updated
    ```js
    axios
      .put(`/api/appointments/2`, {
        id: 2,
        time: "1pm",
        interview: {
          student: "Archie Cohen",
          interviewer: 9,
        },
      })
      .then((res) => {
        console.log(res);
      });
    ```

<a id="day5lec"></a>
## **DAY 5 LECTURE NOTES**

### CUSTOM HOOKS

  - A JS function that uses a hook
  - Separate the logic from the presentation
  - All hooks need to start with *use*

  ```js
  // To make a custom hook for the following useEffect since it will be used in multiple pages
  //    useEffect(() => {
  //      document.title = title;
  //    }, [title]);
  ////////////////////////////////////////////////////////////////////////////////////////////
  // useDocumentTitle.js
  // below custom hook can be used like a function in the component
  import { useEffect } from 'react';

  Function useDocumentTitle(title) {
    useEffect(() => {
      document.title = title;
    }, [title]);
  }
  ////////////////////////////////////////////////////////////////////////////////////////////
  ```

  ```js
  // Mouse.jsx
  import { useState, useEffect } from 'react';
  import useMousePosition from '../hooks/useMousePosition';
  import useDocumentTitle from '../hooks/useDocumentTitle';

  const Mouse = () => {
    const mousePosition = useMousePosition()
    useDocumentTitle(`X: ${mousePosition.x}, Y: ${mousePosition.y}`)
    /*
    const [mousePosition, setMousePosition] = useState({ x: 0, y: 0});

    useEffect(() => {
      // give function a name to refer to it later
      const mousemoveHandler = (e) => {
        setMousePosition({
          x: e.clientX,
          y: e.clientY
        });
      };

      // every time mouse moves, callback
      document.addEventListener('mousemove', mousemoveHandler);

      // clean up after
      return () => {
        document.addEventListener('mousemove', mousemoveHandler);
      }
    }, []) // run one time on initial render
    */

    return (
      <h2>X: {mousePosition.x}, Y: {mousePosition.y}</h2>
    )
  }

  // useMousePosition.js
  import { useState, useEffect } from 'react';
  const useMousePosition () => {
    const [mousePosition, setMousePosition] = useState({ x: 0, y: 0});

    useEffect(() => {
      // give function a name to refer to it later
      const mousemoveHandler = (e) => {
        setMousePosition({
          x: e.clientX,
          y: e.clientY
        });
      };

      // every time mouse moves, callback
      document.addEventListener('mousemove', mousemoveHandler);

      // clean up after
      return () => {
        document.addEventListener('mousemove', mousemoveHandler);
      }
    }, []) // run one time on initial render
  }
  export default useMousePosition;
  ```

  ```js
  //Login.jsx
  import { useState } from 'react';
  import useInput from '';
  
  function Login () {
    const username = useInput('hello');
    const password = useInput('');

    const submitHandler = (e) => {
      e.preventDefault();
      alert(`thanks for submitting: ${username.value} and ${password.value}`);
      username.clear();
      password.clear();
    };
    // const [username, setUserName] = useState('');
    // const [password, setPassword] = useState('');

    // const submitHandler = (e) => {
    //  e.preventDefault();
    //  alert(`thanks for submitting: ${username} and ${password}`);
    // };

    return (
      <div>
        <h2>Login Form</h2>
        <form onSubmit={submitHandler}>
          <label>Username</label>
          <input
            value={username.value}>
            onChange={username.onChange}
            // {...username} => cannot use clear with spread
          />
          <label>Password</label>
          <input
            value={password.value}>
            onChange={password.onChange}
            // {...password}
          />
          <button type="submit">Login</button>
        </form>
      </div>
    )
  }

  // useInput.js
  import {useState} from 'react';

  const useInput = (initialValue) => {
    const [value, setValue] = useState(initialValue);
  }

  const clear = () => {
    setValue('');
  }

  const onChange = (e) => {
    setValue(e.target.value);
  }

  return {
    value,
    onChange,
    clear
  }

  export default useInput;
  ```

  ```js
  // Location.jsx
  import useLocationData from '';

  const Location = () => {
    const {lat, long} = useLocationData();

    return (
      <h2>Lat: {lat}, Long: {long}</h2>
    )
  }

  // useLocationData.js
  import {useEffect, useState} from 'react';

  const useLocationData = () => {
    const [coords, setCoords] = useState({ lat: 0, long: 0});
    useEffect(() => {
      navigator.geolocation.getCurrentPosition((data) => {
        setCoords({
          lat: data.coords.latitude,
          long: data.coords.longitude
        });
      })
    }, []);

    return coords;
  };
  ```

windows.document
windows.naviigator

### AXIOS REQUEST

```js
const Request = () => {
  const url = 'http://';
  const {data, loading, errorMsg} = useRequest(url);

  return (
    { data && <p>Data: {data.length}</p> }
    { loading && <p>Loading...</p> }
    { errorMsg && <p>Darn! Something went wrong!! </p> }
  )
}

export default Request;
```

<a id="day5comp"></a>
## **DAY 5 COMPASS NOTES**

### REACT HOOKS TESTING LIBRARY

  - Hooks can only be used within React components
  - This npm package allows to test Hooks without needing to use them within a component for the test
  - https://github.com/testing-library/react-hooks-testing-library

<a id="dayWEcomp"></a>
## **DAY WE COMPASS NOTES**

### AUTOMATED TESTING

  - Testing is a repetitive work
    - Perfect candidate for automation
  - Earlier stage in a project:
    - Easier to manage with manual testing (i.e. console/browser)
  - As the project grows in complexity:
    - Automated testing
    - *Regression testing*
      - Process of verifying that previously uncovered bugs have not returned in *all* subsequent versions of the software
  
  - Why write tests?
    - Enhanced workflows
    - *Confidence*
  
  - **Not too many**
  - **Mostly integration**

  - **Types of Tests**
    1. *Static Code Analysis*
        - i.e ESLint, TypeScript, Flow
        - Cannot test business logic

    2. *Unit Tests*
        - Testing a specific function or component in *isolation*
          - Automatically check for expected behaviour
        - i.e. Storybook, Jest

    3. *Integration Tests*
        - Comebine differnt units of code to create an application
        - Process of proving that two or more units of *code work together*
        - Includes setting up and running the server
        - Best balance of cost, time spent, scale of problems

    4. *End-to-end Tests*
        - Test as close to simulated user behaviour as possible

    - From top to bottom:
      - Increase in cost
      - Increase in the amount of time needed to perform
      - Increase in scale of problems
      - Increase in confidence

### TEST DRIVEN DEVELOPMENT (TDD)

  - **Rules**
    1. Write new code only if an automated test has failed
    2. Eliminate duplication

  - **Process**
    1. Red - Write a small test that does not pass
    2. Green - Do the minimal amount of work to make the test pass
    3. Refactor - Improve the code, continuing to ensure all tests still pass

### BUILDING A TESTING- AND QUALITY-DRIVEN CULTURE

#### BATTLE-TESTED STRATEGY

  - Code changes must be sent as pull requests
  - A build pipeline runs tests automatically
  - The new code must meet testing requirements
  - The new code must meet quality guidelines
  - Change must be peer reviewed and approved

#### TESTING REQUIREMTNS

  - The app builds successfully
  - All tests pass
  - Coverage thresholds must be met for new code
  - Coverage thresholds for the whole repo (maybe)

#### QUALITY GUIDELINES

  - Limit cyclomatic and cognitive complexity
    - i.e. no too many nested loops, no too long function
  - Avoid known problematic patterns
    - i.e. === instead of ==
   - Eliminate duplicate does