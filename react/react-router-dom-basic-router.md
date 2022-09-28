# React-router-dom Basic Router

Code Example:

```jsx
import { BrowserRouter as Router, Switch, Route, Link } from 'react-router-dom';

// This site has 3 pages, all of which are rendered
// dynamically in the browser (not server rendered).

export default function BasicExample() {
	return (
		<Router>
			<div>
				<ul>
					<li>
						<Link to="/">Home</Link>
					</li>
					<li>
						<Link to="/about">About</Link>
					</li>
					<li>
						<Link to="/dashboard">Dashboard</Link>
					</li>
				</ul>

				<Switch>
					<Route exact path="/">
						<Home />
					</Route>
					<Route path="/about">
						<About />
					</Route>
					<Route path="/dashboard">
						<Dashboard />
					</Route>
				</Switch>
			</div>
		</Router>
		// A <Switch> looks through all its children <Route>
		// elements and renders the first one whose path
		// matches the current URL.

		// Use a <Switch> any time with multiple routes, only one
		// of them to render at a time
	);
}
```

```jsx
// Think of these components as "pages" in app

function Home() {
	return (
		<h2>Home</h2>
	);
}

function About() {
	return (
		<h2>About</h2>
	);
}

function Dashboard() {
	return (
		<h2>Dashboard</h2>
	);
}
```
