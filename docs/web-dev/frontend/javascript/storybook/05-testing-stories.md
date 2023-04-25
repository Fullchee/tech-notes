# Testing Stories

## Unit testing

### 1. React Testing Library imports

```jsx
import React from "react";
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import "@testing-library/jest-dom/extend-expect";
```

### 2. Storybook imports

-   instead of importing the component
    -   re-use the stories
        -   just JS
        -   where the component is already setup and has props

```jsx
// composeStories will add the decorators in your stories, optional
import { composeStories } from "@storybook/testing-react";
import * as stories from "@src/stories/EarningsCell.stories";

// wrap the stories with the decorators defined in the story
const { ButtonWithoutName, ButtonWithName } = composeStories(stories);
```

### 3. Regular React Testing Library!

```jsx
const earnerCell = render(<ButtonWithoutName {...DefaultEarningsCell.args} />);
const infoIcon = earnerCell.getByTest("test-id");
userEvent.hover(infoIcon);
const infoPopover = screen.getByTestId("button-popover");
expect(infoPopover).toHaveTextContent("Some text");
```

## Component Testing

????

[Component testing in Storybook with play functions - YouTube](https://www.youtube.com/watch?v=dcuzwCHI940)

## Interactive tests

-   https://storybook.js.org/blog/interaction-testing-with-storybook/

![width:800px](https://storybookblog.ghost.io/content/images/2022/02/account-form-viz.gif)

## Regression testing with Chromatic

-   Example where I make a change to the `Card` component
    ![width:1000px](https://user-images.githubusercontent.com/11246258/158290938-f8261168-8d32-4b3d-b602-79f8e3b335ff.png)
