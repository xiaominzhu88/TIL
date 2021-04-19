# Children inside Tags

When there are content inside the open and close tags of one of components ( example here as `Parent` component with <></> ), you can get access to it as the children prop.

```jsx
const Parent = ({ children }) => {
	return (
		<>
			<p>These are children names:</p>
			{children}
		</>
	);
};

const App = () => (
	<div>
		<Parent>Lola and Zhu</Parent>
	</div>
);

// These are children names:
// Lola and Zhu
```

🧩 If there is also a `children` prop, the content inside the open and close tags will take over the children prop ( here: `Bubu` ).

```jsx
const App = () => (
	<div>
		<Parent children="Bubu">Lola and Zhu</Parent>
	</div>
);

// Lola and Zhu
```
