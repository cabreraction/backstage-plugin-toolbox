# Getting started

## Installation

Add the plugin to your frontend app:

```bash
cd packages/app && yarn add @drodil/backstage-plugin-toolbox
```

Expose the toolbox page:

```ts
// packages/app/src/App.tsx
import { ToolboxPage } from '@drodil/backstage-plugin-toolbox';

// ...

const AppRoutes = () => (
  <FlatRoutes>
    // ...
    <Route path="/toolbox" element={<ToolboxPage />} />
    // ...
  </FlatRoutes>
);
```

Add the navigation in the frontend:

```ts
// packages/app/src/components/Root/Root.tsx
import BuildIcon from '@material-ui/icons/Build';

// ...

export const Root = ({ children }: PropsWithChildren<{}>) => (
  <SidebarPage>
    // ...
    <SidebarItem icon={BuildIcon} to="toolbox" text="ToolBox" />
    // ...
  </SidebarPage>
);
```

An interface for toolbox is now available at `/toolbox`.

## Adding your own tools

You can also add your own tools to the plugin by passing them to the ToolboxPage as a property:

```ts
import { ToolboxPage, Tool } from '@drodil/backstage-plugin-toolbox';

const extraToolExample: Tool = {
  name: 'Extra',
  component: <div>Extra tool</div>,
};

<ToolboxPage extraTools={[extraToolExample]} />;
```

Also lazy loading is supported:

```ts
import React, { lazy } from 'react';
import { ToolboxPage, Tool } from '@drodil/backstage-plugin-toolbox';
const MyTool = lazy(() => import('./MyTool'));

const extraToolExample: Tool = {
  name: 'Extra',
  component: <MyTool />,
};

<ToolboxPage extraTools={[extraToolExample]} />;
```

## Adding tools to custom home page

You can add tools to the Backstage custom home page as follows:

```tsx
import { CustomHomepageGrid } from '@backstage/plugin-home';
import { ToolboxHomepageCard } from '@drodil/backstage-plugin-toolbox';
import { Content, Page } from '@backstage/core-components';

export const HomePage = () => {
  return (
    <Page themeId="home">
      <Content>
        <CustomHomepageGrid>
          <ToolboxHomepageCard />
        </CustomHomepageGrid>
      </Content>
    </Page>
  );
};
```

This allows the home page users to configure the card so that their favorite tool is available in their home page.
For more information, see https://github.com/backstage/backstage/pull/16744
