# Unreachable `.env` environment variables after deploy to Netlify

I had this issue and it took quite a while to figure out:

I could access my environment variables when running my react app locally (using yarn), but once I deployed it to Netlify I could not access them. ( I mean after inspect network, I noticed that my react app api-key was undefined 🕷 )

Here is what I did to solve it:

- Login to Netlify account and go to

```jsx
Sites > Your Site > Site Settings > Build & Deploy > Environment
```

- Set environment variables ( in my case: add `react_app_api_key` and `value` just like in the `.env` file )

- I added `dotenv-webpack` package with

```jsx
yarn add dotenv-webpack
```

- Created a `webpack.config.js` file ( root ) with

```jsx
const Dotenv = require('dotenv-webpack');
module.exports = {
	plugins: [new Dotenv()],
	systemvars: true,
};
```

🙈 Not sure about this, maybe there is a better way:

By default dotenv-webpack will not pick up properly set environment variables, only those defined `.env` files - so I added the `systemvars: true` setting so that `dotenv-webpack` pick up normal linux environment variables (the kind that are set in netlify build and similar environments).
