# Intro to Promises

## Why JS only has one thread

JS was designed to be a simple scripting language for the Netscape browser to make websites interactive.

Not the powerhouse that can do all the things like today.

Only having one thread makes programs simpler because you don't have to deal with locks and concurrency issues.

??? "We can still run code on multiple threads"

    - [WebWorkers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)
        - don't have access to the DOM
    - [WASM might have real multithreading in the future](https://github.com/dotnet/aspnetcore/issues/17730)

### How the event loop works

<iframe
  width="713"
  height="360"
  src="https://www.youtube.com/embed/8aGhZQkoFbQ"
  title="What the heck is the event loop anyway? | Philip Roberts | JSConf EU"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
  allowfullscreen
></iframe>

## Callbacks

### Why callbacks?

-   execute code after something else finishes

### Example

```js
function printContents(err, data) {
    if (err) console.error(err);
    console.log(data);
}

fs.readFile("package.json", "utf8", printContents);
```

### Problem with callbacks: Callback hell

```javascript
const fs = require("fs");

fs.readFile("package.json", "utf8", function (err, data) {
    if (err) console.error(err);
    console.log(data);
    fs.readFile("file2", "utf8", function (err, data) {
        if (err) console.error(err);
        fs.readFile("file3", "utf8", function (err, data) {
            if (err) console.error(err);
            fs.readFile("file4", "utf8", function (err, data) {
                if (err) console.error(err);
                fs.readFile("file5", "utf8", function (err, data) {
                    if (err) console.error(err);
                    fs.readFile("file6", "utf8", function (err, data) {
                        if (err) console.error(err);
                        fs.readFile("file7", "utf8", function (err, data) {
                            if (err) console.error(err);
                            fs.readFile("file8", "utf8", function (err, data) {
                                if (err) console.error(err);
                            });
                        });
                    });
                });
            });
        });
    });
});
```

### Problem of Inversion of Control

https://fullchee-reminders.netlify.app/link/2089

**Analogy**

[UI Dot Dev Async JS](https://fullchee-reminders.netlify.app/link/2088)

Busy Restaurant

-   callbacks: give the restaurant (3rd party library) your phone number (callback)
    -   we trust that they'll use the callback the way we expect
    -   call it once
    -   call it at the right time
    -   pass in the right args
    -   reality
        -   they can run the callback multiple times
        -   phone: can send you ads
        -   can't take back your phone number

Promises

-   fulfill a contract
    -   can't resolved 3 times in a row
        -   (state machine: once it's resolved, it can't go to another state)
-   promises: restaurant gives you a beeper that lets you know when you have a table
-   you decide what to do when the `.then()` is called or the `.catch()` is called

## Promises

### `.then()` example

```js
let file1;
file8Promise = fs
    .readFile("file1", "utf8")
    .then(function (_file1) {
        // NOTE: you NEED to return in order for the data to get passed into the function
        file1 = _file1;
        return fs.promises.readFile("file2", "utf8");
    })
    .then(function (file2) {
        console.log(file1);
        console.log(_file1); // errors out
        return fs.promises.readFile("file3", "utf8");
    })
    .then(function (file3) {
        return fs.promises.readFile("file4", "utf8");
    })
    .then(function (file4) {
        return fs.promises.readFile("file5", "utf8");
    })
    .then(function (file5) {
        return fs.promises.readFile("file6", "utf8");
    })
    .then(function (file6) {
        return fs.promises.readFile("file7", "utf8");
    })
    .then(function (file7) {
        return fs.promises.readFile("file8", "utf8");
    })
    .catch(function () {
        // if any of the 8 error out
        console.error(err);
    });
```

### async/await

```javascript
async function readFiles() {
    try {
        const file1 = await fs.promises.readFile("file1", "utf8");
        const file2 = await fs.promises.readFile("file2", "utf8");
        console.log(file1);
        const file3 = await fs.promises.readFile("file3", "utf8");
        const file4 = await fs.promises.readFile("file4", "utf8");
        const file5 = await fs.promises.readFile("file5", "utf8");
        const file6 = await fs.promises.readFile("file6", "utf8");
        const file7 = await fs.promises.readFile("file7", "utf8");
        const file8 = await fs.promises.readFile("file8", "utf8");
    } catch (error) {
        console.error(error);
    }
}
```

#### Using `useEffect` with `async/await`

-   `useEffect` can only return a cleanup function
-   need a wrapper

```jsx
useEffect(() => {
    const make_api_call = async () => {
        const response = await fetch();
        const data = await response.json();
    };
    make_api_call();
});
```

### What's a promise

#### My definition

-   magic box
-   call `.then()` or `await`
    -   it'll return the value
    -   or throw an error

One of 3 states

-   `pending`
-   `fulfilled`
-   `rejected`

### What can promises do that callbacks can't?

Run Promises simultaneously

```javascript
Promise.all([api(), api2(), api3()]).then(function(result) {
    //do work. result is an array contains the values of the three fulfilled promises.
}).catch(function(error) {
```

## [Non-intro notes to promises](/frontend/javascript/promises/promises)
