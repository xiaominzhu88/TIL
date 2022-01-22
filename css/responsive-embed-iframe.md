# Create Responsive iframe Embed in a React Way

*Surprisingly, YouTube does not have responsive embed code*🦄

In a project I’m recently working on, some videos are embedded on the website from YouTube, since our website is fully responsive, I also need them to be responsive on desktop or mobile screens.

However, when I added the embed code, no matter how I resize the screen, the video iframe always stays the same! 💥

**The reason is that iframe can’t keep its ratio by itself since the domain is a third party ( e.g YouTube… ), you are not allowed to know the content of the iframe for security and privacy reasons. 🧚**

<hr />

To solve this, below are the example steps:

☘️ First, create a simple React Component named **Video**, \**how to find the embed URL on YouTube*👇

- Go to YouTube.
- Navigate to the video you wish to embed.
- Click the **Share** link below the video, then click the Embed link.
- The embed URL is in the **src** attribute, you just need to copy and paste it as your **embedUrl** ( example below )

```jsx
const Video = () => {
	const embedUrl = 'https://......';
	return (
		// a div will be added hier, explained below by second step
		<iframe
			src={embedUrl}
			allow="autoplay"
			title="..."
			className="iframe"
			allowFullScreen
			frameBorder="0"
		/>
	);
};
```

☘️ Second, to make the full-width iframe, make a **div** that has a position **relative** and wraps this iframe.

```jsx
<div className='videoWrapper'>
```

☘️ Last step, to make the embed video responsive, just make it keeps the fix **aspect ratio (4:3, 16:9, etc.)** within the container ( videoWrapper in this case) which we added above, this means:

```jsx
.videoWrapper{
  position:relative;
  padding-bottom:56.25%;
  overflow:hidden;
  //... whatever you need, e.g breakpoint, margin ...
}
```

✏️ limit the container height to “56.25%” which is 16:9,
and in order to make it **full width**, do it like this:

- make iframe position absolute and **scale** to 100% in both width and height within the container

```jsx
.iframe{
  position:absolute;
  width:100%;
  height:100%;
  overflow:hidden;
  top:0;
  left:0;
  //... whatever you need, e.g breakpoint, margin ...
}
```

And that’s it 🌹! You can also add some breakpoints to adjust different views on mobile or desktops.

<hr />

👉 What is the aspect ratio?

- The aspect ratio of an element describes the proportional relationship between its width and its height. Two common video aspect ratios are 4:3 (the universal video format of the 20th century), and 16:9 (universal for HD television and European digital television, and for YouTube videos).
