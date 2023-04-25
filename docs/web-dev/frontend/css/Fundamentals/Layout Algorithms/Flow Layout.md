https://courses.joshwcomeau.com/css-for-js/01-rendering-logic-1/09-flow-layout

```css
display: inline;
display: block;
display: inline-block;
```

## Inline Elements
- thinks it's Typography
	- [Typography Layout](Typography%20Layout.md)

> [!What's 2 special things about inline?]-
>    - no height/width
>       - can't apply padding 
>    - Inline elements don't have to be rectangles
>        - ![inline-line-wrap.png](inline-line-wrap.png)
>        -   Horizontal padding is just on the tips

### Troubleshooting inline issues
#### Mysterious space at the bottom of image

- Not a part of the box model
        -   ![magic-bottom-space-inline.png](magic-bottom-space-inline.png)

> [!Solution to magic space at the bottom]-
> - `display: block`
> - `line-height: 0` on the wrapping div

#### Unexpected space between inline elements (images)
- ![whitespace-spacing.png](whitespace-spacing.png)


> [!Solution to magic space at the bottom]-
> whitespace in HTML
> 
> - `display: flex` or `grid`
>    - (this problem is only in flow)
> - `line-height: 0` on the wrapping div
>    -   ![cats-without-whitespace.png](cats-without-whitespace.png)

### Inline padding-left/right

Default

```css
box-decoration-break: slice;
```

![inline-padding-left-right.png](inline-padding-left-right.png "inline-padding-left-right.png")

Since it line wraps, it only applies padding on the tips

```css
-webkit-box-decoration-break: clone;
box-decoration-break: clone;
```

![box-decoration-break-clone.png](box-decoration-break-clone.png)

### Replaced elements

-   img
-   video
-   canvas

Inline wrapper on some foreign object

???? replaced elements vs inline elements????
- images seem to act like inline elements (see above)

## Inline-block

-   like `inline` except it has width/height
	- can apply padding
-   Like block that you drop in an inline context
-   Parent will treat it like inline
-   example: buttons
    -   inline elements with padding
-   doesn't have that sweet sweet word wrap


## [Width](https://courses.joshwcomeau.com/css-for-js/01-rendering-logic-1/10-widths)
---

Default: `width: auto`

### Width keywords

#### auto vs 100%

> [!Solution]-
> `100%`: horizontal scroll if the child has margin
> - margin not a part of `box-sizing: border-box`
> 
> `auto`  takes margin into account
> - will line wrap if needed
> - [Kevin Powell: Stop using with: 100%](https://fullchee-reminders.netlify.app/link/2232)
> - TODO: embed the short video

#### min-content

-   sizing based on the children
-   ![min-content.png](min-content.png "min-content.png")

#### `max-content`

-   never add line breaks
-   may cause horizontal scroll

> [!Use case of max-content]-
>   why: if you want the background to only cover the text
>    - max-content:   ![width-max-content.png](width-max-content.png)
>    -   auto: ![width-auto-background-color.png](width-auto-background-color.png)

#### `fit-content`

-   content can fit in parent -> act like `max-content`
-   otherwise: act like `width: auto`

##### [Implementing `fit-content`](https://courses.joshwcomeau.com/css-for-js/01-rendering-logic-1/10-widths#solutions-have-been-discovered)

```css
/* width: auto */
max-width: max-content;
min-width: min-content;
```

1. implicit `width: auto`
2. content is short (eg: 100px) -> max-width kicks in
3. content is long af
	1. max-width: has no effect 
	2. `width: auto`
4. `min-width` handles large unbreakable word in narrow container
	1.  ![unbreakable-word-in-narrow-char.png](unbreakable-word-in-narrow-char.png)

### min-width vs max-width

`min-width` > `max-width` > `width`

### Exercise

```html
<figure>
    <img alt="" src="" />
    <figcaption>Found on Unsplash.</figcaption>
</figure>
```

Before
![[image-20230113144441882.png]]

After

![make-figure-caption-word-wrap.png](make-figure-caption-word-wrap.png)


> [!Solution to dynamic width figure and caption]-
> on the parent `figure` -> `width: min-content`
> 
> will look for the widest child and make that the width

### Setting a fixed width

- set a `max-width`
- prevent horizontal scroll where the width is wider than the screen


```css
.button {
  max-width: 100%;
}
```

### [[Which units to use#Width/heights]]

## [Height](https://stackoverflow.com/a/22675563/8479344)
---

> look down the tree to see how tall it should be

* children determine parent height

Default height is like `width: min-content`
- as small as possible to fit content

### Setting a fixed height
- you really shouldn't, will almost always cause overflow
- use `min-height`

### Why percentage height has no effect

Goal

![[image-20221024080322661.png]]

Actual

![[image-20221024080337789.png]]

Parents shrink-wrap to fit their children snuggly

#### Solution

```css
html, body, #root, #__next {
  height: 100%;
}
```

When the `body` has height: 100%

this is better than `height: 100vh` because `100vh` is a bit taller on mobile devices

Or the new CSS viewport height`height: 100dvh`
* doesn't take the keyboard into effect


need to add `height: 100%` for every element between the `html` element and the element we want to stretch to 100% of the screen

### Aspect Ratio

aspect-ratio: 1 / 1;

#### Implementing Aspect Ratio

```css
width: 300px;
height: 0;
padding-bottom: calc(300px * 9 / 16);
```

For 9/16 ratio
[clientHeight](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientHeight)

> returns the inner height of an element in pixels, including padding but **not**

-   Horizontal scrollbar
-   height
-   **border**
-   **margin**

[offsetHeight](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetHeight)

> is a measurement which **includes** the element **borders**, the element vertical padding, the element horizontal **scrollbar** (if present, if rendered) and the element CSS height.

[scrollHeight](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollHeight)

> is a measurement of the height of an element's content **including** content **not visible** on the screen **due to overflow**

## [[Margin#Margin Collapse]]
