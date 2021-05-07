# Create a page with Gatsby

For my current project I have to use gatsby react(FR) with laravel(BE), SQL(DB), I'm not really used to work with gatsby, but after learn some basic, it becomes clearly a bit, I listed some steps:

- create new pages inside `src/pages`, pretty simple, any React component defined in `src/pages/*.js` will automatically become a page.

```jsx
Gatsby uses hot reloading to speed up development process, any time save a file, changes will be immediately reflected in the browser.
```

- create sub-components inside `src/components` folder and import them from pages, and play around with props 😸

- use `Link` component to link to the `intern` pages

🤖 The Gatsby `<Link />` component is for linking **between pages** within the site. For external links to pages not handled by your Gatsby site, use the regular HTML `<a>` tag.

```jsx
import { Link } from 'gatsby';

...
<Link to="/">Home</Link>;
...
```

- it is also possible to create pages programmatically in the `gatsby-node.js` file

\*\* In `gatsby-node.js`, add an export for `createPages`

\*\* Destructure the createPage action from the available actions so it can be called by itself, and add or get data

\*\* Loop through the data in `gatsby-node.js` and provide the `path, template`, and `context` (data that will be passed in the props pageContext) to createPage for each invocation

my project example:

```jsx
const glob = require('fast-glob');

const pages = glob.sync('./data/pages/**/*.json').map(file => {
  const test = require(path.resolve(file));
  return {...test, filePath:file.split('./')[1]}
})

exports.createPages = async ({ actions }) => {
  const { createPage } = actions;

  const doCreatePage = (slug, page) => {
    const { layout = null } = page;

    const pageTemplate = layout
      ? path.resolve(`src/templates/${layout}/${layout}.js`)
      : path.resolve(`src/templates/default/default.js`);

    createPage({
      path: slug,
      component: pageTemplate, // code example below
      context: {
        pagePath: slug,
        ...page,
      },
    });
  };

  pages.forEach(page => {
    const pageClean = {
      ...page,
    };
    doCreatePage(page.slug, pageClean);
  });
```

- The createPage action requires that you specify the component template that will be used to render the page.

\*\* 🖼 So, create a React component inside `src/components` to serve as the template for the page that was used in createPage

🍉 Below is my project Code example:

```jsx
// src/pages/user.js
import PageTemplate from 'templates/userPage/userPage';

export default PageTemplate;
```

```jsx
// src/templates/userPage.js
import Footer from 'components/Footer/Footer';
import styles from 'templates/userPage/userPage.module.scss';
import React from 'react';

const Page = () => {
	return (
		<div>
			<div className={styles.pageContainer}>
				<div className={styles.userPage}>
					<div>User Page</div>
				</div>
			</div>
			<div className={styles.footerContainer}>
				<Footer />
			</div>
		</div>
	);
};

export default Page;
```

☘️ When building with Gatsby, GraphQL is also a good choise. It declaratively express the data needs. This is done with `queries`, queries are the representation of the data needed.

```jsx
{
  site {
    siteMetadata {
      title
    }
  }
}
```

🍒 I'm still on learning this, to be continued ...
