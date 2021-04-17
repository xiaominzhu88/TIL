# Add FontAwesome Fab Icons

- Install

```jsx
yarn add @fortawesome/fontawesome-svg-core
yarn add @fortawesome/free-solid-svg-icons
yarn add @fortawesome/react-fontawesome

// ...solid, brands, regular.....
```

Code Example

```jsx
// Light:
<FontAwesomeIcon icon={["fal", "coffee"]} />
// Regular:
<FontAwesomeIcon icon={["far", "coffee"]} />
// Solid
<FontAwesomeIcon icon={["fas", "coffee"]} />
// ...or, omit as FontAwesome defaults to solid, so no need to prefix:
<FontAwesomeIcon icon="coffee" />
// Brand:
<FontAwesomeIcon icon={["fab", "github"]} />
```
