# Gatsby router / route

User Authentication example from one of my company project which based on Gatsby:

🦋 First create a store which contains user state in **pages/site/src/store.js**:

```jsx
import create from 'zustand';
import { persist } from 'zustand/middleware';

export const useStore = create(
	persist(
		(set) => ({
			user: null,
			setUser: (user) => set({ user }),
		}),
		{
			name: 'user',
		},
	),
);
```

🦋 Second create a PrivateRoute which contains user login modal logic in **src/pages/admin/components/PrivateRoute.js**
: ( user login modal ):

```jsx
import useStore from 'store';
import React, { useState, useEffect } from 'react';
import { navigate } from 'gatsby';

const PrivateRoute = ({ component: Component, location, ...rest }) => {
	const store = useStore();
	const [isLoginModalOpen, setIsLoginModalOpen] = useState(false);

	useEffect(() => {
		if (!store.user && location.pathname !== `/`) {
			setIsLoginModalOpen(true);
		}

		if (!store.user && location.pathname !== `/`) {
			navigate('/', { state: { isLoginModalOpen } });
		}
	});

	if (!store.user) {
		return null;
	}

	return <Component {...rest} />;
};

export default PrivateRoute;
```

🦋 Then just use it in **src/pages/admin/app.js**:

```jsx
import PrivateRoute from './components/PrivateRoute.js';
import AdminUsersList from './components/user/list/AdminUsersList.js';
import EditUser from './components/user/list/EditUser.js';
import TrialEdit from 'components/admin/trialEdit/trialEdit';
import TrialCompare from 'components/admin/trialEdit/trialCompare/trialCompare';
import React from 'react';
import { Router } from '@reach/router';

const App = () => {
	return (
		<Router basepath="/admin">
			<PrivateRoute path="/users/list" component={AdminUsersList} />
			<PrivateRoute path="/users/list/:id" component={EditUser} />
			<PrivateRoute path="/trials/:nct_id/edit" component={TrialEdit} />
			<PrivateRoute
				path="/trials/:nct_id/compare/:new_version/:old_version"
				component={TrialCompare}
			/>
		</Router>
	);
};
export default App;
```

<hr />
👉 Then, create components as you need ( e.g for AdminUsersList ):

```jsx
site / src / pages / admin / components / user / list / AdminUsersList.js;
```
