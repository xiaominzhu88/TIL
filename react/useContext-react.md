# useContext React

Context provides a way to pass data through the component tree without having to pass props down manually at every level.

Code Example:

```jsx
// src/ThemeContext.js

import React from 'react';

const ThemeContext = React.createContext(null);

export default ThemeContext;
```

The Context's Provider component can be used to provide the theme to all React child components below this React top-level component which uses the Provider:

```jsx
// src/ComponentA.js

import React from 'react';
import ThemeContext from './ThemeContext';

const A = () => (
	<ThemeContext.Provider value="green">
		<D />
	</ThemeContext.Provider>
);
```

Somewhere below component A,( ! not component D ), but any other child component, e.g component C, will use this theme to style itself:

```jsx
// src/ComponentC.js

import React from 'react';
import ThemeContext from './ThemeContext';

const C = () => (
	<ThemeContext.Consumer>
		{(color) => <p style={{ color }}>Hello World</p>}
	</ThemeContext.Consumer>
);
```

🐹 But as you can see, the Consumer component coming from React's Context is by default a "render prop component". In a world where we can use 🧤 React Hooks, a render prop component isn't always the best choice.

So the previous example with React's **useContext** Hook:

```jsx
// src/ComponentC.js

import React from 'react';
import ThemeContext from './ThemeContext';

const C = () => {
	const color = React.useContext(ThemeContext);

	return <p style={{ color }}>Hello World</p>;
};
```
