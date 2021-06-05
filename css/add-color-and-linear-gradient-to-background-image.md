# Add color and linear-gradient to background-image

☄️ Implementing responsive background-image is very simple, but combining it with `background-color` and `linear-gradient` is not as simple as imagined, and if you also have to make the backgound-image light and transparent, but the text on it should not be transparent ...

It should look like below in my project Task: 👇

**mobile version**: 📲

<img src='./image/bgImage1.png' height='150px'/>

**desktop version**: 🖥

<img src='./image/bgImage2.png' />

My solution: 🤞

```jsx
// component
<Container size="full">
	<div className={styles.heroImageWrapper}>
		<div className={styles.heroText}>
			Find a Clinical Trial that fits your Spinal Cord Injury
		</div>
	</div>
	<div className={styles.heroImageMobileWrapper}>
		<div className={styles.heroMobileText}>
			Find a Clinical Trial that fits your Spinal Cord Injury
		</div>
	</div>
</Container>
```

```jsx
@import 'assets/styles/variables';

// desktop version
.heroImageWrapper {
  display: none;

  @include media-breakpoint-up(sm) {
    display: block;
    position: relative;

    // width and height are important
    height: 490px;
    width: 100%;
    border: 1px solid #616161;
    opacity: 0.92;

    // multiple backgrounds
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
    background-image: linear-gradient(
    90deg,
    #cde1f1,
    rgba(201, 222, 237, 0.8) 36.47%,
    rgba(201, 222, 238, 0) 40.95%
    ),
    url('../../assets/hero.svg');

  // here comes container background-color with opacity
    &::before {
      content: '';

      background: #3c99DC;
      opacity: 0.2;
      position: absolute;
      width: 100%;
      height: 100%;
      left: 0;
      top: 0;
      border: 1px solid #616161;
    }
}

.heroText {
    position: absolute;

    @include media-breakpoint-up(sm) {
      font-weight: bold;
      letter-spacing: -0.01em;
      color: #15004F;
      font-size: font-size(xxl);
      left: 5%;
      top: rem(95px);
      width: rem(250px);
      height: rem(132px);
    }

    @include media-breakpoint-up(lg) {
      left: 5%;
      width: rem(360px);
      font-size: rem(32px);
      line-height: rem(44px);
    }
    @include media-breakpoint-up(xl) {
      left: 8%;
    }
  }
}

 // mobile version
.heroImageMobileWrapper {
position: relative;
height: 312px;
background-size: 100% 100%;
background-position: center;
background-repeat: no-repeat;
background-image: linear-gradient(
360deg,
#fff,
rgba(255, 255, 255, 0.7) 42.36%,
rgba(255, 255, 255, 0) 56.86%
),
url('../../assets/hero_mobile.svg');
opacity: 0.9;

&::before {
content: '';
background: #3c99DC;
position: absolute;
width: 100vw;
height: 312px;
opacity: 0.2;
}
@include media-breakpoint-up(sm) {
display: none;
}
.heroMobileText {
position: absolute;
bottom: space('250');
width: 100%;
padding: 0 space('100');
font-weight: bold;
font-size: rem(20px);
line-height: rem(28px);
text-align: center;
color:  #15004F;
}
@include media-breakpoint-up(md) {
display: none;
}
}
```
