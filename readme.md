# @charlietango/emotion-sx

### Using `sx` prop

Normally when running [emotion](https://www.emotion.sh/) through Babel you can use the `css` prop -
this allows you to write the tagged template or Object styling directly on the components. It's then
converted into a style and `className` by Babel.

We extend this setup by adding support for [@styled-system/css](https://styled-system.com/css) under
a new `sx` props. This allows us to consume the theme and add responsive values with arrays. This is
done by creating a custom JSX Pragma that adds support for the `sx` prop on all React elements.

```jsx harmony
const Example = () => (
  <div
    sx={{
      color: 'red',
      px: [3, 6],
    }}
  />
);
```

> Make sure
> [@charlie-tango/babel-preset-sx-prop](https://github.com/charlie-tango/babel-preset-sx-prop) is
> installed, otherwise the `sx` prop will not do anything.

### Custom JSX pragma

If you can't add
[@charlie-tango/babel-preset-sx-prop](https://github.com/charlie-tango/babel-preset-sx-prop) to the
project, you can still use the `sx` prop by defining a custom JSX Pragma in the React file.

Include this at the top of the file:

```tsx
/** @jsx jsx */
import { jsx } from '@charlietango/emotion-sx';
```

This replaces the normal `import * as React from 'react'` (which imports the default JSX from
React).

## Base CSS

The library includes a `<BaseCss />` Global styles file - It's built on top of
[sanitize.css](https://github.com/csstools/sanitize.css), with some of our settings included.

```typescript jsx
import { ThemeProvider } from '@emotion/react';
import { BaseCss, baseTheme } from '@charlietango/ui';

const App = () => (
  <ThemeProvider theme={baseTheme}>
    <BaseCss />
    <App />
  </ThemeProvider>
);
```

In addition to this, it also extracts a few values (if set) from the theme, and defines as global
defaults.

```css
html {
  background-color: 'theme.colors.background';
  color: 'theme.colors.text';
  font-family: 'theme.fonts.body';
}
```
