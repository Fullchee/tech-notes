## When is a new stacking context created?

position: not the default static and has a z index

element has opacity less than 1

transforms, filters,


## Reducing z-index usage

[JC: Managing z-index](https://courses.joshwcomeau.com/css-for-js/02-rendering-logic-2/08-reducing-z-index)

### `isolation: isolate`
```css
.pricing {
  isolation: isolate;
}
```

just creates a stacking context

really nice in components which could be used 