# [CSS Inheritance](https://courses.joshwcomeau.com/css-for-js/01-rendering-logic-1/01-built-ins-and-inheritance)

like JS prototypal inheritance

```css
<main style="color: black;">
  <p style="color: red;">
    Hello <span>World</span>
  </p>
</main>
```

```javascript
class Main {
    color = "black";
}
class Paragraph extends Main {
    backgroundColor = "red";
}
class Span extends Paragraph {}
const s = new Span();
console.log(s.color);
```

### `initial`, `inherit`, `unset`, `revert`

initial

-   Spec default
-   Not browser user agent stylesheet!

inherit

-   "Get the first ancestor who set this property"
-   Some elements inherit some properties by default
	- typography properties
-   Need to explicitly set inherit for everything else
    -   anchor tag with href: doesn't inherit color
    -   Height

unset

-   For a property that is inherited
    -   (e.g. color)
    -   it means inherit
-   for a property that isn’t inherited
    -   (e.g. float)
    -   it means initial
-   I don't know why you'd use `unset` when `revert` is nicer

revert

-   For a property that is inherited
    -   (e.g. color)
    -   it means inherit
-   For non inherited
    -   Revert to User Agent browser default
        - example: `display`

### Why don't form elements inherit styles?

-   button
-   input
-   select

Historical reasons

-   They're user interface elements
-   which were should look like the OS
