# Find longest in Array

Code Example

```jsx
const array = ['Apple', 'Pine-apple', 'Banana', 'Jack-fruit'];

const longest = array.reduce((longest, current) => {
	if (longest.length < current.length) {
		return current;
	}

	return longest;
});

console.log(longest); // Pine-apple
```
