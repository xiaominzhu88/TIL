# Access Env Value In create-react-app

Access environment variables in create-react-app
code using `process.env`.

⛑ There are a couple built-in environment variables, such as `NODE_ENV`.
Anything custom that you want to provide must be prepended with
`REACT_APP_`. If it isn't, that environment variable will be ignored with no
warning.

Code Example:

```jsx
const my_api_key = process.env.REACT_APP_MY_API_KEY;
```

```jsx
REACT_APP_MY_API_KEY="abcdefg1234567"
yarn start
```
