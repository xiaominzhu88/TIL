# Filter distance using geolocation Api

🐤 In one of my projects, there was a task to get Trial information from api
which created by php.

🌐 The Trial information includes a lot of locations for each Trial around the world, I need to find the closest location to the user local area
based on those different locations and display them.

This are my solution Steps: 👇

- First, I created a function as a custom hook to calculate the distance with latitude and longitude.

```jsx
export function distance(lat1, lon1, lat2, lon2, unit) {
	const radlat1 = (Math.PI * lat1) / 180;
	const radlat2 = (Math.PI * lat2) / 180;
	const theta = lon1 - lon2;
	const radtheta = (Math.PI * theta) / 180;
	let dist =
		Math.sin(radlat1) * Math.sin(radlat2) +
		Math.cos(radlat1) * Math.cos(radlat2) * Math.cos(radtheta);

	if (dist > 1) {
		dist = 1;
	}
	dist = Math.acos(dist);
	dist = (dist * 180) / Math.PI;
	dist = dist * 60 * 1.1515;
	if (unit === 'K') {
		dist *= 1.609344;
	}
	if (unit === 'N') {
		dist *= 0.8684;
	}
	return dist;
}
```

- Second, import this custom hook in the component

```jsx
import { distance } from 'hooks/useLocationDistance.js';
```

- Within this component

1. 🐝 get Data from Api

```jsx
// get single Trial object from api
useEffect(() => {
	async function fetchTrial() {
		const response = await fetch(`.../api/${mockId}`);
		const jsonData = await response.json();
		setTrialDetail(jsonData);
	}
	fetchTrial();
	getFinalTrial();
}, [mockId]);
```

2. 🐝 get current user position using `geolocation api`

```jsx
useEffect(() => {
	if (!navigator.geolocation) {
		alert('Geolocation is not supported by your browser');
	} else {
		navigator.geolocation.getCurrentPosition((position) => {
			setLocationPosition({
				...position,
				defaultLatitude: position.coords.latitude,
				defaultLongitude: position.coords.longitude,
			});
		});
	}
}, []);
```

3. 🐝 use the custom hook, calculate distance to each location

```jsx
// get closest final object:
// locationTotal is the length of Location, only if it's not empty
const getFinalTrial = () => {
	if (trialDetail && locationTotal >= 1) {
		const userLatitude = trialDetail.locations?.map((el) => el.latitude);
		const userLongitude = trialDetail.locations?.map((el) => el.longitude);
		const distanceArray = userLatitude.map((lat, idx) => {
			const log = userLongitude[idx];
			return distance(
				locationPosition.defaultLatitude,
				locationPosition.defaultLongitude,
				lat,
				log,
			);
		});

		// Above returns an Array, then find the shortest distance, and get the index of this distance
		// display this index value from Trial object
		const closest = Math.min(...distanceArray);
		const closestLocationIndex = distanceArray.indexOf(closest);
		return trialDetail.locations[closestLocationIndex];
	}
	return {};
};

// Call the function above and update each list information, then display them in  `return`...
useEffect(() => {
	const finalLocationInfo = getFinalTrial();

	setGetInTouchInfo({
		...finalLocationInfo,
		locationAdress: `${finalLocationInfo.city},
${finalLocationInfo.state_province},
${finalLocationInfo.country}`,

		recruitmentStatus: finalLocationInfo.recruitment_status,
		organisationAdress: finalLocationInfo.name,
	});
}, [getFinalTrial]);

return (...)
```
