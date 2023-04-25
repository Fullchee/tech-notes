<iframe width="426" height="360" src="https://www.youtube.com/embed/9Y4P3FvZ5bg" title="How to create SVG shapes [ A beginners guide to SVG part 2 ]" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Why SVG

## How SVG describes an image

-   container that defines a new coordinate system and viewport
-   can embed an SVG in HTML or another SVG

TODO: nested SVGs???

## `<svg>` properties

-   width
-   height

```html
xmlns="http://www.w3.org/2000/svg"
```

### [`viewBox`](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/viewBox)

## `<circle>`

default `fill` is black

```html
<circle r="120" cx="125" cy="125" fill="none" stroke="red" stroke-width="10" />
```

## `<rect>`

```html
<rect x="0" y="0" height="100" width="100" rx="15" ry="100" />
```

### Round corners

-   how many pixels before it stops curving
-   same as border-radius

if either `rx` or `ry` is 0, then it goes back to 90 degree angles

## `<line>`

```html
<line x1="10" y1="125" x2="225" y2="225" stroke="green" />
```

## Path

```css
M 213.1,6.7
```

-   Move to (don't draw anything)

upper case: absolute
lower case: relative

```css
c -32.4-14.4-73.7,0-88.1,30.6
```

-   curve
    https://css-tricks.com/svg-path-syntax-illustrated-guide/

```css
z
```

closes the path

| **M**x,y       | Move to the absolute coordinates x,y                                                                     |
| -------------- | -------------------------------------------------------------------------------------------------------- |
| **m**x,y       | Move to the right x and down y (or left and up if negative values)                                       |
| **L**x,y       | Draw a straight line to the absolute coordinates x,y                                                     |
| **l**x,y       | Draw a straight line to a point that's relatively right x and down y (or left and up if negative values) |
| **H**x         | Draw a line horizontally to the exact coordinate x                                                       |
| **h**x         | Draw a line horizontally relatively to the right x (or to the left if a negative value)                  |
| **V**y         | Draw a line vertically to the exact coordinate y                                                         |
| **v**y         | Draw a line vertically relatively down y (or up if a negative value)                                     |
| **Z**(or**z**) | Draw a straight line back to the start of the path                                                       |

## SVG Sprites

### `<symbol>`

```html
<svg xmlns="http://www.w3.org/2000/svg" style="display:none;">
  <symbol id="icon-circle" viewBox="0 0 32 32">
    <circle cx="16" cy="16" r="16" />
  </symbol>
  
```

```html
<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32">
  <use href="#icon-circle" />
</svg>
```

### Using SVG Sprites in React

```jsx
function Icon({ id, ...props }) {
  return (
    <svg {...props}>
      <use href={`/images/sprite.svg#${id}`} />
    </svg>
  );
}

<Icon id="icon-circle" />
```