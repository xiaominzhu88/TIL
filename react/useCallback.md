# React useCallback

If the prop which was passed is a function, useMemo will not work:

```jsx
const Counter = () => {
	const [count, setCount] = useState(0);
	const titleContent = useMemo(() => ({ name: 'counter' }), []); // ok
	
	const addCount = useMemo(() => setCount(count + 1),[]); // not ok, addCount is a function

	return (
		<>
			<Title title={titleContent} />
			<span>{`Current：${count}`}</span>
			<AddCountButton addCount={addCount} /> 
		</>
	);
};
```

We have to use useCallback, 💥 but after update the code like below, this will still not work:

```jsx
const addCount = useCallback(() => {
	setCounte(count + 1);
}, []);
```
```jsx
const Counter = () => {
	const [count, setCount] = useState(0);
	const titleContent = useMemo(() => ({ name: 'counter' }), []);
	
	// addCount function is handled by useCallback, wrapped with useCallback
	// when the Counter is re-rendered, addCount will not generate a new memoized of the entire function
	// so the count inside is always the original 0. At this time, 0 is still 1 no matter how much you add
	const addCount = useCallback(() => {
		// same as useMemo, except that useCallback will return the memoized of the entire function instead of returning the value. 
		// second parameter Array is the same as useMemo
		setCount(count + 1);
	}, []);

	return (
		<>
			<Title title={titleContent} />
			<span>{`Current：${count}`}</span>
			<AddCountButton addCount={addCount} />
		</>
	);
};
```

🧚‍♀️ This works:

```jsx
setCount((currentCount) => currentCount + 1);
```
