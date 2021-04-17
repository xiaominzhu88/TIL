# JSX Spread Operator <Component {…props} />

If you already have props as an object, and you want to pass it in JSX, you can use ... as a “spread” operator to pass the whole props object.

These two components are equivalent:

```jsx
function App1() {
	return <Greeting firstName="Lola" lastName="Zhu" />;
}

function App2() {
	const props = { firstName: 'Lola', lastName: 'Zhu' };
	return <Greeting {...props} />;
}
```

You can also pick specific props that your component will consume while passing all other props using the spread operator.

```jsx
const Button = (props) => {
	const { kind, ...other } = props;
	const className = kind === 'primary' ? 'PrimaryButton' : 'SecondaryButton';
	return <button className={className} {...other} />;
};
// The kind prop is safely consumed and is not passed to the <button> element in the DOM.

const App = () => {
	return (
		<div>
			<Button kind="primary" onClick={() => console.log('clicked!')}>
				Hello World!
			</Button>
		</div>
	);
};
// All other props are passed via the ...other object making this component really flexible, it passes an onClick and children props.
```
