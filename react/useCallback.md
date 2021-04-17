# React useCallback

If the prop which was passed is a function, useMemo will not work:

```jsx
const Counter = () => {
	const [count, setCount] = useState(0);
	const titleContent = useMemo(() => ({ name: 'counter' }), []);
	const addCount = () => {
		setCount(count + 1);
	};

	return (
		<div>
			<Title title={titleContent} />
			<span>{`目前計數：${count}`}</span>
			<AddCountButton addCount={addCount} />
		</div>
		// addCount is a function
	);
};
```

We have to use useCallback, 如果說 useMemo 是為了對抗 reference 而存在，那 useCallback 就是為了 function

Code Example:

```jsx
const addCount = useCallback(() => {
	setCounte(count + 1);
}, []);
```

💥 But this will still not work:

```jsx
const Counter = () => {
	const [count, setCount] = useState(0);
	const titleContent = useMemo(() => ({ name: 'counter' }), []);
	const addCount = useCallback(() => {
		// 它和 useMemo 其實一模一樣，只差在 useCallback 會回傳整個 function 的 memoized，而不是回傳值，至於第二個參數的 Array 就和 useMemo 相同

		setCount(count + 1);
		// addCount 這個事件被 useCallback 處理掉了！它被包起來了，所以在 Counter 重新 Render 的時候 addCount 也不會產生一個新的 memoized，導致裡面的 count 一直都是最初的 0，這時候 0 不管再怎麼加 1 也都還是 1
	}, []);

	return (
		<div>
			<Title title={titleContent} />
			<span>{`目前計數：${count}`}</span>
			<AddCountButton addCount={addCount} />
		</div>
	);
};
```

🧚‍♀️ This works:

```jsx
setCount((currentCount) => currentCount + 1);
```
