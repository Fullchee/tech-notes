[The Surprising Truth About Pixels and Accessibility: should I use pixels or rems?](https://www.joshwcomeau.com/css/surprising-truth-about-pixels-and-accessibility/)

[Video](https://courses.joshwcomeau.com/css-for-js/01-rendering-logic-1/05-padding#units-1)

## Ways to affect zooming
1. zooming (cmd +/-)
	1. increases the size of a pixel
	2. everything gets bigger (except viewport units)
2. font scaling
	1. browser/OS font size settings
	2. re-defines the baseline font size
	3. pixels ignore this
	4. rems take this into account


## Text

> [!Unit for text]-
> `rem` for text
> `em` will cascade
> - usually unexpectedly, especially in nested components

## Border/margin/padding

> [!Unit for border/margin/padding generally]-
> pixels
> 
> we want more words on the screen

> [!Why not percents for border/margin/padding]-
> `rem` and not pixels!
> always relative to the width!
> ```css
> /* top padding/margin will be 50% of the width */
> padding-top: 50%;
> ```
> on wider screens, the top/bottom padding would get larger
> - prob not desired


### Vertical margin

[Vertical Margins](https://www.joshwcomeau.com/css/surprising-truth-about-pixels-and-accessibility/#vertical-margins-8)

> [!Unit for vertical margin]-
> `rem` and not pixels!
> vertical margin is functional and not decorative

#### When would you ever use `em`?

sharing margin-top and bottom for headers

```css
h1 {
  font-size: 3rem;
}
h2 {
  font-size: 2rem;
}
h3 {
font-size: 1.5rem;
}
h1, h2, h3 {
  margin-top: 2em;
  margin-bottom: 0.5em;
}
```

## Media queries
[Josh Comeau: media query units](https://www.joshwcomeau.com/css/surprising-truth-about-pixels-and-accessibility/#media-queries-7)

> [!Unit for media queries]-
> `rem`
> think of media queries as available space
> 
> on a laptop, they may see the mobile layout
> 
> when they increase the default font size
> 
> they reduce the amount of available space
> 
> so they should get some optimizations
'


## Width/heights

you should use `max-width` and `min-height` to allow 

```css
.button {
  max-width: fit-content;
  min-height: 2rem;
}
```

> [!Units for width/height]-
> generally `rem` 
> 
> pixels if vertical margin is functional and not decorative


## Making `rem` nicer to use

CSS variables!

```css
html {
  --16px: 1rem;
  --17px: 1.0625rem;
  
  --font-size-sm: 0.875rem;
  --font-size-md: 1rem;
  --font-size-lg: 1.125rem;
}
h1 {
  font-size: var(--21px);
}
```


### Problems with the 62.5% trick

```css
html {
  font-size: 62.5%;
}
p {
  /* Equivalent to 18px */
  font-size: 1.8rem;
}
h3 {
  /* Equivalent to 21px */
  font-size: 2.1rem;
}
```

> [!Problems with the 62.5% trick]-
> - baseline assumption:`1rem` will produce readable text
> - break compatibility with third-party packages
> 	- eg: tooltip library that uses rem-based font sizes
> 	- break browser extensions

