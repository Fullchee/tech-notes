# JavaScript

## Strings

### Template Literals

Feels like Python `f"formatted_string"`

```javascript
myTag`A${1}B${2}C${3}D${4}E${5}F`;

function myTag(strings, ...args) {
    console.log(strings); // ['A', 'B', 'C', 'D', 'E', 'F']
    console.log(args); // [1,2,3,4,5]
    return strings;
}
```

### JS Regex

[[python-regex]]

[The dot in RegExp doesn't match all characters in JS](https://www.stefanjudis.com/today-i-learned/the-dot-in-regexp-doesnt-match-all-characters-in-javascript/)

#### `RegExp.test()` -> boolean

```javascript
console.log(/^([a-z0-9]{5,})$/.test('abc1')); // false
```


#### `String.match()` vs `RegExp.exec()`

[regex - match Vs exec in JavaScript](https://stackoverflow.com/questions/27753246/match-vs-exec-in-javascript)

`match` can do all at once with global flag
```javascript
console.log("[22].[44].[33].".match(/\d+/g));
// [ '22', '44', '33' ]
```

without global flag, will find the first

#### `RegExp.exec()`

has a nice syntax for looping with capturing groups?

One at a time
```js
// NEED THE global flag
myRegexp = /\[(\d+)\]/g

while (result = myRegexp.exec("[22].[44].[33].")) {
    console.log(result, myRegexp.lastIndex);
// [
//  '[33]',
//  '33',
//  index: 10,
//  input: '[22].[44].[33].',
//  groups: undefined
//  ] 14
}
```

## Numbers

### NaN

```javascript
Number.isNaN("a"); // false
isNaN("a"); // true

Number.isNaN(Number(input)) === isNan(input);
```

## Functions

### kwargs (obj --> params)

```js
const sum = (a, b) => a + b;
```

How do I pass this in `args = {a: 1, "1": 2}`?

Can't destructure

```jsx
// sum(args)  // a = args, b = undefined
// sum(...args)  // TypeError: Found non-callable @@iterator
```

#### Solution: get the object values as an array

```js
// order: [Does JavaScript guarantee object property order?](https://stackoverflow.com/a/23202095)
// 1. integer keys (like "11")
// 2. string keys
// 3. Symbol keys
argValues = Object.values(args); // [2,1]
c = sum(...argValues);
console.log(c);
```



## Importing

CommonJS vs AMD

at the start, commonJS sucked on browsers

AMD was used because people had to use it

you explicitly declare your dependencies for each function/module

now, neither are the best

Use a build tool

### Import a package in the dev tools

[Dynamic imports](https://stackoverflow.com/a/63784868/8479344)

```js
const { default: Confetti } = await import('https://cdn.skypack.dev/canvas-confetti');
```



## Symbols

### Why symbols

- All symbols are unique 
- For fully unique keys
-  private properties
	- (PITA to access)  
	  
[Unique sentinel values, identity checks, and when to use object() instead of None](https://treyhunner.com/2019/03/unique-and-sentinel-values-in-python/)
  
React uses symbols

