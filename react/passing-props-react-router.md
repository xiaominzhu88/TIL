# Passing Props Down To React-Router Route

When using [react-router](https://github.com/ReactTraining/react-router),
you'll often use the `component` prop to have a certain component rendered.

```jsx
<Route path="/my/path" component={MyComponent} />
```

If, however, need to pass props down into `MyComponent`, then use the `render` prop with an inline function.

```jsx
<Route
	path="/my/path"
	render={(routeProps) => <MyComponent {...routeProps} {...props} />}
/>
```

这两个扩展运算符语句必不可少。
