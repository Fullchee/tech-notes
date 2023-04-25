```html
a[class|="link"]
```


|=
{{c1::starts w/ "link-" or exactly "link"}}

^=
{{c2::starts w/ "link"}}

$=
{{c3::ends w/ "link"}}

*=
{{c4::looks for "link" a/wh}}


## `:has`

https://codesandbox.io/s/bytes-has-selector-lg94f7

```html
<ul>
  <li>Home</li>
  <li>About</li>
  <li>Contact</li>
  <li>Blog</li>
</ul>
```

????

```css
li {
  display: block;
  cursor: pointer;
  transition: opacity 0.3s ease-in-out;
}

li:has(~ li:hover),
li:hover ~ li {
  opacity: 0;
}
```