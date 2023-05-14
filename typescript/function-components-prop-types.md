# Function components prop types

These can be written as normal functions that take a props argument and return a JSX element.

```jsx
// Use `interface` if exporting so that consumers can extend
// Declaring type of props
type AppProps = {
	message: string,
};

// Easiest way to declare a Function Component; return type is inferred.
const App = ({ message }: AppProps) => <div>{message}</div>;

// you can choose annotate the return type so an error is raised if you accidentally return some other type
const App = ({ message }: AppProps): JSX.Element => <div>{message}</div>;

// you can also inline the type declaration; eliminates naming the prop types, but looks repetitive
const App = ({ message }: { message: string }) => <div>{message}</div>;
```

👉 React.FC is removed from Typescript template since [React 18 type updates](https://github.com/DefinitelyTyped/DefinitelyTyped/pull/56210)
