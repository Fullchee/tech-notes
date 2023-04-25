## Only getting the second value in an array

```javascript
[count, setCount];
[, setCount];
```

## Conditional values in an array

```javascript
const arr = [flag && value].filter(Boolean);
```

## 2 arrays: check identical? (same order)

```javascript
Arr1.length === arr2.length && arr1.every((item, i) => arr2[i] === item);
```

## [Sorting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

mutates the existing array

-   Alphabetically
    -   `arr.sort()`
-   numerically ascending
    -   `arr.sort((a, b) => a - b)`