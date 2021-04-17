# Persisting state between page reloads

### Use LocalStorage

```jsx
useEffect(() => {
	setCount(JSON.parse(window.localStorage.getItem('count')));
}, []);
// retrieve the stored value from LcoalStorage at the initialization.

useEffect(() => {
	window.localStorage.setItem('count', count);
}, [count]);
// track changes and update the LocalStorage.
```
