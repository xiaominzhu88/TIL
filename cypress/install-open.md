# Install and Open Cypress

Install:

```jsx
$ npm install cypress
//
$ yarn add cypress
```

Open:

```jsx
yarn run cypress open
```

👗 Adding npm scripts

It's much easier and clearer to add Cypress commands to the scripts field in package.json file.

```bash
{
  "scripts": {
    "cypress:open": "cypress open"
  }
}
```

Now you can invoke the command from project root:

```bash
npm run cypress:open
```
