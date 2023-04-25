# Writing your first Story

[⬅ Back to Why Storybook](01-why-storybook.md)

[Storybook docs: Writing stories](https://storybook.js.org/docs/react/writing-stories/introduction#using-args)

[Storybook blog: Writing stories in TypeScript](https://storybook.js.org/blog/writing-stories-in-typescript/)

!!! TODO: Update for Storybook 7

    ????

TOOLS TO CREATE STORIES FOR YOU
[GitHub - hussamkhatib/my-sb-app](https://github.com/hussamkhatib/my-sb-app)

[Storybook Snippets - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=jayantasamaddar.clk-storybook-snippets&ssr=false#overview)

## Create your file

-   `name.stories.tsx`
    -   or `.jsx`
-   can be anywhere in the `src` folder

## Imports

```tsx
import React from "react";
import { action } from "@storybook/addon-actions";
import { ComponentMeta, ComponentStory } from "@storybook/react"; // type generics

// import your component (don't need to import the props!)
import { AddButton } from "@src/Components/Button";
```

## [Story metadata (default export)](https://storybook.js.org/docs/react/writing-stories/introduction#default-export)

```tsx
export default {
    title: "Buttons/AddButton", // Buttons is the group in Storybook's sidebar
    component: AddButton,
    decorators: [],
    parameters: {
        componentSubtitle: "",
        design: {
            type: "figma",
            url: "https://www.figma.com/file/...",
        },
    },
} as ComponentMeta<typeof AddButton>;
```

## Create a story `Template`

```tsx
import { ComponentStory } from   '@storybook/react';

const Template: ComponentStory<typeof AddButton> = (args) => <AddButton {...args}>;
```

**JSX example**

```jsx
const Template = (args) => <AddButton {...args} />;
```

You may want to to create a wrapper

-   example: `Chart.stories.jsx`

```jsx
const Template = (args) => (
    <Card>
        <Chart {...args} />
    </Card>
);
```

### [Template with a `useState`](https://storybook.js.org/docs/react/writing-stories/introduction#working-with-react-hooks)

```jsx
const Template = (args) => {
    const [value, setValue] = useState(null);
    return (
        <Card>
            <Chart value={value} {...args} />
        </Card>
    );
};
```

-   If your component needs Redux, you may also need a wrapper like

```jsx
const Template = (args) => {
    return (
        <BrowserRouter>
            <Provider store={useMockStore(defaultState)}>
                <div style={{ backgroundColor: "white", padding: 20 }}>
                    <ConfigurableTable
                        {...args}
                        calculateAggregate={calculateTotal}
                    />
                </div>
            </Provider>
        </BrowserRouter>
    );
};
```

## Creating the stories

-   Pass in the props via the `args` property
-   `Template.bind({})` is a vanilla JS way of creating a copy of the function

```jsx
export const WithoutName = Template.bind({});
WithoutName.args = {
    onClick: action("onClick"),
};

export const WithName = Template.bind({});
WithName.args = {
    onClick: action("onClick"),
    buttonName: "My button name",
};
```

### Decorators example

-   Just like Python decorators
-   wrapper around each story

```jsx
[
    withContext,
    withReduxState({
        someKey: {
            someValue: {},
        },
    }),
];
```

## Debugging

### My story isn't appearing in the sidebar!

-   if there's a problem with the story, it'll fail without erroring out 😢
    -   look in the browser console for any errors
