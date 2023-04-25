# Redux

-   Redux is usually used with React
-   can be used with other frameworks

### What Redux limits you to do

-   application state as plain objects and arrays
-   changes in the system as plain objects.
-   the logic for handling changes as pure functions.


### Extra features Redux has

-   Redux Dev Tools
-   time travel debugging

## [Immutability Helper](https://github.com/kolodny/immutability-helper)

## Redux Hooks

### `useSelector`

```jsx
import { useSelector } from "react-redux";
const user = useSelector((state) => state.user);
```

### `useDispatch`

```jsx
import { useDispatch } from 'react-redux';
const dispatch = useDispatch();

dispatch({
    type: "ACTION_TYPE",
    ...
});
```

### Before Redux Hooks: `connect`

Higher Order Component that injects more props to the component

```javascript
const mapStateToProps = (state) => ({
    prop_injected_into_component: state.path.in.redux,
});

const mapDispatchToProps = (dispatch) => ({
    // also injected as a prop into the component
    addToast: () => dispatch({ type: "ADD_TOAST" }),
});

export default connect(mapStateToProps, mapDispatchToProps)(MyComponent);
```

## [Redux Style Guide](https://redux.js.org/style-guide/#priority-a-rules-essential)

-   only have JSON serializable data in Redux
    -   no sets in Redux
    -   it won't show up in the Redux Dev Tools
-   reducers shouldn't have side effects
    -   no API calls in reducers

## [`redux-thunk`](https://github.com/reduxjs/redux-thunk)

### What is a thunk

[What the heck is a 'thunk'?](https://daveceddia.com/what-is-a-thunk/)

wrap a function around an expression to delay when it gets called

```javascript
const x = 1 + 3;
const myThunk = () => 1 + 3;
```

lets your actions be functions
- lets you do stuff
- can't do it in reducer
	- reducers have to be pure

```ts
// MyComp.jsx
import { useSelector, useDispatch } from 'react-redux';

function MyComp() {
	const dispatch = useDispatch();
	useEffect(() => {
		dispatch(getPokemon({id: 1}))
	}, []);
}
```

```js
// actions.js
export const function getPokemon(options) {
	return dispatch => {
		return axios.get(`/pokemon/${options.id}`).then(data => {
			dispatch({
				type: 'SET_POKEMON',
				id: data.id,
				name: data.name
			})
		})
	}
}
```

```js
// reducers.js
export function reducers (state, action) {
	switch(action.type) {
		case 'SET_POKEMON': {
			return {
				...state,
				[action.id]: action.name,
			}
		}
	}
}
```


### redux-thunk code

runs the function if the action is a function

```js
function createThunkMiddleware(extraArgument) {
  return ({ dispatch, getState }) => next => action => {
	// called for every action you dispatch.
	// If it's a function, call it.
    if (typeof action === 'function') {
      return action(dispatch, getState, extraArgument);
    }

	// Otherwise, just continue processing this action as usual
    return next(action);
  };
}

```


## Provider

```jsx
import { Provider } from "react-redux";

<Provider store={store}>
    <App />
</Provider>;
```

similar to React Context Provider

```jsx
const ThemeContext = React.createContext("light");
<ThemeContext.Provider value="dark">
    <Toolbar />
</ThemeContext.Provider>;
```
