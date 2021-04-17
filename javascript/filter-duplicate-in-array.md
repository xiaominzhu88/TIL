# Filter Duplicate in Array

Code Example:

```jsx
const array = [1, 2, 3, 2, 1, true, true, false, 'Ratul', 1, 5];
const filtered**array = [...new Set(array)];
console.log(filtered**array) // [ 1, 2, 3, true, false, 'Ratul', 5 ]
```
