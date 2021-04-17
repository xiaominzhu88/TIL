# React.memo && useMemo

- Memo

If you have a Component Counter:

```jsx
const Counter = () => {
	const [count, setCount] = useState(0);
	return (
		<div>
			<Title />
			<span>{`目前計數：${count}`}</span>
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
// 對 React 來說，只要 Counter 的 State 改變，它裡面的 DOM 就全都會被重新 Render，就算是沒有任何改變的 Title 也是一樣，因為它在 Counter 裡面
```

只需要在 Component 外包上 React.memo 就可以搞定了：

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

假設 Title 的內容是需要從外面傳進去的，然後用 Props 傳進去的內容是 Object，像是這樣子：

This will not work with object:

```jsx
const Title = React.memo((props) => {
	console.log('Render title component');
	const {
		title: { name },
	} = props; // {} === {}   => false
	return (
		<div>
			<h1>{name}</h1>
		</div>
	);
});

const Counter = () => {
	const [count, setCount] = useState(0);
	return (
		<div>
			<Title title={{ name: 'counter' }} />
			<span>{`目前計數：${count}`}</span>
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

就用 useMemo 吧！一個基本的 useMemo 長這樣子：

```jsx
const titleContent = useMemo(() => ({ name: 'counter' }), []);
```

Code Update:

```jsx
const Counter = () => {
	const [count, setCount] = useState(0);
	const titleContent = useMemo(() => ({ name: '計數器' }), []);
	// useMemo 會接收兩個參數
	// 第一個參數是函式，該函式回傳的內容會是一個memoized，它會把回傳的 { name: counter } 存放在 titleContent，
	// 第二個參數是一個 Array，只要該 Array 內的變數值沒有改變，那 useMemo 就不會重新產生一個 memoized，既然不會重新產生，那 Title 也就不會重新 Render 了！然後上方的 Array 是空的，也就代表不管在任何情況下，這個 useMemo 都不會重新產生 memoized。

	return (
		<div>
			<Title title={titleContent} />
			<span>{`目前計數：${count}`}</span>
			<button
				type="button"
				onClick={() => {
					setCount(count + 1);
				}}
			>
				點我加一
			</button>
		</div>
	);
};
```
