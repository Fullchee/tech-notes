<iframe width="560" height="315" src="https://www.youtube.com/embed/5-1LM2NySR0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Redux vs React Context

-   [Dan Abramov: You might not need redux](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367)
-   Redux actually uses React Context behind the scenes
-   Redux should only store JSON serializable stuff
    -   Context can store anything like functions and react components


[[react-query]] for server state

## Simpler alternatives to Redux for client state

1. useState
2. jotai
	1. globals
3. zustand
	1. creates a store and actions
	2. machine
	3. subscribe to just 
