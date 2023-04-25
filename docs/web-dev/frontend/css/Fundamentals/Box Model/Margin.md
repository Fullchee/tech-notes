## [[box-model]]

## [[Which units to use#Border/margin/padding]]

## Margin vs padding

### One liner: margin vs padding

**Margin**
- space from the box & everything else
	- space between siblings

**Padding**
- space between parent and child

### Only margin
- negative margins
- has collapsing margins
- margin-left/right has the `auto` property

## When to use margin

[Margin considered harmful](https://mxstbr.com/thoughts/margin/)

> Margin is like putting glue on something before you’ve decided what to stick it to, or if it should be stuck to anything.

For spacing between siblings, use layout components like Stack

```jsx
function BlogPost() {
  return (
    <Stack>
      <p>Hello world!</p>
      <VideoClip />
      <p>Yadda yadda yadda</p>
      <SomeEmbeddedThing />
    </Stack>
  )
}
```

[Syntax FM Margin episode](https://traffic.libsyn.com/secure/syntax/Syntax_-_503.mp3?dest-id=532671)

-   Only use padding for standalone components
    -   you don't know where the component will be
-   only margin-bottom
	- no `margin-top` (predictable)
-  flex/grid for everything
	- no collapsing margin
-   a div component just for space

## Negative margin

the only one of the three that can be negative

-   will still move around the children
    -   because of the flow algo
-   unlike `transform: translate()`

## `margin: auto`

### `margin: auto` in flow layout

-   left/right `margin: auto` only works if there's an explicit width
-   put the leftover space in the left/right

```css
margin-left: auto;
width: 24rem;

margin-top: auto; /* spec says 0 */
```

### [[Positioned Layout#`margin: auto`]]

### Stretch out an image with margin

Get child to break free from the parent padding

When width: auto, left and right margin extend the width of the box

.stretched works if you put a paragraph in it too

-   you could use `calc()`

if this feels hacky, see [[CSS Grid]] and full bleed layout

```diff
<div class="card">
    <p>The otter is the best</p>
+    <div class="stretched">
        <img src="/otter.jpg" />
+    </div>
    <p>The best</p>
</div>
```

```css
.stretched {
    margin-left: -32px;
    margin-right: -32px;
}

.stretched img {
    width: 100%;  /* parent's width is made wider by the -ve margin */
}
```

![margin-can-go-through-parent-padding.png](margin-can-go-through-parent-padding.png)
![margin-stretched-out.png](margin-stretched-out.png)

## Margin collapse

only in flow layout

[Rules of Margin Collapse](https://courses.joshwcomeau.com/css-for-js/01-rendering-logic-1/12-rules-of-margin-collapse)

[Will It Collapse? (Game)](https://courses.joshwcomeau.com/css-for-js/01-rendering-logic-1/13-will-it-collapse)

![collapsing-margin.png](collapsing-margin.png)

Margin will collapse when margins are

1. Vertical
	1. parent and child margins can merge if they're in the same direction
	2. horizontal doesn't collapse
2. touching (adjacent)
	1. not blocked by
		1. padding/border
		2. another element
		3. a gap (child margin doesn't extend outside of parent)
		4. scroll container
			1. overflow: auto, hidden, ...


This won't collapse margin

```html
<p>Paragraph One</p>
<br />
<p>Paragraph Two</p>
```

Margin increases distance between siblings
- child can transfer margin to parent!


```html
<div>
  <p>Paragraph One</p>
</div>
<p>Paragraph Two</p>
```


Padding gap between child and the parent's bounding box

```html
<div style="min-height: 500px">
	<p style="margin-bottom: 20px">P One</p>
<div>
<p style="margin-top: 20px">P Two</p>
```

![[image-20221024103552947.png]]


-   including parent margin and child margin
    -   (both can be margin-top)
- only flow layout
	- flex and grid don't have this issue


### How margin gets calculated

1. Find the largest positive margin
2. Find the largest (absolute) negative margin
3. add them together