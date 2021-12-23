# Add comma after every element in an array except last element (React)

Let's say there is an array which contains multiple items

```jsx
const exampleArray = ['item1', 'item2', 'item3', 'item4', 'item5'];
```

🦋 The result should be like below, we want to render items with uppdercase and add commas between those items but except last one:

```jsx
Result Tabs: Item1, Item2, Item3, Item4, Item5
```

<hr />

👉 First create a function which convert each item to Uppercase:

```jsx
const renderUpperCase = (item) =>
	item !== null && item.charAt(0).toUpperCase() + item.slice(1);
```

👉 Then create **renderExampleItems** function, map the exampleArray and render items:

🌸 _we are prepending value, we have to make sure we dont add extra comma, for that just use ternary operator_

```jsx
const renderExampleItems = (exampleArray) => {
	return (
		<div>
			{exampleArray
				? exampleArray.map((item, index) => {
						// Since in JS 0 is falsey, for first iteration, nothing will be added
						return <>{`${index ? ',' : ''}  ${renderUpperCase(item)}`}</>;
				  })
				: 'Something went wrong'}
		</div>
	);
};
```
