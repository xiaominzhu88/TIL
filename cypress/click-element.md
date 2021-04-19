# Cypress Clicks Failing with "Detached from DOM" Errors

You may run into issues where the .click() calls in your Cypress tests fail, giving you errors about elements being "detached from the DOM":

```jsx
... failed because this element is detached from the DOM
```

Try changing your click to include .should('be.visible') before the .click(), like this:

```jsx
cy.get('[data-cy="buy-button"]').should('be.visible').click();
```

🎨 In my react working projects, I like to add e.g `data-purpose="element"` in React components (e.g in a div) for cypress
and in `cypress _spec files` define

```jsx
const selectors = {
  element1: "div[data-purpose='element']",
  element2: "a[data-purpose='element']",
  ...};

cy.get(selectors.element2).should('be.visible').click();

cy.get(selectors.element1).should('be.visible').children().should('have.length', 2);
// ...
```
