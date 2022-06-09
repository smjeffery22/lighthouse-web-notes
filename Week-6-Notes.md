# **Jeffery Park's LHL Week 6 Notes**

## **Table of Contents**
- [DAY 5 COMPASS NOTES](#day5comp)
- [DAY WE COMPASS NOTES](#daywecomp)


<a id="day5comp"></a>
## **DAY 5 COMPASS NOTES**

### HOST VS GUEST MACHINE

  - **Host Machine**
    - Our physical computer

  - **Guest Machine**
    - Virtual machine (VM) that is ran using software such as VirtualBox
    - Configured to have access to a shared drive that belongs to the Host
      - Vagrant to configure
        - *vagrant up* to start the VM
        - *vagrant ssh* to connect to the VM
  
  - During Week 7 and 8, run all applications in the Host environment
    - i.e. all `npm` commands
    - run `psql` in *vagrant*
  
### NODE VERSION MANAGER (NVM)

  - Allows to install and use different versions of node via the command line
  - [Installation](https://github.com/nvm-sh/nvm#installing-and-updating)
  - Example:
    ```
    $ nvm use 16
    Now using node v16.9.1 (npm v7.21.1)
    $ node -v
    v16.9.1
    $ nvm use 14
    Now using node v14.18.0 (npm v6.14.15)
    $ node -v
    v14.18.0
    $ nvm install 12
    Now using node v12.22.6 (npm v6.14.5)
    $ node -v
    v12.22.6

    // to see locaclly installed nvm versions
    $ nvm ls

    // to list the versions of Node.js available for installation
    $ nvm ls-remote
    ```

### REACT

  - JS library for building *user interfaces*
    - Easily create interactive UIs
    - Manage the *state* (the current status of each view) in application
      - update and render the browser to reflect the current state

  - **Encapsulation**
    - A *group of elements* can be stored inside a *component*
      - A component can be called by another component
  
  - **JavaScript XML (JSX)**
    - Synyax extension to JS
    - The language of choice for React developers
    - Allows to *create React elements*
      - Can be *renedered into DOM*
    - Combined markup (i.e. HTML) and logic in *components*
    - Variables can be called using *curly braces {}*
      - *JS expression* can be used inside *curly braces {}* as well
      ```js
      


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
  
### REACT RULES

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

### REACT - `create-react-app`

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
          
### REACT - Importing & Showing Components**

  - Components can be imported using `import ... from ...` syntax
    ```js
    import Navigation from './components/Navigation'
    import Profile from './components/Profile'
    import TweetList from './components/TweetList'
    import TweetForm from './components/TweetForm'
    ```
  - To show components in JSX, wrap the component name in `<>`
    - `<Component />` or `<Component></Component>`
  - *Tags must be closed* since JSX is more strict than HTML
    - Ex. <br> => <br />

### REACT - Event Handling

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
  
<a id="daywecomp"></a>
## **DAY WE COMPASS NOTES**

### DATA STRUCTURES

  - **Data Structure**
    - A broad term that covers all of the way that we can store data in our programs
  - **Data Types**
    - Holds only one value
      - undefined, Boolean, Number, String, BigInt, Symbol
  - **Structural Types**
    - Represent a structure that will hold data
      - Object, Array, Date, Map
        - Array, Date, Map are constructed from the Object structural type
        - Sub-categories of the Object type

### ARRAYS VS. OBJECTS

#### ARRAYS

  - **Pros**
    - Storing a collection of *independent items*
    - Storing information *in order*
  - **Cons**
    - To store *related data*
    - To create, read or modify elements that are not at the beginning or theend of the array

#### OBJECTS

  - **Pros**
    - Storing *related* information with labels
    - Order is not important (i.e. as long as appropriate key-value pairs are created)
    - Easy to *access and and manipulate values*
  - **Cons**
    - When order is important
    - For independent items

#### SUMMARY

  - Are they independent items? If yes, maybe use an array.
  - Are they related items? If yes, maybe use an object.
  - Will you need to access specific values often? If yes, maybe use an object.
  - Will you need to remove the first or last element often? If yes, maybe use an array.

### REACT PROPS

  - Properties given to a component, *similar to parameters/arguments for function in JS*
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
      - **PROPS GO DOWN AND FUNCTIONS RUN AT THE TOP (even if it is called down)**
        ```
        function doStuff () {
          console.log("This is the doStuff function.");
        }
        // doStuff is passed as a reference!
        <Profile doStuff={doStuff} />
        ```

    - *Keys* should be given to the *elements inside an array* to give the elements a stable identity
      - Helps identify which items have changed, are added or are removed
      - Typically suse *id from data* as key
        ```js
        const parsedMatches = matchData.map(match => <Match key={match.matchNumber} {...match} />);

        for (let i = 0; i < repetitions; i++) {
          textArray.push(<span key={i}>I like this text</span>);
        }
        ```

### RENDERING ARRAYS IN JSX

  - When an array is referenced in JSX, the *values of the array are automatically looped and rendered*
    ```js
      const someArray = [<p>a paragraph</p>, <p>another paragraph</p>, <p>yet another paragraph</p>];
      return(
        <div>
          {someArray}
        </div>
      );

      // returns this in HTML
        <div>
          <p>a paragraph</p>
          <p>another paragraph</p>
          <p>yet another paragraph</p>
        </div>
    ```