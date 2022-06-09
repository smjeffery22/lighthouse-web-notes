# Material UI

## Install and CDN MUI

```
npm install @mui/material @emotion/react @emotion/styled
```

```html
<link
	rel="stylesheet"
	href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap"
/>
```

## CssBaseline

- Default styling for MUI applications
  - Similar to `normalize.css`
    - The margin in all browsers is removed
    - The default Material Design background color is applied
    - Font antialiasing is enabled for better display of the Roboto font
    - No base font-size is declared on the <html>, but 16px is assumed (browser default)

```jsx
import { CssBaseline } from '@mui/material';

return (
	<div>
		<CssBaseline /> {/* apply normalize.css */}
		{/* Application code.. */}
	</div>
);
```

## Typography

```jsx
import { Typography } from '@mui/material';
```

## Container

- Container centers content horizontally
- Max width can be set using `maxWidth` props

## Grid

- Material Design responsive layout grid adapts to screen size and orientation
- Props `container` allows the component to have *flex* container behaviour
  - Wrap in `<Container></Container>` component

