# [underscore.js](https://underscorejs.org/)

**Playground**

https://stackblitz.com/edit/underscore-playground

```javascript
var stooges = [
    { name: "curly", age: 25 },
    { name: "moe", age: 21 },
    { name: "larry", age: 23 },
];
```

## `_.chain`

Allows you to chain (like vanilla JS)

-   wraps your data in an object with a ton of methods
-   those methods return the wrapped object until you call `.value()`

```javascript
var sorted = _.sortBy(stooges, (stooge) => stooge.age);
var formatted = _.map(sorted, (stooge) => `${stooge.name} is ${stooge.age}`);
var first = _.first(formatted);
```

```javascript
var youngest = _.chain(stooges)
    .sortBy(function (stooge) {
        return stooge.age;
    })
    .map(function (stooge) {
        return stooge.name + " is " + stooge.age;
    })
    .first()
    .value();
```

Note that you need the `.value()` after

Problem with `_.chain`

-   it imports all of `underscore`

## [`_.groupby`](https://underscorejs.org/#groupBy)

```javascript
_.groupBy([1.3, 2.1, 2.4], (num) => Math.floor(num));
=> {1: [1.3], 2: [2.1, 2.4]}

_.groupBy(['one', 'two', 'three'], 'length');
=> {3: ["one", "two"], 5: ["three"]}
```
