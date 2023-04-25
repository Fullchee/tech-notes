## Mixins

[Sass: @mixin and @include](https://sass-lang.com/documentation/at-rules/mixin)

### Mixin vs Function

`@function` returns a value

`@mixin` returns CSS


### Using mixins

```scss
@mixin reset-list {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav ul {
  @include reset-list;
}
```


### Mixins with variables where you can set the property

```scss
@mixin rtl($property, $ltr-value, $rtl-value) {
  #{$property}: $ltr-value;

  [dir=rtl] & {
    #{$property}: $rtl-value;
  }
}

.sidebar {
  @include rtl(float, left, right);
}
```

### Mixins with optional params

```scss
@mixin square($size, $radius: 0) {
  width: $size;
  height: $size;

  @if $radius != 0 {
    border-radius: $radius;
  }
}

.avatar {
  @include square(100px, $radius: 4px);
}
```

[Taking Arbitrary arguments[]()](https://sass-lang.com/documentation/at-rules/mixin#taking-arbitrary-arguments)

## Loops

????
