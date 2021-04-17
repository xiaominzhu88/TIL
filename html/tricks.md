# HTML Tricks Nobody is Talking About

- Lazy loading image, the image is loaded when the user scrolls and the image becomes visible otherwise, it is not loaded.

```jsx
<img src="image.png" loading="lazy" alt="…" width="200" height="200">
```

- Input suggestions, show a set of pre-defined suggestions, using the `<datalist>` tag.
  👆 Remember that this `tag’s ID` attribute must be the same as the `input fields list attribute`.

```jsx
<label for="country">Choose your country:</label>
<input list="countries" name="country" id="country">

<datalist id="countries">
  <option value="UK">
  <option value="Germany">
  <option value="USA">
  <option value="Japan">
  <option value="India">
</datalist>
```

- Picture tag allowing you to add multiple images fitting different widths instead of having a single one scale up and down.

```jsx
<picture>
  <source media="(min-width:768px)" srcset="med_flag.jpg">
  <source media="(min-width:495px)" srcset="small_flower.jpg">
  <img src="high_flag.jpg" alt="Flags" style="width:auto;">
</picture>
```

- Base URL, when you have a lot of anchor tags redirecting to a certain URL and all the URLs start with the same base address.

```jsx
<head>
  <base href="https://www.twitter.com/" target="_blank">
</head>

<body>
<img src="elonmusk" alt="Elon Musk">
<a href="BillGates">Bill Gate</a>
</body>

✅ The code will generate an image redirecting to `https://www.twitter.com/elonmusk` and an anchor tag redirecting to `https://www.twitter.com/billgates`.
The `<base>` tag must have either “href” or a target attribute present.
```
