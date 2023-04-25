# [Error Boundaries](https://reactjs.org/docs/error-boundaries.html)

Render a fallback when there's an error

-   can take in a `FallbackComponent` arg
-   Problem with using the `key` prop for the error boundary
    -   it'll mount and unmount every time the `key` is updated
    -   flashing
-   we can pass `resetErrorBoundary` prop that gets triggered in the `FallbackComponent`
-   `resetKeys` prop works as well

