# Styled Components 💅🏾

CSS in JS

Why

-   Scoped CSS

uses [template literals](https://fullcheezhang.com/frontend/javascript/javascript/?h=template+literal#template-literals)

```javascript
import styled from "styled-components";
const Logo = styled.h1`
    font-size: 4rem;
`;
```

## Global styles

```javascript
const GlobalStyles = createGlobalStyle`
    @font-face {
    ...
    }
    :root {
        --black: #393939
        --grey: #393939
        --gray: var(--grey)
    }
`;

const Page = () => (
    <div>
        <GlobalStyles />
        <Header />
        <InnerStyles>{children}</InnerStyles>
    </div>
);
```

## Next JS and Styled components

-   https://styled-components.com/docs/advanced#server-side-rendering
-   https://courses.wesbos.com/account/access/5fbfe7466ef8b359b1d11782/view/505027401
-   example: https://github.com/vercel/next.js/blob/canary/examples/with-styled-components-babel/pages/_document.tsx#L10

1. The server renders things
    - styled components generates random IDs
2. and client renders again
    - styled components renders a different random ID

```
Prop `className` did not match.
Server: "sc-asdf"
Client: "sc-fdsa"
```

### Solution: ServerStyleSheet

Next JS hook: `getInitialProps`

-   wait until the method has been resolved
-   then it sends the data (server --> browser)
