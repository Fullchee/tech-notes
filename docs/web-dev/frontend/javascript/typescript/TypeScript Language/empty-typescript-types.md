# Empty TypeScript Types

All fields in JS can have the value `null` or `undefined`

unless strict mode is enabled

-   `unknown`
    -   I don't know
        -   could be anything
    -   need to type check/guard
-   `any`
    -   I don't care

## [`never`](https://stackoverflow.com/a/54243343/8479344)

things that should never happen

```ts
const reportError = function (): never {
    throw Error("my error");
};

const loop = function (): never {
    while (true) {}
};
```

-   prune conditional types

```ts
type NonNullable<T> = T extends null | undefined ? never : T;

// NonNullable<MyType> can't be assigned null or undefined
type A = NonNullable<number | null>; // number
```

-   infinite loops
-   only ever throwing errors

## Forcing a `number` to not be `undefined`

Only in strict mode???

This still lets `myNum` be `undefined`

```typescript
type NotUndefinedButNullable<T> = T extends undefined ? never : T;
type NumberOrNull = NonNullable<number>;

const myNum1: NumberOrNull = undefined;
const myNum2: NotUndefinedButNullable<number> = undefined;
```




>[!Void vs undefined]-
>Void: the return value won't be observed/used, if you use this function, don't bother getting the return value
>eg: setValue()
>
>undefined: the return value is still useful
>const user = getUser()
>if (!user) ...