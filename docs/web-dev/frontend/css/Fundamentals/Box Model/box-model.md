# Box Model

1. content
2. Padding
	1. inner space
	2. same background as content
3. [[Border, outline and box shadow]]
4. [[Margin]]

## [[Which units to use#Border/margin/padding]]

## Logical properties

Prefix with

-   `border`
-   `margin`
-   `padding`

-   -block-start: top
-   -block-end: bottom
-   -inline-start:left
-   -inline-end: right

example

-   `border-block-start: 10px`

## `box-sizing`

![[image-20230313225608713.png]]


Default: `box-sizing: content-box`

-   `width: 100px`
    -   content: 100px

`box-sizing: border-box`

-   setting `width: 100px`
-   content + padding + border = 100px

### Where to set box-sizing?

```css
html {
    box-sizing: border-box;
}

*,
*:before,
*:after {
    /* by default: isn't inherited, isn't typography */
    box-sizing: inherit;
}
```
