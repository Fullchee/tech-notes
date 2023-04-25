[React TypeScript Cheatsheets](https://react-typescript-cheatsheet.netlify.app/docs/basic/setup/)

## React, JSDoc and JS

- [TypeScript-JSDoc-Guides.md · GitHub](https://gist.github.com/DeruiDENG/074b15de1ebc23ee8d307c14198c1231#work-with-react)

### Return type

[javascript - When to use JSX.Element vs ReactNode vs ReactElement? - Stack Overflow](https://stackoverflow.com/questions/58123398/when-to-use-jsx-element-vs-reactnode-vs-reactelement)

`JSX.Element` or `React.ReactElement`?

`React.ReactElement` works for an array of functions??

`React.ReactNode`
- type for children

### Type of a React "callable"

```typescript
interface ComponentProps {
    id: number;
}

const renderRoutes = (PassedComponent: React.ComponentType <ComponentProps>) => {
    return <PassedComponent
}
```

### Click event

```typescript
(event: React.MouseEvent<HTMLElement>) => void
```
