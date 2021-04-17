# useEffect Fetch Example

```jsx
useEffect(()=> {
fetch('https://....')
.then(res=> res.json())
.then(res => setState(...))
.catch(err=>console.error(err))

return <div>{JSON.stringify(...)}</div>

}, [])
```
