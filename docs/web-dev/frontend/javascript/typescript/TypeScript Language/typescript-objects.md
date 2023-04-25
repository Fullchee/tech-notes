# TypeScript Objects

```typescript
const activeGlobalFilters = typeToFilter[
    globalFilter
] as typeof filterOptions[keyof typeof filterOptions];
```

## Object that has at least these two properties

```typescript
<T extends {first: string; last: string}>(obj: T)
```

```typescript
/**
 * Make all properties in T optional
 */
type Partial<T> = {
    [P in keyof T]?: T[P];
};
```

```typescript
/**
 * Make all properties in T required
 */
type Required<T> = {
    [P in keyof T]-?: T[P];
};
```

## Extend a type

```ts
interface LoadingWidgets {
    [widgetId?: number]: boolean;
}

interface IsLoading {
    widgets: LoadingWidgets;
    [key?: string]: boolean | LoadingWidgets;
}
```

## Avoid optional properties

-   Explicitly model which combinations exist and which don't

```ts
interface Product {
    id: string;
    type: "digital" | "physical";
    weightInKg?: number;
    sizeInMb?: number;
}
```

```ts
interface Product {
    id: string;
    type: "digital" | "physical";
}

interface DigitalProduct extends Product {
    type: "digital";
    sizeInMb: number;
}

interface PhysicalProduct extends Product {
    type: "physical";
    weightInKg: number;
}
```

## Record

Restrict what the key and the value can be
- restrict the keys (`string` union)
- restrict the values

```typescript
type User = {
    name: string;
    email: string;
};
type Country = "uk" | "france" | "india";

const myData: Record<Country, User> = {
    uk: { name: "John", email: "a@a.a" },
    france: { name: "Sarah", email: "a@a.a" },
    india: { name: "Jane", email: "a@a.a" },
};
```

### Empty object

```typescript
type PropertyKey = string | number | symbol
const a: Record<PropertyKey, never> = {}
```

### Record: object of string -> string

```typescript
Record<string, string>;
```

## `object` type vs `UnknownObject`

```typescript
interface UnknownObject {
    [key: string]: unknown;
}

type UnknownObject = Record<string, unknown>;
```

`object` will match functions too!

```typescript title="thisIsValid.ts"
const a: object = () => {};
```

```typescript
(a: object) => a.something  // error

(a: UnknownObject) => a.something // unknown
```


Narrowing which props are accepted for subtypes

There is something


### Enums

-   enums have issues
-   union of strings
-   `type Options = 'one' | 'two' | 'three'`
-   https://react-typescript-cheatsheet.netlify.app/docs/basic/troubleshooting/types/#enum-types

May be fixed in TypeScript 5.0?


### How to iterate over string union

```javascript
const names = ["Bill Gates", "Steve Jobs", "Linus Torvalds"] as const;
type Names = typeof names[number];
```