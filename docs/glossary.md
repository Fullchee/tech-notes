# Glossary

<span style="font-size: 2.5rem;">**[A](#a)** **[B](#b)** **[C](#c)** **[D](#d)** **[E](#e)** **[F](#f)** **[G](#g)** **[H](#h)** **[I](#i)** **[J](#j)** **[K](#k)** **[L](#l)** **[M](#m)** **[N](#n)** **[O](#o)** **[P](#p)** **[Q](#q)** **[R](#r)** **[S](#s)** **[T](#t)** **[U](#u)** **[V](#v)** **[W](#w)** **[X](#x)** **[Y](#y)** **[Z](#z)**</span>

## A

### Argument (vs parameter)

-   the values you provide when you call a function
-   `funcName("arg1", "arg2)`

## B

### Barrel file

```js
export { Component1 } from "./Component1";
export { Component2 } from "./Component2";
export { Component3 } from "./Component3";
// ...
```

-   problem
    -   when VSCode auto imports, it usually imports from the barrel file 😥

## C

### Chesterton's fence
- only remove the fence
- after you learn why the fence was there in the first place

### Concurrent

-   2+ actions in progress at the same time
    -   can be done with one thread
    -   example: JS
    -   in contrast to parallel
        -   2+ actions executing at the same time (multi-thread/core)

## D

### Debounce

-   do something after 1 second
-   examples
    -   live search
        -   make an API call once they stop typing
    -   scroll position
    -   do something when the user stops resizing their window
    -

#### Debounce vs throttling

-   example: only allow 100 API calls per hour

### DEI

-   Diversity, Equity and Inclusion

## E

## F

### Feed

-   example: news feed, Facebook feed
-   the analogy turns us into livestock
-   we're given feed, not food

## G

### Generativity

-   what you generate
-   your team + you vs your team without you
-   usage example: [Jessica Kerr talk](forget-velocity-lets-talk-acceleration.md)
-   more useful than personal productivity
    -   shaving yaks is super generative but not productive

### GHCR

-   GitHub Container Registry
-   I saw this when downloading stuff with brew

### Glue work

-   Tanya Reilly talk: https://fullchee-reminders.netlify.app/link/1454
- Glue work makes projects succeed
-   less glamorous (and often less-promotable) work that needs to happen to make a team successful
    -   documentation
    -   creating reports
    -   onboarding teammates
    - noticing when people are blocked
        - unblocking them
    - making sure the roadmap is up to date
    - Requirements: noticing when things are being hand-waved and aren't gonna work
- senior stuff
- if you do glue work too early, it can be career limiting
	- you might get glowing performance reviews
	- but if your tech skills aren't good enough, you won't get promoted to senior
	- manager should've told her that she wasn't doing promotable work
- getting everyone to agree on coding standards
- bias
	- when your role is "manager", people assume that your tech skills are gone

### Golden yak

-   see yak shaving
-   Jessica Kerr
-   https://fullchee-reminders.netlify.app/link/1927

## H

### [Heisenbug](https://en.wikipedia.org/wiki/Heisenbug)

-   bug that's not reproducible when you try to fix it

### HMR
- Hot Module Replacement
	- instead of restarting your server while developing every time a change is made
	- replaces, adds or removes modules when code is edited

### Hyrum's Law
- implicit dependencies
- when an API has sufficient users
	- all observable behaviours of the system will be depended on by someone
- eg: [Removing an unused form field](https://thebootstrappedfounder.com/hyrums-law/)
	- teachers wrote notes in that form field
	- when it was removed -> they lost their notes

## I

### ISR

-   incremental static regeneration
    -   create/update static pages after building site
    -   Next.JS can do this
    -   ????
    -   Is it the thing when someone visits a page
        -   The backend generates an updated page
        -   So the next person will get the updated page?

## J

## K

### Kreplit

-   A unit of time and energy, love and affection
-   see Jessica Kerr's talk
-   usage example: [Jessica Kerr talk](forget-velocity-lets-talk-acceleration.md)

## L

### Leaky abstraction

- abstraction exposes some implementation details
	- underlying details aren't completely hidden
- example
	- SQL or ORM (similar queries can be slow or fast)
	- car: you can sort of feel the transmission as it switches gears
	- Tailwind: you have to know CSS to use it
- 

## M

## N

## O

### OLAP

-   online analytical processing
-   business insights from data
-   running queries in your data warehouse

### OLTP

-   online transaction processing
-   concurrent transactions
    -   online banking, shopping, texting
    -   Running queries in your RDBMS

### Online vs offline Algo

????

I remember I had to implement Prim's Algo online version

## P

### Parameter vs Argument

-   the variables in the function definition
-   `function myFunc("arg1", "arg2)`
-   ????

### [Pendo](https://www.pendo.io/)

-   like Google Analytics but has more features for product owners?


### Purpose

#### Purpose vs Meaning
- Purpose : looking forward, meaning: looking back

#### Purpose vs Goals
- Goals
	- intentions that can be accomplished
- Purpose
	- intentionality, life aim, always in front of you
	- example: being a caring father, organizer of goals (Theme CGP Grey video)
	- ![[image-20221022145133249.png]]
- When your purpose is actually a goal
	- #1 tennis player: feeling ground hog day when you're the #1 tennis player (Andre Aggaci) to maintain

## Q

## R

### RUM
- [Real User Monitoring](https://docs.datadoghq.com/real_user_monitoring/)
- Datadog

## S

### [Sentinel value](https://treyhunner.com/2019/03/unique-and-sentinel-values-in-python)

-   completely unique (very specific) value
-   like Singletons
-   example
    -   Python's `None`, enums
    -   ????

### Slug

-   the part of the URL after the last slash
    -   `https://fullcheezhang.com/glossary` -> `glossary`

### SoC

-   Separation of Concerns

### SSG
* example
	* Server side (Java) with JS sprinkled
	* Switching between languages
* Server side generation
	* Great for small sites
* Spinner site generator
	* Anytime you need to show data that could change, you need to rebuild or show the user loading 


### symmathesy

-   https://medium.com/@jessitron/symmathecist-n-c728957ce71f
-   Jessica Kerr talk: https://fullchee-reminders.netlify.app/link/1117

## T

### Throttle

-   do something max once a second
-   see Debounce vs throttle

### Touring Complete

-   a program or language can express all possible programs
-   anything that's equivalent to the [Touring Machine](https://www.youtube.com/watch?v=RPQD7-AOjMI) is Touring complete

## U

## V

## W

### [Walrus operator](https://realpython.com/python-walrus-operator/)

## X

## Y

### [yak shaving](https://fullchee-reminders.netlify.app/link/1928)

-   doing `z` to do `y` to do `x` ... so you can do `a`
-   https://xkcd.com/1739/
-   https://sketchplanations.com/yak-shaving
-   [Malcolm in the middle example](https://fullchee-reminders.netlify.app/link/38)
-   [Jessica Kerr: shaving the golden yak](https://www.infoq.com/presentations/easier-software-development/)

## Z
