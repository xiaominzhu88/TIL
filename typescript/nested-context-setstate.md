# Set Parent state with nexted Context | typescript

[codesandbox](https://codesandbox.io/s/context-typescript-7nznb8?file=/src/App.tsx)

1. Wrap the components that need the context with a context provider:

```jsx
import { FirstChild } from './FirstChild';
import { createContext, Dispatch, SetStateAction, useState } from 'react';

// define both context types
export type ThemeContextType = {
	theme: string,
	setTheme: Dispatch<SetStateAction<string>>,
};
export type NameContextType = {
	name: string,
	setName: Dispatch<SetStateAction<string>>,
};

// export both context so that child components have access
export const ThemeContext =
	createContext <
	ThemeContextType >
	{
		theme: 'dark',
		setTheme: () => undefined,
	};

export const NameContext =
	createContext <
	NameContextType >
	{
		name: 'React',
		setName: () => undefined,
	};

export default function App() {
	const [theme, setTheme] = useState('dark');
	const [name, setName] = useState('React');

	return (
		// nested context can be used for different child components
		// pass set function and context value
		<ThemeContext.Provider value={{ theme, setTheme }}>
			<NameContext.Provider value={{ name, setName }}>
				<FirstChild />
			</NameContext.Provider>
		</ThemeContext.Provider>
	);
}
```

2. Call useContext to read and subscribe to the context.

```jsx
// Second child
import { LastChild } from './LastChild';
import { useContext } from 'react';
import { ThemeContext, NameContext } from './App';

export const SecondChild = () => {
	// use context value and set parent THEME
	const { theme, setTheme } = useContext(ThemeContext);
	const { name } = useContext(NameContext);

	return (
		<div
			style={{
				color: name === 'React' ? 'pink' : 'blue',
				backgroundColor: theme === 'dark' ? 'grey' : 'white',
				padding: '2rem',
			}}
		>
			It's {theme} !
			<br />
			<button onClick={() => setTheme('light')}>Get light</button>
			<LastChild />
		</div>
	);
};
```

```jsx
// Last child
import { useContext } from 'react';
import { NameContext } from './App';

export const LastChild = () => {
	// use context value and set parent NAME
	const { name, setName } = useContext(NameContext);
	return (
		<>
			HELLO: {name} !
			<button onClick={() => setName('Angular')}>Go to Angular</button>
		</>
	);
};
```

<image src='image/dark.png' alt='dark'>
<image src='image/angular.png' alt='angular'>
<image src='image/dark-angular.png' alt='dark-angular'>
