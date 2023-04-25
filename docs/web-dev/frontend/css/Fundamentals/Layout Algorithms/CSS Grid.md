[CSS Grid cheat sheet](https://css-tricks.com/snippets/css/complete-guide-grid/)

One liners
 - [One liners](https://web.dev/one-line-layouts)

## Units

### 1fr vs auto

auto is shy

1fr is greedy

1. grid calclates the min width of the auto items
2. gives the rest of the space to fr units
3. if there isn't any fr units, give the rest of the space to the auto items

If there isn't enough space, auto looks bigger than 1fr?

1fr might be greedy when it comes to taking space away too???? 

https://codepen.io/Fullchee/pen/VwQzZZV



### Auto-fill vs Auto-fit

**Auto-fill**

-   ![922ec503ac8c417fa3ba5fc6153c4e82.png](922ec503ac8c417fa3ba5fc6153c4e82.png)
-   adds new empty columns that occupy space

**auto-fit**

-   ![a58ffd7243a8a657fdc3b1e5d5a8f655.png](a58ffd7243a8a657fdc3b1e5d5a8f655.png)
-   make the columns fit the space
-   empty columns occupy no space

## Full-Bleed Layout

https://www.joshwcomeau.com/css/full-bleed/

```css
.wrapper {
    display: grid;
    grid-template-columns:
        1fr
        min(65ch, 100%)
        1fr;
}
.wrapper > * {
    grid-column: 2;
}
.full-bleed {
    width: 100%;
    grid-column: 1 / 4;
}
```

## Refactor 

```jsx
const style =
    data.length === 3
      ? { gridTemplateColumns: 'repeat(3, 1fr)' }
      : { gridTemplateColumns: 'repeat(2, 1fr)' };

return <div style={style}></div>
```


### Solution

> [!info]-
> ```jsx
> return <div data-grid-columns={data.length === 3 ? 3 : 2}></div>
> ```
> ```css
> div {
>   grid-template-columns: repeat(2, 1fr);
>  &[data-grid-columns="3"] {
>      grid-template-columns: repeat(3, 1fr);
>    }
> }
> ```
