# React Router v5

[[React Router v6]]

## Why React Router?

-   client side routing
    -   go to another page
    -   render a page given a URL
-   also do server side rendering (with Remix or Next.js)

## Philosophy and Intro

[uidotdev: React Router v5: Philosophy and Introduction](https://fullchee-reminders.netlify.app/link/2071)

## What is BrowserRouter?

-   Parent component
-   can pass routing props to any component
    -   uses React Context

## `<Route>`

`Route` always has to render something

```tsx
<Route path="/"
	<Dashboard />
</Route>
```

- children or render prop if there's a match
- `null` if no match

```jsx
import {BrowserRouter as Router} from 'react-router-dom'

ReactDOM.render(
    <Router>
        <App>
    </Router>
, document.getElementById('app'))
```

## `<Route>` and partial matching

`/users/new`

-   will render both `Users` and `NewUser`

```jsx
<Route path="/users">
    <Users />
</Route>
<Route path="/users/new">
    <NewUser />
</Route>
```

### Route's `render` prop

```jsx
<Route
    path="/path"
    render={({ match }) => (
      <React.Suspense fallback={<>...</>}>
        <Component id={parseInt(match.params?.id, 10)} />
      </React.Suspense>
    )}
  />,
```

### Optional param

[How to Add Optional Path Parameter with React Router v5](https://thewebdev.info/2021/09/18/how-to-add-optional-path-parameter-with-react-router-v5/)

```jsx
<Route exact path="/route1/" component={MyComp} />,
<Route exact path="/route1/:optionalParam" component={MyComp} />,
```

```jsx
<Route exact path="/route1/:optionalParam?" component={MyComp} />,
```

### [Switch](https://v5.reactrouter.com/web/api/Switch)

render the first `<Route>` that matches

```jsx
let routes = (
  <Switch>
    <Route exact path="/">
      <Home />
    </Route>
    <Route path="/about">
      <About />
    </Route>
    <Route path="/:user">
      <User />
    </Route>
    <Route>
      <NoMatch />
    </Route>
  </Switch>
);
```

### [Protected Routes](https://ui.dev/react-router-v5-protected-routes-authentication)

[Protected routes and authentication with React Router v5](https://ui.dev/react-router-v5-protected-routes-authentication)

You can create your own Routes

```tsx
function PrivateRoute({ children, ...rest }) {
  return (
    <Route
      {...rest}
      render={() => {
        return fakeAuth.isAuthenticated === true ? (
          children
        ) : (
          <Redirect to="/login" />
        );
      }}
    />
  );
}
```




## Prompt

Raise an alert when they try to leave

```jsx
<Prompt
    when={hasUnsavedChanges()}
    message="You have unsaved changes, are you sure you want to leave?"
/>
```

[Custom Modal Component](https://michaelchan-13570.medium.com/using-react-router-v4-prompt-with-custom-modal-component-ca839f5faf39)

## Hooks

### Why `withRouter` HOC?

#### Before `withRouter`

1. You passed in a component to `Route`
2. `Route` would create a HOC and pass props `history`, `match`, `location` to your component 3. so you can `history.push("new/path")`

```js
import { Route } from "react-router-dom";
<Route path="/path" component={MyComponent} />;
```

Some components (example: Header) are in every page

-   can't wrap with a `Route`

```js
import { withRouter } from "react-router-dom";

export default withRouter(Header);
```

gives `<Header />` access to the props

-   `history`
-   `match`
-   `location`

Now they have their own hooks!

## Why isn't `history.push()` changing the page?

-   https://v5.reactrouter.com/web/api/history

we don't have a router wrapped around the component?

### How to access history?

#### `useHistory`

```jsx
let history = useHistory();
history.push("/home");
```

Route's `render` prop

```jsx
<Route render={({history}) => <MyComponent history={history}} /> />
```

`withRouter`

## Preventing transitions

https://fullchee-reminders.netlify.app/link/2070

## Relative URLs

`/configurator/1/..` --> 404

-   theory: would resolve to `/configurator`
-   actual: just checks for `/configurator/1/..`
    -   it doesn't do a `path.resolve`
-   need to route to `/configurator` with `exact`

I think it should be supported tho?


## [Link](https://v5.reactrouter.com/web/api/Link)

Internal links only 😢

External links need to use `<a>`

We had a `<Link>` component that would use `<Link />` or `<a>`  if the href was external