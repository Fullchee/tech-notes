# Using Storybook

See YouTube channel

## Top Toolbar

![image](https://user-images.githubusercontent.com/11246258/158058778-c065bade-8d77-445c-ae5f-2275c95ee502.png)

### Canvas

-   play around with one story
-   ![width:800px](https://user-images.githubusercontent.com/11246258/158720714-1be5666e-0ba3-43ec-83c7-1951af8b9454.png)

### Docs

![width:800px](https://user-images.githubusercontent.com/11246258/158720996-9591b243-5c75-422b-9d9e-a7d199209dbc.png)

## Add-ons (Bottom toolbar)

![image](https://user-images.githubusercontent.com/11246258/158058822-dc62aa07-8b85-48ee-bce1-526ae3449c27.png)

### Controls 🕹️

-   replaces the `knobs` add on
-   ![width:1000px](https://user-images.githubusercontent.com/11246258/158058729-c9553bc7-1474-425e-835e-f4d35bda4541.png)

---

### Actions

![image](https://user-images.githubusercontent.com/11246258/158293001-0acb6216-0dc1-4695-aa66-a9bef7dbaa43.png)

-   see what parameters are being passed in to event handlers

-   [MSW (Mock Service Worker)](https://storybook.js.org/addons/msw-storybook-addon)
-   [Mock query params](https://github.com/storybookjs/addon-queryparams)
-   [Interaction Testing](https://storybook.js.org/addons/@storybook/addon-interactions)

### Accessibility

-   runs some a11y tests
-   recommends some manual checks
    ![image](https://user-images.githubusercontent.com/11246258/158293213-769371f6-da7c-4ff4-b46f-157afdc91425.png)

## Troubleshooting

### Storybook is stuck loading locally!

If you're getting this error in the browser console: `Singleton client API not yet initialized`

Reinstall your node_modules

```
rm -f package-lock.json && rm -rf node_modules && npm i
```

### The bottom controls bar disappeared! What do I do?

You may have pressed `S`, `A`, `T` or `F` which toggle the visibility of the controls

<img
  src="https://user-images.githubusercontent.com/11246258/161261251-8a1953c3-1092-413e-83de-e67065562cee.png"
  width="300px"
/>

![width:250px](https://user-images.githubusercontent.com/11246258/158721400-3728d42b-473b-4207-9bb5-27cd84719db8.png)

-   I don't see the add-ons toolbar!
    -   Keyboard shortcut: Press `S` `A` `T`

### Why isn't my story showing up?

1. Did you name it \*.stories.tsx?
2. Is there a syntax/runtime error in your story? (check the browser console)
3. Is the default export's **title** unique?

### How do I change the order of stories?

[Modify the order in `.storybook/preview.js`](https://storybook.js.org/docs/react/writing-stories/naming-components-and-hierarchy)
