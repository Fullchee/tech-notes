# Multi-threaded JavaScript

<iframe
  width="713"
  height="360"
  src="https://www.youtube.com/embed/8aGhZQkoFbQ"
  title="What the heck is the event loop anyway? | Philip Roberts | JSConf EU"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
  allowfullscreen
></iframe>

## Web Assembly (WASM)

-   example: Figma
    -   the menus are in React
    -   the main body is in Rust

## Web workers

Web worker vs main thread

-   no access to DOM
-   can still `fetch()`, `setTimeout()`

## Service workers

### Web workers vs service workers

## Generators

same as Python!

```javascript
function* fibonacci() {
    let [prev, curr] = [0, 1];
    while (true) {
        [prev, curr] = [curr, prev + curr];
        yield curr;
    }
}

for (n of fibonacci()) {
    if (n > 100) break;
    console.log(n);
}
```

```bash
1
2
3
5
8
13
21
34
55
89
```

### Generators before async/await

How `async/await` is implemented behind the scenes

Before async/await, you needed a library

```javascript
var prom = require("bluebird");
```

```javascript
var mongo = prom.promisifyAll(require("mongodb"));
var MongoClient = mongo.MongoClient;

var connectToMongo = prom.coroutine(function* () {
    var db = yield MongoClient.connect(mongoURL);
    return db;
});

var doMongo = prom.coroutine(function* () {
    var db = yield connectToMongo("mongodb://localhost:27017");
});
```
