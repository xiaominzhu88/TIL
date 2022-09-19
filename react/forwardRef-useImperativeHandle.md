# React Hooks: forwardRef and useImperativeHandle

- ## forwardRef to react child component

Use the <span style="color:yellow">useRef()</span> hook to create a ref which returns a mutable object with a current property set to the initial value we passed to the hook, and use it on the DOM element for example **input**:

```jsx
const inputRef = useRef(null);

<input ref={inputRef} type=”text” />

inputRef.current.focus() => focus input
```

By default, refs only work in a native _html_ element, regular function or class components don’t receive the ref argument, and ref is not available in _props_ either.

We need to pass our InputWrapper into forwardRef, which receives props and the refs passed to the functional component and returns the JSX.Element for it.

```jsx
const App = () => {
  ...
	return <InputWrapper ref={...}/>;
};
const InputWrapper = forwardRef((props, ref) => {…})
```

- By doing this we are telling React that this component can take in a ref and the second parameter to InputWrapper will be the ref that is passed in.

🔴 The second ref argument only exists when we define a component with forwardRef call.

<hr />

- ## forward multiple refs ( modify parent ref by passing the reference )
<div style='color:yellow; font-size:16px' >1. create refs and pass them in an object and then use the same logic as forwardRef above.</div>

```jsx
// parent
const videoRef = useRef();
const focusRef = useRef();

// 👇 pass refs
 <VideoWrapper ref={{ videoRef, focusRef }}>
```

```jsx
// child
// 👇 destructure refs
const { videoRef, focusRef } = ref;
<video
  ref={videoRef}
  ...
/>
<input ref={focusRef} ... />
```

<div style='color:yellow; font-size:16px' >2. useImperativeHandle</div>

```jsx
// parent
const ref = useRef(null);
// 👇 exposed method from child
const handlePlay = () => {
    ref.current.playVideo();
    ref.current.focusThisInput();
  };
// 👇 pass ref
<VideoWrapper ref={ref}>
```

```jsx
// child
const videoRef = useRef();
const inputRef = useRef();

// 👇 call them whatever you like: playVideo, pauseMe, focusThisInput...
useImperativeHandle(ref, () => ({
         playVideo: () => {
             videoRef.current.play();
       },
         pauseMe: () => {
             videoRef.current.pause();
       },
         focusThisInput: () => {
             inputRef.current.focus();
       }
   }),[]);

    <video
      ref={videoRef}
      ...
    />
    <input ref={inputRef} .../>

```

Code above means: adding the methods inside of the _useImperativeHandle_ hook, and then they will be exposed and usable by its parent. 🙌
