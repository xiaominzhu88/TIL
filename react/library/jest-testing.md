# Testing with Jest and React-Testing-Library

**Jest** is a JavaScript test runner that lets you access the DOM via jsdom, it is for running unit tests. Unit tests simply ensure that your methods return the expected value for different cases.

**React Testing Library** is a set of helpers that let you test React components without relying on their implementation details, it simulates user interactions on isolated components and asserts their outputs to ensure the UI is behaving correctly.

_React Testing Library is not specific to any testing framework, we can use it with any other testing library, we need to install Jest because React Testing Library only provides methods to help us write the test scripts, so we still need a JavaScript test framework to run the test code, Jest is recommended and preferred by many developers._

👉 [My Todo App codesandbox](https://codesandbox.io/s/todo-jest-react-zp3hhy?file=/src/App.js)

<hr />

## Install dependencies with a package manager

```jsx
npm install — save-dev jest
```

or

```jsx
yarn add — dev jest
```

\*projects created with create-react-app have out of the box support for React Testing Library, if that is not the case, you can add it like so:

```jsx
npm install — save-dev @testing-library/react
```

or

```jsx
yarn add — dev @testing-library/react
```

## Test 1: default Input is displayed correctly, user can type in the input field and the button is enabled from disabled

( input → Input.js / Input.test.js, listView → ListView.js/ ListView.test.js, etc. )

```jsx
// Input.test.js
import { render, screen } from '@testing-library/react';
import '@testing-library/jest-dom';
import Input from './Input';
import userEvent from '@testing-library/user-event';
// import { fireEvent } from "@testing-library/react";

describe('<Input />', () => {
	// block 1
	test('displays text input and disabled button by default', () => {
		render(<Input />);
		const userInput = screen.getByTestId('input-field');
		const addButton = screen.getByRole('button', { name: /add/i });

		expect(userInput).toBeInTheDocument();
		expect(userInput).toHaveAttribute('type', 'text');
		expect(addButton).toBeDisabled();
		expect(addButton).toHaveTextContent('add');
	});

	// block 2
	test('user should be able to type in the input field', async () => {
		const handleChange = jest.fn();
		render(<Input handleChange={handleChange} />);
		const userInput = screen.getByTestId('input-field');
		// fireEvent: Simulates a specified event, e.g input onChange
		// fireEvent.change(userInput, {target: { value: "apple" }});

		await userEvent.type(userInput, 'apple');
		expect(handleChange).toHaveBeenCalled();
		expect(userInput.value).toBe('apple');
	});

	// block 3
	test('button should be enabled with input value', async () => {
		const addTodo = jest.fn();
		render(<Input inputValue="apple" addTodo={addTodo} />);
		const addButton = screen.getByRole('button', { name: /add/i });

		//button enabled
		expect(addButton.disabled).toBeFalsy();
		await userEvent.click(addButton);
		expect(addTodo).toHaveBeenCalled();
	});
});
```

👉 The describe(name, callback) block is the test suite, and the test('...', () => {}) block (or simply test) is the test case. The describe block can have multiple test cases, but a test block doesn’t have to be in a describe block, at least one test block is required in each test file.

Run the tests using the following command:

```jsx
npm test
```

- test(name, callback): A test block accepts two required parameters: 1. a string representing the test case ( e.g displays something correctly ), 2. a function containing the test’s expectations.

- render(Component): React Testing Library provides a render method to render our component into the DOM. After the given component has been rendered into the test environment’s screen, we can start writing code to confirm the expected functionality.

- Screen: The React testing library provides a screen object as a convenient way to access the relevant queries needed to make assertions against the test DOM environment. ( const userInput = screen.getByTestId(“input-field”) ).

- getByTestId() and getByRole(): By default, React Testing Library provides queries that allow us to locate elements within the DOM, in this article, I will focus on the getBy\*query, which is the most common query type, it finds element by data-testid attribute, easier said, it is a shortcut to screen.querySelector(`[data-testid="${someId}"]`).

- expect(): The expect function (e.g expect(…).someMatcher() ) is used whenever we want to check a specific outcome result, most expect functions are coupled with a matcher function ( mostly provided by jest-dom ) to confirm something about a specific value. ( for example, .toBeInTheDocument is the matcher for the expect function in the first line, while getByTestId() and getByRole() are the selectors to get the DOM elements ).

```jsx
<input
        onChange={...}
        value={...}
        className="..."
        type="..."
        data-testid="input-field"
      />
```

```jsx
describe('<Input />', () => {
	test('user should be able to type in the input field', async () => {
		const handleChange = jest.fn();
		render(<Input handleChange={handleChange} />);
		const userInput = screen.getByTestId('input-field');

		// fireEvent: Simulates a specified event, e.g input onChange
		// fireEvent.change(userInput, {target: { value: "apple" }});

		await userEvent.type(userInput, 'apple');
		expect(handleChange).toHaveBeenCalled();
		expect(userInput.value).toBe('apple');
	});
});
```

In this block we test if the user can type in the input field, for that we could use fireEvent from DOM Testing Library and Jest Function Mocks.

'_jest.fn()_' acts as “spy” and lets us spy on the behavior of a function that is called indirectly by some other code, rather than just testing the output ( change, click … ), in our case we can create a mock function for user input with jest.fn() : handleChange callback handler 👇

```jsx
const handleChange = jest.fn();
```

🍄 Use userEvent instead of fireEvent: useEvent simulates complete interactions, and not only single events such as mouseOver(), focus(), change()…, there’s been issues with using fireEvent rather userEvent.

```jsx
// import { fireEvent } from "@testing-library/react";
// fireEvent: Simulates a specified event.
// fireEvent.change(userInput, {target: { value: "apple" }});
```

Now, type the string: “apple” into the input field, and expect the callback function handleChange has been called and “apple” should be in the input field.

```jsx
import userEvent from "@testing-library/user-event";
...// same
userEvent.type(userInput, "apple");
expect(handleChange).toHaveBeenCalled();
expect(userInput.value).toBe("apple");
```

The same logic plays here, we mock the function, render the component with some values, get the button and use Jest API toBeFalsy() to test if the button is enabled after the user input.

```jsx
test('button should be enabled with input value', async () => {
	// same ...
	const addTodo = jest.fn();
	render(<Input inputValue="apple" addTodo={addTodo} />);
	const addButton = screen.getByRole('button', { name: /add/i });

	//button enabled
	expect(addButton.disabled).toBeFalsy();
	await userEvent.click(addButton);
	expect(addTodo).toHaveBeenCalled();
});
```

👉 The reason that I use async-await is because the @testing-library/user-event at v13 didn't return a promise, but the update to v14 does. At the moment, create-react-app provides v13, so it doesn't match the latest documentation.

## Test 2: lists are displayed correctly

```jsx
// ListView.test.js
import { render, screen} from “@testing-library/react”;
import ListView from “./ListView”;
import “@testing-library/jest-dom”;
import userEvent from “@testing-library/user-event”;

describe(“<ListView />”, () => {
  test(“renders emoji by default”, () => {
    render(<ListView />);
      const emoji = screen.getAllByTestId(“emoji”);
      expect(emoji).toHaveLength(1); // default as array
})});
```

As with Input component, we first test that the 🍰 emoji is displayed by default since the user hasn’t added any todos. We use data-testid for each element to be tested in ListView.js.

```jsx
<span data-testid="list-view">{content}</span>
<button data-testid="remove-button">remove</button>
<span role="img" aria-label="cake" data-testid="emoji">🍰</span>
```

Then in the second test block we mock the removeTodo function, render the component with a todo list, grab the testid and test if the “apple” list is showing instead of emoji, then get the remove button and fire the callback function.

```jsx
test(“renders list correctly”, async () => {
  const removeTodo = jest.fn();
  render(<ListView todoList={[{ id: 1, content: “apple” }]} removeTodo={removeTodo} /> );

  const listView = screen.getAllByTestId(“list-view”);

  // displays list content apple
  expect(listView[0]).toHaveTextContent(“apple”);

  // remove list
  const removeButton = screen.getByRole("button", {name: /remove/i });
  await userEvent.click(removeButton);
  expect(removeTodo).toHaveBeenCalled();
})
```
