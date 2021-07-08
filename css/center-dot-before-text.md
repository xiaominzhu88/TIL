# Centering dot before text

In my current Project, I have to conditionally add a `dot` before some list items

🌟 Use `&middot;` for a dot or `&bull;` for a thicker dot

Usage: 👇

<p>&middot; Hello</p>
<p>&bull; World</p>

<hr />

🌟 For use in the `content` attribute, you'll need to escape it:

middot:

```jsx
content: ' B7 ';
```

bull:

```jsx
content: ' \2219 ';
```

Below is how I did in my Project ( mobile / desktop ):

```jsx
.imprintLinkItem {
  padding: space('100') 0;
  font-size: font-size(xs);

// add centered dot before each item
@include media-breakpoint-up(md) {
  font-size: font-size(sm);

    &::before {
    content: '\B7';
    margin-right: space('75');
    }
  }
}

// add centered dot before each item except first one on mobile
.imprintLinkItem:not(:nth-of-type(1)) {
  &::before {
    content: '\B7';
    margin-right: space('150');

    @include media-breakpoint-up(md) {
      margin-right: space('75');
    }
  }
}
//Ignore padding, marging font ... module
```

Result: 👇

Desktop:
<img src='image/centerDot1.png' alt="centerDot1" />

Mobile:
<img src='image/centerDot2.png' alt="centerDot2" />
