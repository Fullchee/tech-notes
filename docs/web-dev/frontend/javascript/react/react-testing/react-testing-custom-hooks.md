# Testing Custom Hooks

[Test Custom Hook | Epic React](https://epicreact.dev/modules/testing-react-apps/testing-custom-hooks-solution)

You should really test components

-   that's how the hooks will be used

like testing decorators with a dummy function

## For complex custom hooks

like refs

when a component re-renders, it creates a new instance

-   which is why we need `ref.current` instead of just the `ref`

```js
import { renderHook, act } from "@testing-library/react-hooks";

test("", () => {
    const { result, rerender } = renderHook(userCounter);
    act(() => result.current.increment());
    expect(result.current.count).toBe(1);

    rerender({ step: 2 });
    act(() => result.current.increment());
    expect(result.current.count).toBe(3);
});
```

act

-   I'm gonna do something that triggers a state change
-   after the callback finishes, I want to flush all the side effects so that the next line of code has a stable component

`userEvent` already wraps things in `act` so we didn't need to do this before
