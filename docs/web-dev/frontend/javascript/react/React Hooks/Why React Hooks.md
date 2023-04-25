
<iframe width="500" height="360" src="https://www.youtube.com/embed/eX_L39UvZes" title="Why React Hooks?" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

>[!Most important reason for react hooks?]


>[! What are custom hooks?]-
>Functions that happen to use other hooks
>
>Can return anything, do anything

**Before: HOCs**

```jsx
withRepos(Component);
```

**After: custom hooks**

```jsx
useRepos();
```

>[!What can custom hooks do that HOCs can't?]
>????

>[!Why couldn't React Query be a HOC?]
>????

0. Always use functional components
	No need to switch to class component to get state

### 1 .Classes: duplicate code in lifecycle methods

custom hooks too!

```jsx
componentDidMount() {
    this.updateRepos(this.props.id)
}

componentDidUpdate (prevProps) {
    if (prevProps.id !== this.props.id) {
        this.updateRepos(this.props.id)
    }
}
```

becomes

```jsx
useEffect(() => {
    this.updateRepos(id);
}, [id]);
```

### Historical Context

-   `React.createClass`
-   `ES6 class`
-   now: just functions!
	- what the original mental model was

#### 2. Sharing non-visual logic

-   Higher Order Components (HOC)
    -   `withRouter`
    -   injects extra props that's shared between components
-   Render prop
    -   `<Route path="/home" render={() => <p>Home</p>} />`
