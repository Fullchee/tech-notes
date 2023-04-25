# Setting up Storybook

!!! TODO: Update for Storybook 7

## Top Toolbar

![image](https://user-images.githubusercontent.com/11246258/158058778-c065bade-8d77-445c-ae5f-2275c95ee502.png)

[Control stories with custom toolbar items - YouTube](https://www.youtube.com/watch?v=DuJ_gmSncLM)

[Localize React with i18next in Storybook - YouTube](https://www.youtube.com/watch?v=sr0Pahym3VM)

### Internationalization

[Localize React with i18next in Storybook - YouTube](https://www.youtube.com/watch?v=sr0Pahym3VM)

-   msw

## Embedding an `iframe` in a Storybook add-on

```tsx
import React from "react";
import { addons, types } from "@storybook/addons";
import { AddonPanel } from "@storybook/components";

// give a unique name for the panel
const DesignNotesPanel = ({ api }) => {
    const { storyId } = api.getUrlState();
    return (
        <iframe
            src={`../docs/${storyId}`}
            frameBorder="0"
            width="100%"
            height="100%"
        />
    );
};

addons.register(ADDON_ID, (api) => {
    addons.add(PANEL_ID, {
        type: types.PANEL,
        title: "Design Notes",
        render: ({ active, key }) => (
            <AddonPanel active={active} key={key}>
                <DesignNotesPanel api={api} />
            </AddonPanel>
        ),
    });
});
```
