<iframe width="676" height="360" src="https://www.youtube.com/embed/zM9UPcIyyhQ" title="TypeScript: Should you use Types or Interfaces?" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## [`interface` vs `type`](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)

>[!Rule of thumb: which to use: interface vs type]-
>use types unless you need a specific feature of interfaces

>[!Why?]-
>interface: declaration merging
>if you redefine an interface somewhere else, it just extends it
>causes a bug

Interface vs type: not gonna be the TypeScript compiler bottleneck

>[!What only `interface` can do]-
>-   declaration merging
>-   interfaces can be changed after being created
>
>```ts
>interface Point {
>    x: number;
>}
>interface Point {
>    y: number;
>}
>//becomes: interface Point { x: number; y: number; }
>```

>[!What only `type` can do]-
>-   primitives
>    -   `#!ts type Name = string`
>-   unions
>    -   `#!ts type Id = string | number`
>-   tuples
>    -   `#!ts type Data = [number, string]`