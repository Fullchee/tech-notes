<iframe width="500" height="360" src="https://www.youtube.com/embed/Wm_xI7KntDs" title="The Story of React" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

[React, visualized – react.gg](https://react.gg/visualized)

## History

### jQuery

- DOM manipulation library
- App state is in the DOM
	- Just read what's on the page to see the state
- Problem: DOM as global state
	- Hard to debug and understand what changed what when you have a ton of mutations 

### Angular 1
- Opinionated all in one tool
- Everything out of the box
	- 2 way data binding
	- Model, view, controller
	- Routing
	- Templates
	- mini jQuery
	- ..  
- 2011: lots of backend devs having to write frontends

>[!Problems with Angular 1]-
>- 2 way data binding
>- Hard to understand & debug code
>- not performant, constantly check for updates

## Why React

### One way data binding

>[!Benefits of one way data binding]-
>1. easier to debug
>2. more performant, only run code when it needs to

>[!How does React do one way data binding?]-
>`rendered app = f(state)`
>
>state changes -> re-render app


### Components

>[!Why weren't there components before React?]-
>React rethought: the default separation of concerns: HTML, CSS, JS
>
>- they're all the concern of the component
>   - Lots of initial dev hate

>[!How did React implement components?]-
>JSX: HTML, CSS & JS in one
>view = f(state)
>- compose components
>- view = comp1(comp2(state))

>[!Biggest benefit of components]-
>Scalable design systems
>- build your own
>- or 3rd party
>   - Material UI
