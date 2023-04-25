# Next JS

## Debugging

-   try deleting the `.next` folder
    -   could be a caching issue
    -   kinda like reinstalling your node modules

## Components on every page

How you add the same header & footer to every page

!!! What if you don't want that custom app for certain pages?

https://nextjs.org/docs/basic-features/typescript#custom-app

Create `./pages/_app.js`

### [Custom Document](https://nextjs.org/docs/advanced-features/custom-document)

`pages/_document.js`

-   edit the HTML tag

```tsx
NextScript } from 'next/document'

export default function Document() {
  return (
    <Html>
      <Head lang="en-CA"/>
      <body>
        <Main />
        <NextScript />
      </body>
    </Html>
  )
}
```
