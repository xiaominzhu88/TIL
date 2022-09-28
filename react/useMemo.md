# React.memo && useMemo

- Memo

If you have a Component Counter:

```jsx
const Counter = () => {
	const [count, setCount] = useState(0);
	return (
		<div>
			<Title />
			<span>{`Current：${count}`}</span>
			<button
				type="button"
				onClick={() => {
					setCount(count + 1);
				}}
			>
				Add 1
			</button>
		</div>
	);
};
// as long as the State of the Counter changes, all the children will be re-rendered, even if Title component stays the same, because it is inside the parent component Counter 
```

👉 Fix: wrap the child component with React.memo:

```jsx
const Title = React.memo(() => {
	console.log('Render title component');
	return (
		<div>
			<h1>counter</h1>
		</div>
	);
});
```

- useMemo

Suppose the props for Title component need to be passed in from the parent

This will not work with object:

```jsx
const Title = React.memo((props) => {
	console.log('Render title component');
	const { title: { name } } = props; // 💥 {} === {}   => false
	return (
		<div>{name}</div>
	);
});

const Counter = () => {
	const [count, setCount] = useState(0);
	return (
		<div>
			<Title title={{ name: 'counter' }} />
			<span>{`Current：${count}`}</span>
			<button
				type="button"
				onClick={() => {
					setCount(count + 1);
				}}
			>
				Add 1
			</button>
		</div>
	);
};
```

👉 In this case, useMemo! A basic useMemo looks like this:

```jsx
const titleContent = useMemo(() => ({ name: 'counter' }), []);
```

Code Update:

```jsx
const Counter = () => {
	const [count, setCount] = useState(0);
	const titleContent = useMemo(() => ({ name: 'counter' }), []);
	// useMemo accepts 2 parameters
	// first parameter is a function which returns memoized value，it stores { name: counter } inside titleContent，
	// second parameter is an Array，as long as the value in the Array does not change, useMemo will not regenerate a memoized value
	// Title will not re-Render because Array is empty, which means that in any case, useMemo will not regenerate.

	return (
		<div>
			<Title title={titleContent} />
			<span>{`Current：${count}`}</span>
			<button
				type="button"
				onClick={() => {
					setCount(count + 1);
				}}
			>
				Add 1
			</button>
		</div>
	);
};
```
