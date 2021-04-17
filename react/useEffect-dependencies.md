# Add Dependencies to useEffect

The `useEffect` hook is all about performing side-effects (e.g API calls).

The second argument to `useEffect` is where to
declare all of the values that are depended on within the `useEffect`.

_For example API call, this array is likely made up of parameters passed to that call._

- Giving it an empty array acts like componentDidMount as in, it only runs once
- Without second argument acts as both `componentDidMount` and `componentDidUpdate`, as in it runs first on mount and then on `every re-render`.
- Array with any value inside, ([variable1]) will only execute the code inside useEffect hook `ONCE` on mount, as well as whenever that particular variable `(variable1)` changes.

Code Example:

```jsx
useEffect(() => {
	const options = {
		credentials: 'include',
		method: 'GET',
		url: `https://.../${astro}`,
		headers: {
			'x-rapidapi-key': `${process.env.REACT_APP_KEY}`,
			'x-rapidapi-host': '...rapidapi.com',
		},
	};
	axios
		.request(options)
		.then(function (response) {
			setMonthData(response.data[`${astro}`]);
		})
		.catch(function (error) {
			console.error(error);
		});
}, [astro]);
```

It is safer to specify all of the values used in the body of the `useEffect`
all of them.
