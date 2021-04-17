# Add \_redirects file

In a redirect, the browser first attempts to visit a URL at, say, netlify.com/features/forms but on arrival is instructed to visit another URL netlify.com/docs/forms instead. A redirect is an explicit instruction by the server to find a specific resource elsewhere.

In one of my React Projects I was facing the refreshing problem with React-router urls after deployed on `netlify`, one page was loading successfully, but after refresh, it returns 404:

So add a `_redirects` file to `publish` directory with will solve the problem

```jsx
 /* /index.html 200
```
