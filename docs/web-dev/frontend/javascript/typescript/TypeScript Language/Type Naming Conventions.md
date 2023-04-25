<iframe width="500" height="300" src="https://www.youtube.com/embed/qA65QjWCl60" title="How to Name your Types" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

>[!When to have a plural type name?]-
>only for arrays


>[!Why should types always be Pascal case?]-
>so the syntax highlighter doesn't get confused


## Generics
- `T`
- or prefixed with T
	- `TData`

```typescript
export type Response<T, U> = {
  data: T
  error: U
}
```

>[!Better generic name]-
>```typescript
>export type Response<TData, TError> = {
>  data: TData
>  error: UError
>}
>```


Why isn't this good?

```typescript
type TUser = {
  id: string;
  name: string;
}

interface IUser {
  id: string;
  name: string;
}
```

What if you want to turn an interface into a type?
- or vice versa?
- unnecessary refactoring
- just hover over to see the type definition