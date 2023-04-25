@font-face

## Problem with underlining

-   underline usually means a link

[Magic spacing at the bottom](https://courses.joshwcomeau.com/css-for-js/01-rendering-logic-1/09-flow-layout#inline-elements-have-magic-space)

## Line height

**The minimum recommended value is 1.5.**

Why?

`text-wrap: balance`


![[image-20221026153823856.png]]

## How to make it wrap?
- white-space: normal;

### word-wrap vs white-space property


word-wrap got renamed to overflow-wrap

choose whether to break words to the next line

white-space

whether to not go to wrap text or not

## Word break vs overflow wrap

Word break has logic for asian characters  
  
Overflow wrap knows about words whereas word break will just cut off words at the end of the container




### [Inline content separators](https://medium.com/@mandy.michael/you-dont-need-a-media-query-for-that-1-inline-content-separators-a9c562a597a6)

-   ![a0e93e7fc4e12ce32b05d5bb73386607.png](a0e93e7fc4e12ce32b05d5bb73386607.png "a0e93e7fc4e12ce32b05d5bb73386607.png")
-   ![916f43045c6b45731a9e9c76b6afd4ae.png](916f43045c6b45731a9e9c76b6afd4ae.png "916f43045c6b45731a9e9c76b6afd4ae.png")

```css
.container {
    overflow: hidden;
}
.entry {
    transform: translateX(-10px);
    padding-left: (10px);
}

.entry::before {
    top: 0;
    left: 0;
    width: 1px;
}
```
