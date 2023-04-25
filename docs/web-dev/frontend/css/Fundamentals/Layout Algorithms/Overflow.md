[JC: Overflow](https://courses.joshwcomeau.com/css-for-js/02-rendering-logic-2/14-overflow)

## Scroll bars

### Always show scroll bars on mac!
-   by default, scroll bars are always visible on non-macs
- macs: fade away on blur

## Scroll containers

like Dr Who's TARTIS
- telephone box on the outside
- giant spaceship on the inside

### When does a scroll container scroll?

- when the inner size exceeds the outer size
	- only when there's overflow
- height: the outer size can keep on growing


## `overflow` values

> [!Default overflow value?]-
> `overflow: visible`
> we want overflow to be visible by default
> 
> so even if the site is broken, we have all the content

> [!When to use `overflow: scroll`]-
> if it will always scroll

> [!When to use `overflow: auto`]-
> use if it MIGHT scroll
> doesn't need to scroll? won't show the scroll bar

> [!When to use `overflow: hidden`]-
> - truncate text with ellipses
> - decoration
>    - ![b1c377c5de363ba8c6064889e2d9f6fd.png](b1c377c5de363ba8c6064889e2d9f6fd.png)
> - Solve specific problems
> 	- mobile: when the menu is open, we don't want the lesson content on the right to cause a horizontal scroll
> - ![6279ff3f7c7ff1aa8ec781a1fc9a36c8.png](6279ff3f7c7ff1aa8ec781a1fc9a36c8.png)

> [!`overflow: scroll` vs `overflow: hidden`]-
> they're the same thing
> `hidden` has the scrollbars removed
> you can still toggle over


- always comment explaining why you used `overflow:hidden`
	- future self might remove it
	- not obvious what it broke

> [!`overflow: hidden` vs `overflow: clip`]-
> `clip` is kinda similar except no scroll container is created
> when you toggle to a hidden link, it won't scroll the container: ![[image-20230315112938976.png]]
> 
> so we have to test manually


## Exercise: Only overflow in one axis
[JC: Scroll container with `overflow: clip`](https://courses.joshwcomeau.com/css-for-js/02-rendering-logic-2/14.1-scroll-containers#overflow-clip-1)
![[image-20230314184845128.png]]

Setting overflow to non-visible turns an element into a scroll container

```css
overflow-x: hidden;
overflow-y: visible;
```

![de9ff42109765ccb58504230868356c2.png](de9ff42109765ccb58504230868356c2.png)

2 solutions

1. `overflow: clip`
2. wrapper with `overflow-x: hidden`

### Scroll containers and positioned layout

#### `position: relative`

- ensure that the containing block (the `position: relative` parent)
- is a scroll container (has `overflow: ...`)

### `position: fixed`

containing block for `position: fixed` is outside of the DOM
- can't put/hide `position: fixed` in a scroll container!

**TODO: confirm in the JC lesson**

## Horizontal Overflow

```css
white-space: nowrap;
overflow: auto;
```

### Find the random overflowing element that makes the whole page scroll horizontally

```js
document.querySelectorAll("*").forEach(el => {
  if(el.offsetWidth > document.documentElement.offsetWidth) {
    console.log(el);
  }
})
```

or use the classic trick
```css
* {
  border: 1px solid red;
}
```
