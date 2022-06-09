# REACT

  - JS library for building *user interfaces*
    - Easily create interactive UIs
    - Manage the *state* (the current status of each view) in application
      - update and render the browser to reflect the current state

  - **Encapsulation**
    - A *group of elements* can be stored inside a *component*
      - A component can be called by another component
  
  - **JavaScript XML (JSX)**
    - Syntax extension to JS
    - The language of choice for React developers
    - Allows to *create React elements*
      - Can be *renedered into DOM*
    - Combined markup (i.e. HTML) and logic in *components*
    - Variables can be called using *curly braces {}*
      - JS expression can be used inside {} as well   

    - **`React.createElement (Component Creation)`**
      - Define the type of element and any properties to pass to it
      - JSX uses *className* instead of class to define CSS classes
      - Variables can be passed in using `{variable_name}` in place of hardcode
        ```js
        // JSX
        const element = <h2 className="name">Name</h2>

        //JS
        const element = React.createElement("h2", {
          className: "name"
        }, "Name")
        ```
      - *Component is created* and *comoponent name* must start with a *capital letter*
        ```js
        function Tweet() {
          return (
            <article className="tweet">
              <header className="tweet__header">
                <img className="tweet__header-avatar" src={ props.avatar } />
                <h2 className="tweet__header-name">{ props.name }</h2>
              </header>
              <main className="tweet__content">
                <p>{ props.content }</p>
              </main>
              <footer className="tweet__footer">{ props.date }</footer>
            </article>
          )
          }

        // component created
        const tweet = <Tweet />
        ```

    - **`ReactDOM.render`**
      - An element can be *rendered into any DOM node* using *react-dom* library
      - `ReactDOM.render(element, container)` to render
        ```js
        ReactDOM.render(
          <Tweet
            name="React"
            avatar="https://api.adorable.io/avatars/64/react@adorable.png"
            content="A JavaScript library for building user interfaces"
            date="May 29th, 2013"
          />,
          document.getElementById("root")
        )
        ```
  
## REACT RULES

  1. All *tags* must be *closed*
      ```
      <div>
      <img>
      <Album />
      </div>
      ```

  2. A child tag must close before its parent

  3. All JSX expression must reult in one root level element
    - JSX expressions must have one parent element
      - JSX does not allow more than one parement element
      ```js
      // Good - one parement element (div)
      return (
        <div>
          <input />
        </div>
      )
      
      // Bad - two parement elements (div and input)
      return (
      <div>
      </div>
      <input />
      )
      ```

  4. No HTML comments
      ```js
      return (
      <div>
        <!--- Not allowed --->
        {/* Allowed */}
      </div>
      )
      ```

## REACT - `create-react-app`

  - Package tool that enables to create a fully independent React app in one command
    - React can be installed and built manually, but this makes it much easier 
    - Includes the following scripts:
      - *npm start*
        - starts the development server
        - shows what the app looks like
      - *npm run build*
        - to deploy the app
        - creates a static version of the app once finished with the development
      - *npm test*
        - for testing
      - *npm run eject*
        - to remove create-react-app and replacing with all the dependencies to make the app work
        - once ejected, *cannot reverse*
    - Includes the following folders:
      - *node_modules*
      - *public*
        - contains files that will be accessible to the broser when the development server is running
        - contains *index.html* file
      - *src*
        - contains all of the code for the app
        - App.js => *component file*
        - index.js => file to *render component*
          
## REACT - Importing & Showing Components**

  - Components can be imported using `import ... from ...` syntax
    ```js
    import Navigation from './components/Navigation'
    import Profile from './components/Profile'
    import TweetList from './components/TweetList'
    import TweetForm om './components/TweetForm'
    ```
  - To show components in JSX, wrap the component name in `<>`
    - `<Component />` or `<Component></Component>`
  - *Tags must be closed* since JSX is more strict than HTML
    - Ex. <br> => <br />

## REACT - Event Handling

  - Event handlers can be attached to React elements
    - Pass a reference to a function directly
      ```
      function Button() {
        return (
          <button onClick={() => console.log("Button Clicked")}>
            Click me!
          </button>
        );
      }
      
      // passing a function as a variable
      // pass the function reference directly without invoking it
      function Button() {
        const doStuff = () => {
          console.log("Do stuff.");
          console.log("Do more stuff.");
          console.log("Do EVEN MORE stuff!");
        };
        return <button onClick={doStuff}>Click me!</button>;
      }
      ```

## REACT PROPS

  - Properties given to a component, similar to parameters for function in JS
  - In JSX, *properties to components* are passed the same way attributes are assigned to HTML elements
    - Can *define property names*, whereas attribute names are fixed
  - Passing props to a component:
    - *destructure or passing down more than one props*
      - name the props using *key=value* pair when passing down
    1. *key=value* pair
        ```
        <Profile firstName="Amy" lastName="Mansel" avatar="/profile-hex.png" />
        ```
    2. *{...variable}* spread operator to destructure an object
        ```
        const user = {firstName: "Amy", lastName: "Mansel", avatar: "/profile-hex.png"};
        <Profile {...user} />
        ```
  - Props passed to a component are automatically stored in an object
    - Props are passed down to children from the parents
    - Object is available as a parameter in the component definition
  - JSX accepts *ternary operator* and *short circuit evaluation*
    - If statement not allowed

      ```js
      // parenemt element
      // passing down props through component
      const MatchList = (props) => {
        const oneMatch = matchData[0]
        return (
          <section className="PlayerList MatchList">
            <h1>Match list</h1>
            <Match {...oneMatch} />
          </section>
        );
      };

      // child element
      // props passed down received and can be used as variables
      const Match = (props) => {
        const { players, winner, scoreDifference } = props;
        // console.log({winner}); => { winner: "name" } - returns key-value as object
        // console.log(winner); => "name" - returns only the value
        return (
          <article className="Match">
            <h1>
              {players[0]} <span>vs</span> {players[1]}
            </h1>

            // winner should not be wrapped in {} since the whole ternary operator is wrapped in {} already
            // variables inside React tags should be enclosed in {} 
            {winner ? <h2>{winner} is the winner by {scoreDifference}!</h2> : <h2>No winners yet!</h2>}
          </article>
        );
      };

      // ternary operator
      {{winner} ? <h2>{winner} is the winner by {scoreDifference}!</h2> : <h2>No winners yet!</h2>}

      // short circuit evaluation
      {wins === 0 && <h2 className="zero">Currently with no wins</h2>}
      {wins === 1 && <h2>Currently at {wins} win</h2>}
      {wins > 1 && <h2>Currently at {wins} wins</h2>}
      ```
    
    - Props can be an entire *function definition*
      - Pass the *function reference* to the component without invoking it
        ```
        function doStuff () {
          console.log("This is the doStuff function.");
        }
        // doStuff is passed as a reference!
        <Profile doStuff={doStuff} />
        ```

## COMPONENTS AND PROPS
  - In a *user-defined component*, *JSX attributes and children* to this component are passed as a *single object* (i.e. *props*)
    ```js
    function Welcome(props) {
      return <h1>Hello, {props.name}</h1>;
    }
    const element = <Welcome name="Sara" />;
    ReactDOM.render(
      element,
      document.getElementById('root')
    );
    ```
    1. We call ReactDOM.render() with the <Welcome name="Sara" /> element.
    2. React calls the Welcome component with {name: 'Sara'} as the props.
    3. Our Welcome component returns a `<h1>Hello, Sara</h1>` element as the result.
    4. React DOM efficiently updates the DOM to match `<h1>Hello, Sara</h1>`.

  - **Composing Components**
    - Components can refer to other components in their output
    - `App` component is typically at the top
      - Start bottom-up (i.e. children => parent)
      ```js
      function Welcome(props) {
        return <h1>Hello, {props.name}</h1>;
      }
      function App() {
        return (
          <div>
            <Welcome name="Sara" />
            <Welcome name="Cahal" />
            <Welcome name="Edite" />
          </div>
        );
      }
      ReactDOM.render(
        <App />,
        document.getElementById('root')
      );
      ```

  - **Extracting Components**
    - To split components into *smaller components*
    - Name props from the component's own point of view
    - *Rule of Thumb*
      - If a part of UI is:
        - used several times (i.e. Button, Panel, Avatar)
        - complex on its own (i.e. App)
      - Good candidate to be extracted to a separate component

## STATE AND LIFECYCLE

## HOOK - USEREDUCER

  - *reduce* describes the process of taking multiple values and processing them one by one to create a single value

  - `useReducer` hook is an *alternative to the useState* hook
    - For managing more *complex state logic*
  
  
  - `const [state, dispatch] = useReducer(reducer, 0)`
    - *alter the state* with a reducer
    - *dispatch* an action that describes the change to make
      - expect the *reducer to handle the action* and *replace the current state*

  ```jsx
  import { useReducer } from "react";

  function reducer(state, action) {
    if (action.type === "add") {
      return state + action.value;
    }

    if (action.type === "subtract") {
      return state - action.value;
    }

    if (action.type === "multiply") {
      return state * action.value;
    }

    return state;
  }

  function BoringCalculator() {
    /* Pass a reducer and an initial state */
    const [state, dispatch] = useReducer(reducer, 0);

    /* These functions dispatch actions described as obejcts */
    function add3() {
      dispatch({ type: "add", value: 3 });
    }

    function subtract5() {
      dispatch({ type: "subtract", value: 5 });
    }

    function add7() {
      dispatch({ type: "add", value: 7 });
    }

    function multiply11() {
      dispatch({ type: "multiply", value: 11 });
    }

    /* Attach the actions to the buttons and render the state */
    return (
      <div className="calculator">
        <div className="result">{state}</div>
        <button className="add" onClick={add3}>
          Add 3
        </button>
        <button className="subtract" onClick={subtract5}>
          Subtract 5
        </button>
        <button className="add" onClick={add7}>
          Add 7
        </button>
        <button className="multiply" onClick={multiply11}>
          Add 11
        </button>
      </div>
    );
  }
  ```

  - *dispatch* uses *reducer function* to handle the *action* and replace the current *state*
  - 