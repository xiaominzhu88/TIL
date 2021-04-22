# Fix the useEffect async function Error

The ‘React Hook Warnings for async function in useEffect:

👉 `useEffect function must return a cleanup function or nothing`

This error may occur when try to pass in an `async function` as an argument of the first argument of the `useEffect` hook.

🍬 The `useEffect` hook’s first argument cannot be an async function.

To use an async function, should define it outside the function and call it:

```jsx
import { useEffect, useState } from 'react';
export default function App() {
	const [data, setData] = useState({});

	const getData = async () => {
		const res = await fetch('https://...../api');
		const data = await res.json();
		setData(data);
	};
	// define getData() outside

	useEffect(() => {
		getData(); // call it
	}, []);

	return (
		<div className="App">
			<p>{JSON.stringify(data)}</p>
		</div>
	);
}
```

Or define it inside the function and call it.

```jsx
useEffect(() => {
	const getData = async () => {
		// define getData() inside
		const res = await fetch('https://...../api');
		const data = await res.json();
		setData(data);
	};

	getData(); // call it
}, []);
```

It' not possible to pass an async function into the useEffect as its first argument because it may lead to race conditions. Async functions complete in an indeterminate amount of time, and hooks order matter.

🤞 My favorite: call `then` and `catch` in the useEffect callback.

```jsx
useEffect(() => {
	fetch('https://...../api')
		.then((res) => res.json())
		.then((data) => setData(data));
}, []);
```
