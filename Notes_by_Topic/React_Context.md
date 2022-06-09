# REACT - CONTEXT

- Context is designed to share data that can be considered "global" for React components
  - When some data needs to be accessible by many components at different nesting levels
  - Ex. current authenticated user, theme, preferred language, etc.

- To avoid manually passing down props across multiple components

```jsx
// user and avatarSize props passed through multiple components
<Page user={user} avatarSize={avatarSize} />
// ... which renders ...
<PageLayout user={user} avatarSize={avatarSize} />
// ... which renders ...
<NavigationBar user={user} avatarSize={avatarSize} />
// ... which renders ...
<Link href={user.permalink}>
  <Avatar user={user} size={avatarSize} />
</Link>
```

## Basic Understanding of Context

- Create Context component and wrap it around the App component
  - App is the root component to all other children components down the component tree
  - Context component has access to the global state and manages it
    - Allows each of the children components to have access to the global state
      - Without having to prop drill   

## Using Context

- Create a *Context* using `createContext(defaultValue)`
  - Creates a Context object
  - When a component is rendered, which subscribes to this Context object
    - Reads the current context value from the closet matching `Provider` above it in the tree
  - `defaultValue` only used when a component does not have a matching Provider

- Use a *Provider* to pass the context
  - Every Context object comes with a Provider React component
    - Allows consuming components to subscribe to context changes
  - Provider component accepts a *value* prop to be passed to consuming components
    - Descendants of this Provider
  - All consumers that are descendants of a Provider will re-render whenever the Provider's value prop changes

```jsx
const MyContext = React.createContext(defaultValue);

<MyContext.Provider value={/* some value */}>
```