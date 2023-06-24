
Define types
```js
/**
 * @typedef {Object} User
 * @prop {string} email
 * @prop {string} name
 */
```

Import a typedef from other files

```js
/** @type {import('./User.js').User} */
```


as const
```js
return /** @type {const} */ ({a: 'a'})
```