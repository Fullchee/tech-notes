[JC: Relative Positioning](https://courses.joshwcomeau.com/css-for-js/02-rendering-logic-2/01-positioning)

Default is static

## Inset

```css
inset: 0;
inset: 0 0 0 0;
inset auto 0 auto 0;  /* doesn't set a value for top and bottom */
```

<=>

```css
top: 0;
right: 0;
bottom: 0;
left: 0;
```

### `margin: auto`

[[Margin#`margin: auto` in positioned layout]]

- centres the element both horizontally and vertically

```css
position: fixed;
margin: auto;
inset: 0; /* top = right = bottom = left = 0*
```


## Position vs margin

Absolute

- ????top: 0 vs margin-top: auto;

margin > top

### `position: sticky`

[JC: Sticky Positioning](https://courses.joshwcomeau.com/css-for-js/02-rendering-logic-2/15-sticky)

- only stick while their container/parent is in view
	- the parent doesn't have to be within sticky
	- eg: parent with `margin: 100rem 0`


can horizontally stick too!

`top: 10px` means that the sticking point is 10px from the top

![[sticky-exercise-1-demo.mp4]]

```css
.header {
	height: 50px;
}
```

> [!Answer]-
> ```css
>   position: sticky;
>   top: -16px;
>   height: calc(50px + 16px);
>   padding-top: 16px;
> ```

