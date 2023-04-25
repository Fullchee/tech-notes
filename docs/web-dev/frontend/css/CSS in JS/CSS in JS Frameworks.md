[Why We're Breaking Up with CSS-in-JS](https://dev.to/srmagura/why-were-breaking-up-wiht-css-in-js-4g9b)

## Pros

- Locally scoped styles
	- CSS modules can do this too!
- CSS is in the same place as where it's used
	- JS variables in styles

## Cons

### Worse performance
- runtime CSS-in-JS
	- example: `emotion` and `styled-components`
	- [x] inserts new style rules when components rendercss mo
- multiple instances of Emotion
- tons of issues
	- component libraries don't give you full control 

### Other cons
- increase bundle size
	- ~10kb
- clutters React Dev Tools
	- ![[image-20221027175025925.png]]


## CSS Modules

- in WebPack or PostCSS
- automatically makes unique class names