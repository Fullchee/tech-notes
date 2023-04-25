[Getting Started · Jest](https://jestjs.io/docs/getting-started)

## Expecting/Asserting

### Expecting objects

['.toMatchObject' vs 'objectContaining'](https://stackoverflow.com/questions/45692456/whats-the-difference-between-tomatchobject-and-objectcontaining)

`objectContaining`: nested properties need to be exact

```js
// FAIL
expect({ position: { x: 0, y: 0 } }).toEqual(expect.objectContaining({
  position: {
    x: expect.any(Number)
  }
}));
```

```js
// PASS
expect({ position: { x: 0, y: 0 } }).toMatchObject({
  position: {
    x: expect.any(Number)
  }
});
```

```js
expect(MyComponent).toHaveBeenCalledWith(
  expect.objectContaining({
	name: 'my name',
  }),
);
```


### Expect an error

Wrap it in an anon function

```javascript
test(‘’, () => {
  expect(() => {
    calculateSquare());
  }).toThrow(‘You must provide a number’);
})
```


## Mocking

like Python patching except with the intuitive API where you mock the imports just in the tests

[Mock Functions · Jest](https://jestjs.io/docs/mock-functions)

### [Mocking modules](https://jestjs.io/docs/mock-functions#mocking-modules)


- has to be at the top of the file
- can't be in a test

```js
import { sum } from './sum';

jest.mock('sum', () => 42));
```


### Expecting mocks

`expect(Component).toHaveBeenCalledWith()`


### Cleaning up mocks

```js
  afterEach(() => jest.clearAllMocks());
```


## Test configuration

`<rootDir>/jest.config.json`

```json
{
  "preset": "ts-jest",
  "transform": {
    "^.+\\.(ts|tsx|js|jsx)$": "ts-jest",
    // because Jest doesn't know what to do with 
    "^.+\\.svg$": "<rootDir>/tests/__mocks__/svgTransform.js"
  },
  "setupFiles": ["<rootDir>/tests/setupTests.js"],
  "setupFilesAfterEnv": ["<rootDir>/tests/setupJestAfterEnv.js"],
  "moduleNameMapper": {
    "^.+\\.(css|scss)$": "identity-obj-proxy",
    "^@src(.*)$": "<rootDir>/src$1",
    "^@tests(.*)$": "<rootDir>/tests$1",
    "^@stories(.*)$": "<rootDir>/stories$1",
    "^.+\\.(svg)$": "<rootDir>/tests/__mocks__/fileMock.js"
  },
  "transformIgnorePatterns": ["node_modules/(?!react-data-grid/lib)"],
  "modulePathIgnorePatterns": ["<rootDir>/dist/"],
  "globals": {
    "REACT_APP_API_ROOT": "http://localhost:8000"
  },
  "bail": true
}

```