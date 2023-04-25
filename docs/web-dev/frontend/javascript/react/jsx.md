# [JSX in Depth](https://reactjs.org/docs/jsx-in-depth.html)

1. `React.createElement` is like `document.createElement()`
    1. `<MyComp>` is sugar for ☝️
2. `document.append(element)` is like `ReactDOM.render(reactComponent, document.body)`
    1. `ReactDOM` because `React` can be rendered in many environments (like `React Native`)

## React 18: `createRoot`

no more ReactDOM.render

```diff
- import { render } from 'react-dom'
+ import { createRoot } from 'react-dom/client'
const container = document.getElementById('app');
- render(<App tab="home" />, container);
+ const root = createRoot(container);
+ // createRoot(container!) if you use TypeScript
+ root.render(<App tab="home" />);
```

## Portals

[JC: Portals](https://courses.joshwcomeau.com/css-for-js/02-rendering-logic-2/10-portals)

Child component needs to be rendered outside of the parent component

-   Modals
-   Tooltips
-   Loaders

To ensure the z-index is above everything else

```jsx
const modalRoot = document.getElementById("modal-root");
const Modal = ({ children }) => ReactDOM.createPortal(children, modalRoot);
```

Parent div onClick will still work!

```jsx
const Parent = () => (
    <div onClick={onClick}>
        <Modal>
            <Child />
        </Modal>
    </div>
);
```

onClick still bubbles up as if the modal were a child of the parent

## What JSX is converted into

```jsx
<MyButton color="blue" shadowSize={2}>
    Click Me
</MyButton>
```

syntactic sugar for

```javascript
React.createElement(
    MyButton, // component name
    { color: "blue", shadowSize: 2 }, // props
    "Click Me" // children
);
```

## Dot notation

It can be an object of Components

```jsx
const MyComponents = {
    DatePicker: function DatePicker(props) {
        return <div>Imagine a {props.color} datepicker here.</div>;
    },
};

function BlueDatePicker() {
    return <MyComponents.DatePicker color="blue" />;
}
```

or a class Component???
