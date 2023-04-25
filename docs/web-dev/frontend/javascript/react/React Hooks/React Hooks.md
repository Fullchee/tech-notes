[[Why React Hooks]]

-   [useState](#usestate)
-   [useEffect](#useeffect)
-   [useReducer](#usereducer)
-   [useCallback and useMemo](#usecallback-and-usememo)
-   [`useContext`](#usecontext)
-   [`useEffect` vs `useLayoutEffect`](#useeffect-vs-uselayouteffect)
-   [`useImperativeHandle`](#useimperativehandle)
-   [`React.forwardRef`](#reactforwardref)


## 2 Rules of Hooks

1. Hooks must be used in a React component
2. Hooks must be declared at the top of the function
	1. must be called in the same order every time
	2. can't be in an `if` statement
	3. see implementation of useState

## useState

-   accepts a function which is a lazy initializer!
    -   `useState` ignores the param afterward
    -   for computationally expensive stuff (async, like getFromLocalStorage)
    -   so that the expensive function only runs once
-

```jsx
const [item, setItem] = useState(() => getFromLocalStorage());
```

### Problem with this

```jsx
const [count, setCount] = useState(0);
setCount(count + 1);
setCount(count + 1);
```

#### Solution

```diff
const [count, setCount] = useState(0)
- setCount(count + 1)
+ setCount(currentCount => currentCount + 1)
```

### [Implementing `useState`](Implementing%20React.md#useState)

## useEffect

-   dependency array does a `===` comparison
    -   will always re-render if you pass it an array/object

### [Implementing `useEffect`](Implementing%20React.md#useEffect)

## `useReducer`
ate range greaterdhttps://beta.reactjs.org/reference/react/useReducer


```tsx
function reducer(state, action) {
  if (action.type === 'increment') {
    return {
      age: state.age + 1
    };
  }
  throw Error('Unknown action.');
}
```

```jsx
const [state, dispatch] = useReducer(reducer, initialValue);

dispatch({type: "increment"})
```

-   first prop: the old state
-   second prop: whatever you pass to `dispatch`
    -   usually `action`
-   doesn't have to follow the Redux style of having actions with a `type` prop

### Implementing `useState` with `useReducer`

```jsx
const [count, setCount] = useState(0);
```

```jsx
function countReducer(state, newState) {
    return newState;
}

const [count, setCount] = useReducer(countReducer, 0);
setCount(1);
```

### useReducer vs useState

-   useReducer might be good for more complex logic

## `useRef`

Why can't we have a direct pointer to a ref?

Why is the API like

```jsx
const ref = useRef();
node = ref.current;
```

The pointer will change

We have an object so that when the ref changes, it just changes the object pointer

Uses of `useRef`

1. pointing to DOM elements
    1. the pointers to the DOM elements are re-rendered all the time
2. Store state where we don't need to rerender when it changes

### `useRef` to access the previous props/state

[Stack Overflow](https://stackoverflow.com/a/57706747/8479344)

```tsx
const usePrevious = <ValueType,>(value: ValueType): ValueType | undefined => {
    const ref = useRef<ValueType>();
    useEffect(() => {
        ref.current = value;
    });
    return ref.current;
};
export default usePrevious;
```

Usage

```jsx
const [count, setCount] = useState(0);
const prevCount = usePrevious(count);
```

## useCallback and useMemo

Use cases (https://kentcdodds.com/blog/usememo-and-usecallback)

1. not have a function re-render every time so that it can be used in a useEffect dep array
2. avoiding unnecessary re-renders when re-rendering is super expensive (Graphs, Charts, Animations)
3. `useMemo` can be passed a function (just like `useState`) and lazily calculate computationally expensive items

```jsx
import { useCallback } from 'react';

const MyParent = ({ seardchTerm }) => {
  const onItemClick = useCallback(event => {
    ...
  }, [term]);
  return (
    <MyBigList
      searchTerm={searchTerm}
      onItemClick={onItemClick}
    />
  );
}
```

-   Without `useCallback`, the `onItemClick` would be redefined whenever a `useState` or a parent's state changes
    -   which means `<MyBigList />` would be re-rendered every time `useState` or a parent's state is called

### `useAsync` custom hook using `useCallback`

[advanced-react-hooks/02.md at main · advanced-react-hooks](https://github.com/kentcdodds/advanced-react-hooks/blob/main/src/exercise/02.md)

???

#### what's the `run` function that we return in `useAsync`?

- instead of the user putting their `fetch` in a `useCallback`
-   the `useEffect` in `useAsync` becomes `run` which is memoized with `useCallback`
-   they can put it in a `useEffect` and `run(result)`

### `safeDispatch` (safe fetch) and `useEffect` cleanup

-   Memory leak when unmounting before the `fetch` finishes
-   it's not a class component so we can't just have a `componentWillMount` and abort the `fetch`
-   I have to cancel subscriptions and async tasks in the useEffect cleanup function

#### How do you know if a component has been unmounted?

```jsx
React.useLayoutEffect(() => {
    mountedRef.current = true;
    return () => {
        mountedRef.current = false;
    };
}, []);
```

-   https://github.com/helderburato/use-is-mounted-ref/blob/main/src/use-is-mounted-ref.ts

## [`useContext`](react-context.md)

## `useEffect` vs `useLayoutEffect`

-   same API
-   useEffect is run after pixels are painted
-   useLayoutEffect is run before so it will delay painting
    -   can update the DOM before it paints

## `useImperativeHandle`

-   ????

### `React.forwardRef`

-   can pass a `ref` as a second param
    -   instead of the first param with all the other regular props

**Could you put `ref` as a prop? in the first param of the component?**

-   yeah but that would cause a re-render
-   you might not want to always re-render when the ref that's passed down to the component changes

### Do you need to always use `useImperativeHandle` when using `React.forwardRef`?

### `useDebugValue`

-   feels like `__repr__` in Python for custom hooks
