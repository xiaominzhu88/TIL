# classNames in React

The `classNames` function takes any number of arguments which can be a string or object. The argument 'foo' is short for { foo: true }. If the value associated with a given key is falsy, that key won't be included in the output.

```jsx
classNames('foo', 'bar'); // => 'foo bar'
classNames('foo', { bar: true }); // => 'foo bar'
classNames({ 'foo-bar': true }); // => 'foo-bar'
classNames({ 'foo-bar': false }); // => ''
classNames({ foo: true }, { bar: true }); // => 'foo bar'
classNames({ foo: true, bar: true }); // => 'foo bar'

// lots of arguments of various types
classNames('foo', { bar: true, duck: false }, 'baz', { quux: true }); // => 'foo bar baz quux'

// other falsy values are just ignored
classNames(null, false, 'bar', undefined, 0, 1, { baz: null }, ''); // => 'bar 1'
```

### Dynamic class names with ES2015

```jsx
let buttonType = 'primary';
classNames({ [`btn-${buttonType}`]: true });
```

React Code Example:

```jsx
import React, { useState } from 'react';
import styles from './styles.css'; // scss
import classNames from 'classnames';

export default function MyComponent({ className }) {
	const [show, setShow] = useState(false);
	return (
		<div>
			{['red', 'yellow', 'blue'].map((buttonColor) => (
				<button
					className={classNames(
						className,
						{ [styles.`btn-${buttonColor}`]: show },
						'global-container',
					)}
					onClick={() => setShow((show) => !show)}
				>
					Button {buttonColor}
				</button>
			))}
		</div>
	);
}
```
