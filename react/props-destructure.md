# Destructure Props to child Component (functional)

When passing down props, typical like this.

```jsx
const MyComponent = () => {
	const firstName = '...';
	const lastName = '...';
	return (
		<div>
			<ChildComponentOne />
			<ChildComponentTwo firstName={firstName} lastName={lastName} />
		</div>
	);
};
```

To access props in ChildComponentTwo:

```jsx
const ChildComponentTwo = (props) => {
	return (
		<div>
			<p>{props.firstName}</p>
			<p>{props.lastName}</p>
		</div>
	);
};
```

🦋 Destructuring our props lets us drop all of the **props**:

Code Example:

```jsx
const ChildComponentTwo = ({ lastName, firstName }) => {
	return (
		<div>
			<p>{firstName}</p>
			<p>{lastName}</p>
		</div>
	);
};
```
