# React Testing: Act and Assert

## 2. Act

### `act`

Extends the testing util from `React`

### When to use `act`?

### Firing events

#### `userEvent` vs `fireEvent`

userEvent

-   simulates a user
-   clicking a button will focus the button
-   everything is async/await

```js
await user.click(screen.getByRole("button", { name: /click me!/i }));
```

`fireEvent`

-   triggers the DOM event
-   clicking a button won't focus

## 3. Assert in Test

```js
expect(button).toHaveStyle(`
  background-color: white;
  color: black
`);
```
