# TypeScript and Redux

## How to type the root state?

`DefaultRootState`

`RootStateOrAny`

### Typed `useSelector` 

```ts
export interface ReduxState {
	key: value;
	// ...
}
export const useStoreSelector: TypedUseSelectorHook<ReduxState> = useSelector;
```
