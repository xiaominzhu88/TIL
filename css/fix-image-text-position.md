# Fix Image (left) and Text (right) position

The problem was that there is a container, inside it I had a large image on the left side and a text container with 3 `div`s on the right side, between all `div`s there are different distances (vertically). The aim is to align text and image (top and bottom).

Here's what I did which solved this problem:

```jsx
.bigImageWrapper {
  position: relative;
  display: block;
  height:100%;
  padding:0;
}
// big Image on the left side
.contentTextWrapper {
  position:absolute;
  bottom:0;
  width:100%;
  display:flex;
  flex-direction:column-reverse;
}
// text on the right side
```
