# Print Page with @media

With `@media print`, all definitions relevant for printing are summarized.

With `display`: you can hide elements that are not required on a printout, for example forms, but also entire areas, such as search or navigation.

Im my case, I had 2 versions (mobile / desktop) which are dynamically rendered regarding to the screen size, see below👇, both are inside the `<Container>`, the mobile version has all the components inside Accordions

```jsx
// desktop version
<Container
  size="md"
  className={classNames(styles.pageDesktop, styles.visibleDesktop)}
 ><div className={styles.content}>...</div></Container>

// mobile version
<Container
  size="md"
  className={classNames(styles.pageMobile, styles.visibleMobile)}
 ><Accordion>...</Accordion></Container>
```

I have a Print button on this page which prints both version, but if I only want to print the desktop version, I did this 👇

```jsx
@media print {
  @page {
    size: 330mm 427mm;
  }
  #root {
    width: 100%;
  }

  // print visibility regarding to the className `visibleMobile` from the Component
  .visibleMobile {
    display: none;
  }
  .visibleDesktop {
    display: block;
  }

  // define some special fonts, spaces ...
  .content {
    margin-bottom: 50px;
    font-size: 15px;
  }
  ...
}
```

🌈 When printing web pages, one of the most important features of `hypertext` is lost - the `linking`. With generated content, however, it is possible to visibly display the `href` attribute, which contains the link target:

```jsx
a[href]::after {
  content: " <"attr(href)">";
  color: #fff;
  background-color: yellow;
  size: 80%;
  ...
}
```

👆 The content of this attribute is appended to all elements `a`, which have an attribute `href`, after a space and an angle bracket. A closing angle bracket is inserted after the attribute value. The remaining definitions correspond to those of this and can be freely varied.
