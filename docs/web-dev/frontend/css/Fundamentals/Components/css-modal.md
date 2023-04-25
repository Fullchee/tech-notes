# CSS Modal

intentionally disruptive

[Modals, Popups, Popovers, Lightboxes — Syntax Podcast 602](https://syntax.fm/show/602/modals-popups-popovers-lightboxes)



-   `aside` has better support than `dialog`

1. dialog tag that's a sibling to the main content
2. blur, decrease contrast and brightness on the main when there's a de-emphasized class on the main content
   filter: blur(3px) contrast(0.8) brightness(0.8)
3. animation

## Lock page scrolling under modals & menus

`overflow: hidden`


```css
body:has(.modal[data-active="true"]) {
	overflow: hidden;	
}
```

React: use portals