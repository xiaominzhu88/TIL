# URL Parameters with React-router-dom

Params are placeholders in the URL that begin with a colon, like the `:id` param defined in
the route.

```jsx
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link,
  useParams
} from "react-router-dom";

export default function ParamsExample() {
  return (
    <Router>
      <div>
        <ul>
          <li>
            <Link to="/netflix">Netflix</Link>
          </li>
           <li>
            <Link to="/astro">Astro</Link>
          </li>
        </ul>

        <Switch>
          <Route path="/:astroId" children={<Child />} />
        </Switch>
      </div>
    </Router>
  );

  function Child() {
  // `useParams` hook here to access
  // the dynamic pieces of the URL.
  let { id } = useParams();

  return (
    <div>
      <h3>ID: {id}</h3>
    </div>
  );
}
```
