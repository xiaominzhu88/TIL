# Use gatsby-transformer-json plug-in and useStaticQuery

Use gatsby-transformer-json to read data from a local JSON file and render in React component

- add gatsby-transformer-json

```jsx
yarn add gatsby-transformer-json
```

- add this in gatsby-config.js file

```jsx
Config file: 'gatsby-transformer-json',
{

      resolve: 'gatsby-source-filesystem',

      options: {

        name: 'data',

        path: `${__dirname}/data`, // path to the JSON file

      },

    }
```

- Create sidebar.json at `src/data` similar like below:

```jsx
[
  {
    "id":1,
    "title":"first title",
    "content":"this is the first content
  },
   {
    "id":2,
    "title":"second title",
    "content":"this is the second content
  }
]
```

- Create a testPage in src/pages

```jsx
import TestComponent from 'components/TestComponent/TestComponent.js';
import React from 'react';

const TestPage = () => {
	return (
		<div>
			<TestComponent />
		</div>
	);
};

export default TestPage;
```

- Create a TestComponent at `src/components`

```jsx
import React from 'react';
import { useStaticQuery, graphql } from 'gatsby';

const TestComponent = () => {
	const data = useStaticQuery(graphql`
		query SidebarQuery {
			allSidebarJson {
				edges {
					node {
						title
						content
					}
				}
			}
		}
	`);
	// console.log({ data });

	// data should look like this
	// allSidebarJson:
	// edges: Array(2)
	// 0: {node: {…}}
	// 1: {node: {…}}
	// length: 2
	// **proto**: Array(0)
	// **proto**: Object
	//

	return (
		<>
			<ul>
				{data.allSidebarJson.edges.map((edge) => (
					<ul key={edge.id}>
						<li>{edge.node.title}</li>
						<li>{edge.node.content}</li>
					</ul>
				))}
			</ul>
		</>
	);
};

export default TestComponent;
```

⛔️ In gatsby v1 you could only fetch data at the page level, and use it as props, but now in v3, you can fetch Data at the Component level with `useStaticQuery`
