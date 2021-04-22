# TailwindCss with Laravel `width:fit-content`

In one of my projects I had to use css `width:fit-content` which present with `tailwindCss`, because I want that each `nav link` should have `focus`and `hover` underline with the same content width, without that, the underline will take the whole `div` width, if I only have one container which contains jetstream links, I have to wrapp several `div`s which looks ugly.

This is what I did with tailwindCss:

```jsx
w-auto  inline-block
```

It resolved that problem, but if this is on each `Link` element, and they will be present as `flex` look (inline), but they should have same space between and `block` display, to make this compact and save, I added to the `div` container:

```jsx
flex-col flex items-start
// dislay:flex;
// flex-direction: column;
// align-items: flex-start;
```

This makes a nice displayed `nav` on the left side with `block` layout, each item has an underline which takes the width from it's content 🤞

⛵️ Hope some day there will be `width:fit-content` with tailwindcss
