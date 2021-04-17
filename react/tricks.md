# React Tricks

## 1. React can assign keys to your children, no need to think of creative ways to come up with them

from

```jsx
{someData.map(item => <div key={item.id}>Hello!</div>}
```

to

```jsx
{React.Children.toArray(someData.map(item => <div>Hello!</div>)}
```

## 2. Fragment shorthand

```jsx
// Long
<React.Fragment></React.Fragment>
// Short
<></>
```

## 3. Keep components small

## 4. Omitting a prop value defaults to true

The React documentation shows that both lines below pass the autocomplete prop as true.

```jsx
<MyTextBox autocomplete />

<MyTextBox autocomplete={true} />
```

## 5. Keep your prop names simple

## 6. Keep your logic out of your JSX

If you’ve got some logic going on in your JSX, whether it is a callback or the rendering of some elements, defining a separate function can go a long way for readability.

```jsx
// Headache later, polluted with logic
<input
	onClick={(event) => {
		// Some logic here
	}}
/>;

// No headache later, easy to find and follow
const handler = (event) => {
	// Some logic here
};
<input onClick={handler} />;
```

## 7. Functional components can be called as functions

😅 This is certainly a trick and one that fellow developers might hate you for if you use it in a public project.This strictly applies to functional components.

```jsx
<SomeComponent/> => SomeComponent()
```
