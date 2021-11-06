# Using Gatsby navigate to link pages and send data

🦋 For internal navigation, Gatsby includes a built-in **Link** component for creating links between internal pages as well as a **navigate function** for programmatic navigation.

<hr />

How to use Link component is quite easy, but:

🌟 If you need to navigate to pages programmatically, such as during form submissions. In these cases, **Link** won’t work.

<hr />

Hier are some Steps how to use navigate function:

- First, import **navigate** 🥇

```jsx
import { navigate } from 'gatsby';
```

- Second, example with form submit: 🥈

```jsx
// form submit using Reakit library => Form
... some other code
onSubmit: async (values, errors) => {
      const requestValues = { ...values, role: values.role };
      try {
// api patch request
      await Client.userUpdate.patch(requestValues.userData.id, requestValues);
// if success, then link to page 2
      navigate(`/user/page2`);
      } catch (e) {
        throw errors;
      }
    },
```

- Another example, sending data between Pages: 🥉

```jsx
const handleClick = row => () => {
  const userData = tableRowsData.find(user => user.id === row.original.id);
// Page 1 link to page 2, and send user data using "state" :
  navigate(`/page2/${row.original.id}`, {
state: { userData, userRoles },
});
};

// Then you can access the data at page 2 with "window.history.state"
// Be sure that window is not undefined
const userRoles = typeof window !== 'undefined' && window.history.state;
const form = useFormState({
values: {
...userRoles,
first_name: '',
last_name: '',
email: '',
role: '',
},
onValidate: values => ...
... other codes
```
