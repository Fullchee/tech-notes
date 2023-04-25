[[box-model]]

## [[Which units to use#Border/margin/padding]]

## Setting border

-   only `border-style` is required
    -   without it, border won't render
    -   `border: solid` => 3px black
    -   there's a bunch of other styles
        -   ![border-styles.png](border-styles.png)

## Color of the border
-   uses `currentColor` by default
-   the font color

## Border vs outline vs box-shadow

Example: for a focus indicator

![button-with-border.png](button-with-border.png "button-with-border.png")

**border**

-   takes up space in flow
-   `box-sizing: border-box`?
    -   it will shrink the content slightly

**outline**

-   takes up no space
    -   not a part of the box model
-   `outline-offset`: can be negative -> inside the content
-   respects `border-radius`
-   Accessibility

**box-shadow**

-   can have multiple box shadows
-   doesn't appear in Windows high contrast themes

workaround: a transparent outline fallback for box-shadow

```css
a:focus {
    /* Visible in the full-colour space */
    box-shadow: 0px 0px 5px 5px rgba(0, 0, 255, 1);

    /* Visible in Windows high-contrast themes */
    outline-color: transparent;
    outline-width: 2px;
    outline-style: dotted;
}
```

### Have a border only on one side

box-shadow!


## Border radius

should've been called **corner radius**
- you don't need a border

### [Nested Rounded Corners](https://cloudfour.com/thinks/the-math-behind-nesting-rounded-corners/)

![image-20221115121033740.png](image-20221115121033740.png)


```css
--outer-radius: 1em;
--padding: 0.5em;
--inner-radius: calc(var(--outer-radius) - var(--padding));
```

## Page dog ear

Cut out a corner

Lea Verou book

??????

```css
background: linear-gradient(-45deg, transparent 15px, blue 0);
```


## Box shadow

### How box shadow works

```css
box-shadow: 1px 2px 3px 4px grey;
```

1. a grey background is drawn with the same size and position as our element
2. moved 1px to the right and 2 px down
3. blurred by 3px
4. spread by 4px (makes your blur start further out)
5. Clip the shadow where the shadows and the element intersect

![6c759c7b2c4ec32d9974357c2a7f72b8.png](6c759c7b2c4ec32d9974357c2a7f72b8.png "6c759c7b2c4ec32d9974357c2a7f72b8.png")
