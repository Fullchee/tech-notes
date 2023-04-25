# TypeScript

## [[TypeScript and React]]

## Comments

-   ignore a rule for the whole file

```javascript
/* eslint-disable rule-name */
// @ts-nocheck (ignores the whole file)
```

-   ignore the rule for one line

```javascript
/* eslint-disable-next-line rule-name */

// @ts-ignore (ignores one line)
```

## Checking types

### [`instanceof` vs `typeof`](https://stackoverflow.com/a/6625960/8479344)

JS built-ins

-   `instanceof` for custom types
-   `typeof` for the simple built-in types

### [User Defined Type Guards](https://basarat.gitbook.io/typescript/type-system/typeguard#user-defined-type-guards)

Return type isn't a boolean!

```ts
function isFish(pet: Fish | Bird): pet is Fish {
    return (pet as Fish).swim !== undefined;
}
```

#### User defined type guards aren't type checked!

[The complete guide to safe type narrowing in TypeScript](https://blog.thoughtspile.tech/2023/01/31/typescript-safe-narrow/)

Design choice: [Suggestion: check narrowed type in user-defined type guards · Issue #29980 · microsoft/TypeScript · GitHub](https://github.com/microsoft/TypeScript/issues/29980)

```ts
const isNumber = (num: unknown): num is number => {
  return typeof num === 'string';
}

const nums = [1, '2', 3]
const onlyNumbers: number[] = nums.filter(isNumber)
console.log(onlyNumbers) // ["2"]
```

#### Downcast function: Alternative 1 to user defined type guard

```ts
function toNumber(arg: unknown, fallback: number): number {  
	if (typeof arg === 'number') return arg;
	if (typeof arg === 'string') return Number(arg);
	return fallback;
}
```

#### Discriminating union: alternative 2 to user defined type guard

[User-Defined Type Guards aren't safe](https://unsplash.com/blog/user-defined-type-guards-not-safe/)

Narrow down from a union

```ts
type Hotdog = {
  _tag: 'Hotdog';
};

type Burger = {
  _tag: 'Burger';
};

type Food = Hotdog | Burger;

// This little helper provides a safer way to narrow the type.
const is = <A, B extends A>(fn: (a: A) => B | undefined) => {
  return (a: A): a is B => typeof fn(a) !== 'undefined';
};

const isBurger = is<Food, Burger>(food => (food._tag === 'Burger' ? food : undefined));

const foods = [{ _tag: 'Hotdog' }, { _tag: 'Burger' }];

const a = foods.filter(isBurger);
console.log(a);
```

## Type Generation

-   [MakeTypes](https://jvilk.com/MakeTypes/)
    -   Generates interfaces from JSON
-   https://github.com/swagger-api/swagger-codegen

## Strings

Convert something to a string

`String(123)`


## Generics

-   Inferred generic: (from the params)
-   example: `React.useState()`
    -   explicitly: `React.useState<UnknownObject>({})`

### Importing a `type` that's the same name as the `class`

When working with `progressbar.js`, I was getting errors

When I tried importing the `Shape`,

```jsx
import ProgressBar, { PathDrawingOptions, Shape } from "progressbar.js";
```

it was still importing the Shape object and not the type

VSCode complains because it knows that Shape isn't a type
- it suggests `typeof Shape` which isn't right because ????

#### Solution

There's a separate import for the `Shape`

```jsx
import type Shape from "progressbar.js/shape";
```


## `declare` keyword

Example: importing from a JS library

Declare that some variable that you has this type

```typescript
declare let module: any;

declare const module = { doSomething: () => boolean };
```
