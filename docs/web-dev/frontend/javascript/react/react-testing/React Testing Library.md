## Links

-   [Testing React Apps | Epic React](https://epicreact.dev/modules/testing-react-apps)
-   [Common mistakes with React Testing Library](https://kentcdodds.com/blog/common-mistakes-with-react-testing-library)

-   [eslint-plugin-testing-library](https://github.com/testing-library/eslint-plugin-testing-library)
-   [eslint-plugin-jest-dom](https://github.com/testing-library/eslint-plugin-jest-dom)


## Philosophy

- test the way your user would
-   don't test internals

### What RTL does
- what happens in a test
	- render a component
	- then tear it down
	- do something once it's rendered
- RTL removes boilerplate
	- has nice practices
	- isolation of tests

### Mocking non JS files

Jest doesn't understand

-   `setupFilesAfterEnv`
-   `['@testing-library/jest-dom/extend-expect', path.join(__dirname, 'src/test/setup')]`
-   create React app: `setupTests.js`

`moduleDirectories: [path.join(__dirname, 'src')]`

-   unless you use Webpack aliases

## Swap `@testing-library/react` with your own test utils

### `render`

[`render` result](https://testing-library.com/docs/react-testing-library/api/#render-result)

-   queries

you don't need to use the result of `render`

### [Wrapper](https://epicreact.dev/modules/testing-react-apps/context-and-custom-render-method-extra-credit-solution-2)

```js title="test-utils.js"
function render({ theme = "light", ...options } = {}) {
    const Wrapper = ({ children }) => (
        <ThemeProvider initialTheme="light">{children}</ThemeProvider>
    );
    return render(ui, { wrapper: Wrapper, ...options });
}

export * from "@testing-library/react";
export { render }; // use our own render
```

## Getting DOM elements

### `screen`

use `screen` instead of using queries from `render`

-   more resilient to changes

[Which query to use](https://testing-library.com/docs/queries/about/#priority)

-   `getByRole` all the time if possible

[Testing Playground](https://testing-playground.com/)

`screen.debug`

```js
screen.getByRole("button", { name: /submit/i });
```

Only use `query*` to check for non-existence

```js
expect(screen.queryByRole("alert")).not.toBeInTheDocument();
```

`find*` uses `waitFor` under the hood

-   use it for something that might not be available right away

```jsx
const submitButton = await screen.findByRole("button", { name: /submit/i });
```

## Mocking

`const handleSubmit = jest.fn()`

`expect(handleSubmit).toHaveBeenCalledTimes(1)`

### Generate test data

#### `faker`

```js
import faker from 'faker'
const buildLoginForm = (overrides) => {
	username: faker.internet.userName(),
	password: faker.internet.password(),
	...overrides,
}

const {username, password} = buildLoginForm()
```

#### `test-data-bot`

```js
import {build, fake} from @jackfranklin/test-data-bot

const buildLoginForm = build({
	fields: {
	username: fake(f => f.internet.userName()),
	password: fake(f => f.internet.password()),
})

const {username, password} = buildLoginForm()
```

`test-data-bot` can create sequences

### [Mocking Browser APIs](https://epicreact.dev/modules/testing-react-apps/mocking-browser-apis-and-modules-intro)


## Snapshot tesing

with [asFragment()](https://testing-library.com/docs/react-testing-library/api/#asfragment)

```typescript
const { asFragment } = render(<MyComp />)
const firstRender = asFragment()
expect(firstRender).toMatchSnapshot()


// snapshot the difference between the first and second render
userEvent.click(screen.getByText(/text/))
expect(firstRender).toMatchDiffSnapshot(asFragment())
```