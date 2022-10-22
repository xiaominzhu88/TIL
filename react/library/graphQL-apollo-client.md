# GraphQL Queries and Apollo Client

GraphQL is a data-oriented API query style, it was developed by Facebook as a solution to get data more efficiently.

Apollo Client is a comprehensive state management library for JavaScript that enables us to manage both local and remote data with GraphQL. 👉🏼Easier explained: frontend sends the GraphQL query to the Apollo Client, which processes the query and requests data from the GraphQL server, the server then sends the data back to the Apollo client which then stores and normalizes the data, finally the frontend receives the updates.

The traditional REST API has limitations of overfetching or underfetching. For example, if the endpoint holds data on a user, we may hit the /user endpoint, and instead of only getting the name that we are interested in, we may get everything that endpoint has to offer - including age, title, address, etc., so it’s very difficult to design the API in a way that it’s able to provide clients with their exact data needs.

With GraphQL, we have the ability to dictate exactly what we need from the server, and receive that data in a predictable way. GraphQL also gives API maintainers the flexibility to add or drop fields without affecting existing queries, developers can create APIs using any method.

[My codesandbox with GraphQL and Apollo Client](https://codesandbox.io/s/relaxed-fast-v1okx9?file=/src/hooks/useSingleCharacter.js)

Rick and Morty API to fetch and display some characters, and show individual character by clicking on each picture. 👇🏼

<img src='../image/graph1.png' alt='characters'>

all Characters

<img src='../image/graph2.png' alt='character'>

one Character

<hr />

## Setup

- Install the following packages

```jsx
npm install @apollo/client graphql
```

👉@apollo/client: Contains virtually everything you need to set up Apollo Client. It includes the in-memory cache, local state management, error handling, and a React-based view layer.

👉graphql: Provides logic for parsing GraphQL queries.
Then, initialize ApolloClient, import the symbols we need from @apollo/client

```jsx
// index.js
import { ApolloClient, InMemoryCache, ApolloProvider } from “@apollo/client";
```

- Passing its constructor a configuration object with the uri and cache fields

```jsx
const client = new ApolloClient({
    uri: “https://rickandmortyapi.com/graphql",
    cache: new InMemoryCache()
});
```

👉 uri specifies the URL of GraphQL server.

👉 cache is an instance of InMemoryCache, which Apollo Client uses to cache query results after fetching them.

- Connect the Apollo Client to React App with the ApolloProvider

ApolloProvider is similar to React’s Context.Provider. It wraps React app and places the client in context, which allows us to access it from anywhere in component tree.

```jsx
root.render(
  <StrictMode>
    <ApolloProvider client = {client}>
      <App />
    </ApolloProvider>
  </StrictMode>
```

- Create components

```jsx
// characters
const Characters = () => {
...// some data
return (
  <div>
    {data.map(({ ... }) => {
      return (
        <div key={id}>
        <img src={...} alt={...} />
        <p>{...}</p>
        </div>
        )})}
  </div>
)}
export default Characters;

// single character
const Character = () => {
...// some single data
return (
  <div>
    <h2>{...}</h2>
    <img src={...} alt={...} />
    <p>Gender: {...}</p>
    <p>Status: {...}</p>
    <p>Species: {...} </p>
    <p>Location: {...}</p>
  </div>
)};
export default Character;
```

<hr />

### Add the functionality that retrieves data!

To fetch characters from the server, we need to write queries that request the exact fields that we want, in our case, we expect images and names to be displayed by default.

- Create custom Hook: useCharacters: src/hooks/useCharacters.js, here we’ll be writing a query with GraphQL

```jsx
import { useQuery, gql } from '@apollo/client';

const GET_CHARACTERS = gql`
	query GetCharacters {
		characters {
			results {
				id
				name
				image
			}
		}
	}
`;

// export custom hook
// executing a query
export const useCharacters = () => {
	const { loading, error, data } = useQuery(GET_CHARACTERS);
	return { error, data, loading };
};
```

The code above means:

- We create a GraphQL query named GetCharacters, wrap it in the gql function and assigned them with a variable GET_CHARACTERS

- The useQuery Hook is the primary API for executing queries in an Apollo application. To run a query, call useQuery and pass it a GraphQL query string ( in our case: GET_CHARACTERS ).

- When our component renders, useQuery returns an object from Apollo Client that contains loading, error, and data properties we can use to render our UI.

That’s it, now move to Characters.js and import custom Hook and retrieve response, let’s update the Characters component:

```jsx
import { useCharacters } from '../hooks/useCharacters';
const Characters = () => {
	const { loading, error, data } = useCharacters();
	if (loading) return <p>Loading...</p>;
	if (error) return <p>Error :(</p>;
	return (
		<>
			{data?.characters.results.map(({ id, name, image }) => {
				return (
					<div key={id}>
						<img src={image} alt={name} />
						<p>{name}</p>
					</div>
				);
			})}
		</>
	);
};
export default Characters;
```

\*As our query executes and the values of loading, error, and data change, the Characters component can intelligently render different UI elements according to the query's state:

As long as loading is true (e.g query is still in flight), the component presents Loading....
When loading is false and there is no error, the query has completed.
The component renders characters returned by the server.

<hr />

We can do the same logic with our single Character component, create a query, get everything we need

```jsx
// custom Hook useSingleCharacter
import { useQuery, gql } from '@apollo/client';
const GET_CHARACTER = gql`
	query GetCharacter($characterId: ID!) {
		character(id: $characterId) {
			name
			image
			gender
			status
			species
			location {
				name
			}
		}
	}
`;
export const useSingleCharacter = (characterId) => {
	const { loading, error, data } = useQuery(GET_CHARACTER, {
		variables: { characterId },
	});
	return { error, data, loading };
};
```

🍎 The query operation above uses a name GetCharacter with one argument. This argument has a '$characterId' variable, with a type of ID. The '!' means that this operation is required, GraphQL won’t execute the operation unless we pass a characterId variable whose type is ID.

\*GraphQL’s default scalar types are:

- Int: A signed 32‐bit integer

- Float: A signed double-precision floating-point value

- String: A UTF‐8 character sequence

- Boolean: true or false

- ID (serialized as a String): A unique identifier that's often used to refetch an object or as the key for a cache. Although it's serialized as a String, an ID is not intended to be human‐readable.

Note that we’re providing a configuration option (variables) to the useQuery hook this time 👇

```jsx
variables: { characterId },
```

This variables option is an object that contains all of the variables we want to pass to our GraphQL query, in our case, we want to pass the currently selected characterId, and this happens inside single Character component with the Hook execution.

Now, let’s update our Character.js

```jsx
import { useSingleCharacter } from “../hooks/useSingleCharacter”;

const Character = () => {
  const characterId = 1; // fake id
  const { loading, error, data } = useSingleCharacter(characterId);
  if (loading) return <p>Loading…</p>;
  if (error) return <p>Error ...</p>;
  const {name, image, gender, status, location, species} = data.character; // destructure data
  return (
    <>
      <h2>{name}</h2>
      <img src={image} alt={name} />
      <p>Gender: {gender}</p>
      <p>Status: {status}</p>
      <p>Species: {species} </p>
      <p>Location: {location.name}</p>
      <Link to={“/”}>
      <span role=”img” aria-label=”back”>⏪</span>
      </Link>
    </>
)};
export default Character;
```

Note that we’re using a fake "characterId = 1" here for now, since this single Character component will be displayed by clicking on the image ( which is inside Characters.js ), we’ll implement this soon.

Last step, let’s realize the interaction of the two components by clicking the image, we will use react-router, first update our index.js file 👇🏼

```jsx
...// same
import { BrowserRouter, Routes, Route } from “react-router-dom”;
import App from “./App”;
import Character from “./components/Character”;
const rootElement = ...;
const root = ...;
const client = new ApolloClient(...);
root.render(
<StrictMode>
<ApolloProvider client={client}>
<BrowserRouter>
<Routes>
<Route path=”/” element={<App />} />
<Route path=”character/:characterId”
element={<Character />} />
</Routes>
</BrowserRouter>
</ApolloProvider>
</StrictMode>
);
```

\*if we navigate to "/character/1” we should see the full information about character 1, the data comes from our useSingleCharacter Hook 👐🏼

Then, let’s implement the clickable image with real characterId, we just need to wrap the image inside Link ( react-router )

```jsx
// Characters.js
// same ...

<Link to={`character/${id}`}>
	<img src={image} alt={name} />
</Link>
```

Last step, update Character.js, use real characterId instead of fake id before

```jsx
// use useParams from react-router to get CharacterId
import { useParams } from 'react-router-dom';
const { characterId } = useParams();
const { loading, error, data } = useSingleCharacter(characterId);
```

Summarize the steps above:

- create components
- consume GraphQL API and request data with queries within the React custom Hooks
- execute hooks from components and get data response, use fake id for quick testing
  define client side routing with react-router, realize the interaction of the two components
- use useParams from react-router and get the CharacterId
- use dynamic CharacterId and complete our App
