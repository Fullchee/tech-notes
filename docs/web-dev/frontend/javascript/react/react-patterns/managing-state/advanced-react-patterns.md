# Epic React 3: Advanced React Patterns

They're all ways of handling the complexity of managing state

## Problem: React Context + useReducer: how to pass helper dispatchers?

-   Example: getting the shopping cart

How do you pass helpers like

-   Add to cart

### Context Module Pattern

don't pass helpers in the context

Kent: doesn't see any good use cases for this pattern

```jsx
// const [state, dispatch] = React.useReducer(...)
const value = {state, increment, decrement}
<CounterContext.Provider value={value} />
```

Return the helper reducers as a standalone export function

-   which the client would've defined anyway
-   Benefits: tree shaking
-   Lazy loading
-   if you have common dispatches you want to share
    -   just export it from the `counter.js` alongside the `CountProvider` and `useCount`

-

```javascript
import { CountProvider, useCount, increment, decrement } from "./user"
```

### Why can't we just put the function in the `useCount` accessor?

-   we'd have to add `useCallback` to each function because we'd be putting it in the Provider's `value`
-   won't be able to tree shake (only get the functions we use)
    -   every function would have a `useCallback` because they'd need to be in the dependency array
-   can't lazy load

TODO: HOW DOES THIS COMPARE TO JOTAI AND ZUCSTAND?

## Problem: the same props in so many places

How to reduce code duplication?

Example: a11y helper props

We want to let the caller override our default values

### Solution: Prop Collections & Getters

```js
function useToggle() {
    const [on, setOn] = React.useState(false);
    const toggle = () => setOn(!on);

    function getTogglerProps({ onClick, ...props } = {}) {
        return {
            "aria-pressed": on,
            onClick: callAll(onClick, toggle),
            ...props,
        };
    }

    return {
        on,
        toggle,
        getTogglerProps,
    };
}
```

**Usage**

```js
<Switch {...getTogglerProps({on})} />
<button
  {...getTogglerProps({
    'aria-label': 'custom-button',
    onClick: () => console.info('onButtonClick'),
    id: 'custom-button-id',
  })}
>
```

## Problem: Our complex state has too many edge cases

We want to let the callers implement their edge cases

### State Reducer

put the state in a useReducer

-   let the user of the hook pass in their own reducer
    -   inversion of control!
-   to avoid duplication, we can do this to just update one case

```js
function toggleStateReducer(state, action) {
    if (action.type === "toggle" && clickedTooMuch) {
        return { on: state.on };
    }
    return toggleReducer(state, action); // default hook reducer
}
```

### Why is it called State reducer?

-   you pass in a reducer that modifies the state

### What does the `={}` do?

```js
// useToggle() will work
function useToggle({initialOn = false} = {}) {...}
```

vs

```js
// useToggle() will result in an error
function useToggle({initialOn = false}) {
```

## Control Props

-   allows users to completely control state values within your component
-   differs from the state reducer pattern
    -   change the state changes based on actions dispatched
    -   also can trigger state changes from outside the component or hook as well
-   replicating what React does to forms (controlled vs uncontrolled)
    -   is there a value that tha sh
-   error when going from uncontrolled to controlled (or vice versa)
    -   example: giving React a value and then later assigning it

Use case

-   Building your own input components

```js
const on = isControlled ? controlledOn : state.on;

function dispatchWithOnChange(action) {
    if (!isControlled) {
        dispatch(action); // update the redux's state
    }
    const newState = reducer({ ...state, on }, action);
    onChange?.(newState, action);
}
```

### When to warn?

1. Passing `on` without `onChange`
2. Passing a value for `on` and later passing `undefined` or `null`
3. Passing `undefined` or `null` for `on` and later passing a value

console.logs always need to be in a `useEffect`

side effect to check if va

## Latest Ref pattern

Keep track of the latest values of props or state

-   When the props

Use case

-   React query ????
-

Benefit

-   Don't need to add the callback in the rep array
    -   Because you're already updating it in another
-   ???? How are these 2 examples equivalent?
    -   When the callback changes, eg1 will run the callback again
    -   Eg2 won't

```tsx
function useExampleOne(callback) {
    React.useEffect(() => {
        callback();
    }, [callback]); // <-- have to include the callback in the dep array
}

function useExampleTwo(callback) {
    const latestCallbackRef = React.useRef(callback);
    React.useEffect(() => {
        latestCallbackRef.current = callback;
    });

    React.useEffect(() => {
        latestCallbackRef.current();
    }, []); // <-- don't have to include the callback in the dep array
}
```
