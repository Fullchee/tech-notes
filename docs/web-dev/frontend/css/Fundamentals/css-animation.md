## TODOs

-   https://www.joshwcomeau.com/tutorials/animation/

1. [Directing Focus](https://fullchee-reminders.netlify.app/link/876)
    - download complete: bouncing arrow
2. [Spatial Orientation](https://fullchee-reminders.netlify.app/link/880)
    - offscreen animation
    - side bar => will come from the left/right
3. [Timing](https://fullchee-reminders.netlify.app/link/877)
	1. 150-500ms
	2. smaller animations should take less time
	3. larger animations should take more time
4. [Easing](https://fullchee-reminders.netlify.app/link/875)
    - ease-in-out
5. [Clarity](https://fullchee-reminders.netlify.app/link/871)
    - don't animate so many things at once
    - no intersecting paths
    - staggering animations
6. [Visual Continuinity](https://fullchee-reminders.netlify.app/link/879)
    - shape morphing


## Pause a CSS keyframe animation

```html
<div class="circle"></div>
```

```css
.circle {
    animation: pulse 1s infinite ease-in-out;
}
```

```js
const animations = document.querySelector(".circle").getAnimations();
animations.forEach(animation => {
  animation.pause();
});
```

[bytes-pause-animation - CodeSandbox](https://codesandbox.io/s/bytes-pause-animation-i5u2ey?file=/index.html&ck_subscriber_id=1879694011)