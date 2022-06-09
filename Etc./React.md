# REACT

## PURPOSE

  - Allows to make UI interactivity simple
  - Simpify Vanilla JS
    - HTML => assign id, class => document.getElementbyId => button.addEventListener => ...
    - React simplies the above process

## REACT AND REACTDOM

  - React (library) is like an engine - allows to have interactive UI
  - ReactDOM is how we insert React elements into HTML
  - ReactDOM.render() takes React element and places it in HTML
    -  Show it to the suer
  - **Start with JS => Becomes HTML**
    - *Create elements using JS and React translates it to HTML*
    - Vanilla JS starts with HTML and use it to find elements and update them


## JSX

  - Extension syntax to JS
  - Allows to create React elements using syntax very similar to HTML
  - Browser does not understand JSX and will return SyntaxError
    - Unexpected token '<'
  - *Babel translates JSX to JS*

  - Cannot use JS syntax
    - class => className
    - for => htmlFor (for `<label htmlFor="username">`)

## REACT STATE

  - React re-renders only parts that have been changed
    - Opposed to Vanilla JS which re-renders the whole page
    - Saves memory

  - *useState()* to re-render automatically after changing certain value
    - const [counter, setCounter] = React.useState(0);
      - counter: data
      - setCounter: *function to modify the data and **re-render the component** (i.e. the function that useState is in) after modification*
        - only updates the part that updated (i.e. counter)
        - change of state => re-render 

## REACT PROPS

  - A way to pass down data from a parent component to children components

  - **React Memo (memorize)**
    - To tell React to not re-render certain component if its props does not change
      - Prevent unnecessary re-rendering
    - When the state changes for the first Btn component, it renders
      - The second Btn component does not render due to React.memo since its props did not change
    - Useful when there are a lot of the same components that do not all change props at the same time
      ```js
        function Btn({ text, changeValue }) {
          console.log(text, "was rendered")
          return (
            <button
              onClick={changeValue}
              style={{
                backgroundColor: "tomato",
                color: "white",
                padding: "10px 20px",
                border: 0,
                borderRadius: 10
              }}>
              {text}
            </button>
          );
        }

        const MemorizeBtn = React.memo(Btn);

        function App() {
          const [value, setValue] = React.useState("Save Changes");
          const changeValue = () => setValue("Revert Changes");

          return (
            <div>
              <MemorizeBtn text={value} changeValue={changeValue} />
              <MemorizeBtn text="Continue" />
            </div>
          );
        };

        const root = document.getElementById("root");

        ReactDOM.render(<App />, root);
      ```

  - **Prop Types**
    - Allows to set the type of props so that error message is shown when wrong types of props are passed down
    - `npm i prop-types`
    ```js
      import PropTypes from "prop-types";

      function Btn({ text, fontSize }) {
        return (
          <button
            style={{
              backgroundColor: "tomato",
              color: "white",
              padding: "10px 20px",
              border: 0,
              borderRadius: 10,
              fontSize
            }}>
            {text}
          </button>
        );
      }

      Btn.propTypes = {
        text: PropTypes.string, // include .isRequired at the end to require text
        fontSize: PropTypes.number
      };

      function App() {
        return (
          <div>
            <Btn text="Save Changes" fontSize={18} />
            <Btn text={14} fontSize="Continue" /> // will cause an error
          </div>
        );
      };
    ```

## REACT STYLES

  - CSS file can be imported into index.js
    - Cannot separate styling for the same component
    - A lot of code
  - **CSS Module**
    - Make a css file with .module included in the filename
      - i.e. `Button.module.css`
      - .module added to activate the CSS Module behaviour
    - Import .module.css file into the component file and assign a name
      - Style code will be transformed into JS object
      - Style code will be key-value pair
    - CRA will create a *random class name*
    - Can use the same className for different components since .module.css are separated

    ```js
    // Button.module.css
    .btn {
      color: white;
      background-color: tomato;
    }

    // Button.js
    import PropTypes from "prop-types";
    import styles from "./Button.module.css";

    function Button({ text }) {
      return (
        <button className={styles.btn}>
          {text}
        </button>
      );
    }
    ```

## REACT EFFECTS

  - Sometimes, you want to run some codes only on the first render
    - i.e. no re-render after a state changes
    - ex. when calling data from API, you only want it to happen on the initial render 
  - **useEffect()**
    - Allows to choose when the code should run
    - *first argument:* a callback you want to run only once
    - *second argument (**dependencies**):* condition to only run if the value given to the argument changes
      - []: empty array means the callback inside the useEffect will only run at the initial render
      - [keyword]: callback inside the useEffect will run whenever keyword value changes

    ```js
      useEffect(() => {
        console.log("call the api");
      }, []);

      useEffect(() => {
        (keyword !== "" && keyword.length > 5) && console.log("search for", keyword);
      }, [keyword]);
    ```

## REACT ROUTER

  - React Router v6 Major Changes
    - https://www.youtube.com/watch?v=k2Zk5cbiZhg&ab_channel=TraversyMedia

  - Allows to create routes
   - `npm i react-router-dom`

  - Import from react-router-dom
    - *BrowserRouter* > *HashRouter*
      - http://localhost:3002/movie vs. http://localhost:3002/#/movie
      - preferred to not include hash in URL
    <!-- - *Switch* included to render one route at a time
      - *Router* can render multiple routes at once
      - Switch not required from react-router-dom v6 -->
    - Wrap `<Route>` with `<Routes></Routes>`
    - *Link* to include link to another route
      - Include in component

  - Place the component inside `<Route></Route>`
    - React will render the component when the URL is visited
    - Assign *route path* as attribute in Route tag
      - Path can be dynamic to include `:id`

  - `useParams` hook to grab the :id from the URL
    - Returns key-value pair as an object
      - can be destructured `const { id } = useParams()`

  ```jsx
  // App.js
  import Home from './routes/Home';
  import Detail from './routes/Detail';
  import {
    BrowserRouter as Router,
    Switch,
    Route
  } from 'react-router-dom';
  function App() {
    return (
      <Router>
        <Switch>
          <Route path='/'>
            <Home />
          </Route>
          <Route path='/movie'>
            <Detail />
          </Route>
        </Switch>
      </Router>
    );
  }

  export default App;

  // Movie.js
  import PropTypes from 'prop-types';
  import { Link } from 'react-router-dom'

  function Movie({ coverImg, title, rating, summary, genres }) {
    return (
      <div>
        <img src={coverImg} alt="movie cover" />
        <h2><Link to={`/movie/${id}`}>{title}</Link> ({rating})</h2>
        <p>{summary}</p>
        {genres &&
          <ul>
            {genres.map((genre) => {
              return (
                <li key={genre}>{genre}</li>
              )
            })}
          </ul>
        }
      </div>
    )
  }

  // Detail.js
  import { useParams } from 'react-router-dom';

  function Detail() {
    const x = useParams();
    console.log(x)
    
    return (
      <h1>Detail</h1>
    );
  }

  export default Detail;
  ```

## PUBLISHING

  - `npm i gh-pages`
    - Allows to upload the finished products to GitHub pages
    - Get a domain

  - `npm build`
    - Generates production ready code
      - Code will be compressed and optimized
    - Creates a folder called `build`

## REACT-ICONS

  - https://react-icons.github.io/react-icons/icons?name=fa
  - `npm install react-icons`
  - `import { IconName } from "react-icons/fa";`
