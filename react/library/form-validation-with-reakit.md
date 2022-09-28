# Form validation with [Reakit](https://reakit.io/docs/get-started/)

🧚 Reakit is a lower level component library for building accessible high level UI libraries, design systems and applications with React.

`Form` is an accessible component with a collection of other components, such as `FormLabel` and `FormInput`.

Use case:

```jsx
import {
	unstable_useFormState as useFormState,
	unstable_Form as Form,
	unstable_FormLabel as FormLabel,
	unstable_FormInput as FormInput,
	unstable_FormMessage as FormMessage,
	unstable_FormSubmitButton as FormSubmitButton,
	unstable_FormCheckbox as FormCheckbox,
} from 'reakit/Form';
```

<img src='./image/validation1.png' width='150px'/>
<img src='./image/validation2.png' width='150px'/>
<img src='./image/validation3.png' width='150px'/>

Give the form state with `values` and `errors`

```jsx
const form = useFormState({
		values: { name: '', email: '', checked: false },
		onValidate: (values) => {
			if (!values.email && !values.name && !values.checked) {
				const errors = {
					email: 'Please enter your email!',
					name: 'Please enter your name!',
					checked: 'You must accept our conditions!',
				};
				throw errors;
			}
			if (!values.email && !values.name && values.checked) {
				const errors = {
					email: 'Please enter your email!',
					name: 'Please enter your name!',
				};
				throw errors;
			}
			if (!values.email && values.name) {
				const errors = {
					email: 'Please enter your email!',
				};
				throw errors;
			}
			if (values.email && !values.name) {
				const errors = {
					name: 'Please enter your name!',
				};
				throw errors;
			}
			if (!values.checked) {
				const errors = {
					checked: 'You must accept our conditions!',
				};
				throw errors;
			}
		},

		onSubmit: () => {},
	});
	console.log(form);
// errors:{email: "..."}
// submitSucceed: 1
// values:{ checked: false, email: "", name: "d"}
...
```

Use form state for the validation, `name` is important

```jsx
return (
	<div className="App">
		<Form {...form} className="form">
			<section className="formSection">
				<FormLabel {...form} name="name">
					Name
				</FormLabel>
				<FormInput {...form} name="name" placeholder="name" />
				<FormMessage {...form} name="name" className="errorMessage" />
			</section>

			<section className="formSection">
				<FormLabel {...form} name="email">
					Email
				</FormLabel>
				<FormInput {...form} name="email" placeholder="email" />
				<FormMessage {...form} name="email" className="errorMessage" />
			</section>

			<section className="checkSection">
				<FormCheckbox {...form} name="checked" className="checkbox" />
				<FormLabel {...form} name="checked">
					Accept conditions
				</FormLabel>
			</section>
			<FormMessage {...form} name="checked" className="errorMessage" />

			<FormSubmitButton className="submitButton" {...form}>
				Submit
			</FormSubmitButton>
			<br />
			{form.submitSucceed === 1 && <div className="dialog">🌟 Success!</div>}
		</Form>
	</div>
);
```
