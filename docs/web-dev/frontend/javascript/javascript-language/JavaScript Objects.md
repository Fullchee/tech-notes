### Destructure 3 levels down

```javascript
match = obj?.props?.match;
```

If you know the property will exist

```javascript
const {
    props: { match },
} = obj;
```

```javascript
const {
    a: {
        b: { c },
    },
} = obj;
```

## Default Dict

```javascript
(obj['key'] || obj['key'] = []).push('value')

(obj['key'] || obj['key'] = 0) += 1
```

## [`new` keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new#description)

1. Creates a new object 2. type: `object`
2. It sets this new object's internal, inaccessible, [[prototype]] (**proto**) property to be the constructor function's external, accessible, prototype object (every function object automatically has a prototype property).
3. Variable points to the newly created object.
4. Executes the constructor function
5. Return the new object
    1. unless the constructor function returns a non-null object reference.
    2. In this case, that object reference is returned instead.

### [How do you know if they used `new`?](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new.target)

```javascript
function Foo() {
    if (!new.target) {
        throw "Foo() must be called with new";
    }
}
```

### Why `Set()` returns an error without `new`

-   without the `new`, the constructor will get called as a regular function
-   it will use `this` from the caller's context and not from `Set` and it might break