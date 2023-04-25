
[eslint-plugin-jsx-a11y - npm](https://www.npmjs.com/package/eslint-plugin-jsx-a11y)

[A little semantic HTML trick for React components — Queen Raae](https://queen.raae.codes/emails/2022-10-10-semantic-react/)

Card can have an `element` prop

```jsx
import React from "react";

export function Card({ element: Element = "div", children }) {
    return <Element>{children}</Element>;
}
```

```jsx
<Card element="aside">
    Something related to the article but a little outside of the normal flow.
</Card>
```


[[advanced-react-patterns#Solution: Prop Collections & Getters]]

```typescript
export const getClickOnEnterOrSpacebarProps = (props: UnknownObject) => ({
  role: 'button',
  className: 'cursor-pointer',
  tabIndex: 0,
  onKeyDown: triggerClickOnEnterKey,
  onKeyUp: triggerClickOnSpacebar,
  ...props,
});

```