# React Performance ⚡

[epic-react/react-performance](https://github.com/kentcdodds/react-performance)

## Why Performance

-   better UX

## Lazy loading

```tsx
import React from "react";
const Dashboard = React.lazy(
    () => import(/* webpackChunkName: "Dashboard" */ "../Pages/Dashboard")
);
```

!!! note

    The [Webpack magic comment](https://webpack.js.org/api/module-methods/#magic-comments) `webpackChunkName` determines the downloaded chunk name.

## Memoization

Storing processed functions based on received props, avoiding the memory effort to the same component.

-   React Memo

```jsx
import React from "react";
const Comp = () => (
    <div className="mt-3">
        <h1>Title</h1>
    </div>
);
export default React.memo(Comp);
```
