# Debounce

See Glossary: debounce vs throttling

Always use arrow functions so that we can use the `this` context

## Example usage

```javascript title="usage.js"
let counter = 1;

const debouncedPrint = debounce(() => console.log("hi"), 1000);

debouncedPrint();
debouncedPrint();
```

## Basic debounce (no args and return value)

-   arguments and return value

```javascript title="debouncev1.js"
function debounce(fn, delay) {
    let timeoutId;

    function debouncedFn() {
        // everytime the function gets called, restart the timer
        clearTimeout(timeoutId);
        const startTimer = () => {
            timeoutId = setTimeout(() => {
                fn();
            }, delay);
        };
        startTimer();
    }

    return debouncedFn;
}
```

## Debounce with args

```diff
function debounce(fn, delay) {
    let timeoutId;

-   function debouncedFn() {
+   function debouncedFn(...args) {
        clearTimeout(timeoutId);

       const startTimer = () => {
            timeoutId = setTimeout(() => {
-               fn();
+               fn.apply(null, args);
            }, delay);
        };
        startTimer();
    }

    return debouncedFn;
}
```

## [Debounce that returns a promise](https://www.30secondsofcode.org/js/s/debounce-promise)

?????????

```diff
function debounce(fn, delay) {
    let timeoutId;
+   const pending = [];

    function debouncedFn(...args) {
+       const prom = new Promise((res, rej) => {
+           pending.push({ resolve: res, reject: rej });
+            clearTimeout(timeoutId);
            const startTimer = () => {
                timeoutId = setTimeout(() => {
+                   const currentPending = [...pending];
+                   pending.length = 0;
-                   fn.apply(null, args);
+                   Promise.resolve(fn.apply(this, args)).then(
+                       data => {
+                           currentPending.forEach(({ resolve }) => resolve(data))
+                       }
+                       error => {
+                           currentPending.forEach(({ reject }) => reject(error));
+                       }
+                   );
                }, delay);
            };
            startTimer();
+       })
    }

    return debouncedFn;
}
```

### Debounce with promise example

```javascript
const fn = (arg) =>
    new Promise((resolve) => {
        setTimeout(resolve, 1000, ["resolved", arg]);
    });
const debounced = debouncePromise(fn, 200);
debounced("foo").then(console.log);
debounced("bar").then(console.log);
// Will log ['resolved', 'bar'] both times
```
