# Export multiple Api Request Hook File

In one of my react project I want to structure and set my API Requests that make different calls in separate components.

I had several components like `Month.js, Daily.js, Week.js...`. In each of them I have a `POST/GET` request using `axios` which fetch different data from a base url with different `parameters` ( which is dynamically updated with user selections ).

This worked well with API calls in each Component, but the code was ugly and violated the `DRY` rules as the same API Options were used with this base url and the headers, the method.., so I decided to move everything to an API Request file and choose special option to use in the components.

- define each API request in e.g `hooks/ApiRequest.js` like this:

```jsx
const baseURL = '...';

const getSomeData = (someData, someDay) => {
	const options = {
		method: 'POST',
		url: `${baseURL}sign=${someData}&day=${someDay}`,
		headers: {
			'x-rapidapi-key': `${process.env.REACT_APP_KEY}`,
			'x-rapidapi-host': '...',
		},
	};
	return axios.request(options); // return is important
};

const getSomeOtherData = (someData) => {
	const options = {
		credentials: 'include',
		method: 'GET',
		url: `${baseURL}/${someData}`,
		headers: {
			'Access-Control-Allow-Methods': 'GET,POST,PUT,PATCH,DELETE',
			'x-rapidapi-key': `${process.env.REACT_APP_KEY}`,
			'x-rapidapi-host': '...',
			'Access-Control-Allow-Credentials': true,
		},
	};
	return axios.request(options); // return is important
};
```

ππ without `return`, an error throw out: `TypeError: Cannot read property βthenβ of undefined` after call it in the Component, and this mistake was what I did πΉ

- Export them

```jsx
export { getSomeData, getSomeOtherData };
```

- Using in Component

```jsx
import { getSomeData } from '../../hooks/ApiRequest.js';

useEffect(() => {
	getSomeData(param) // call getSomeData with param(someData)
		.then((response) => {
			setData(response.data[`${param}`]);
			setLoading(false);
		})
		.catch((error) => {
			console.error(error);
		});
}, [param]);
```
