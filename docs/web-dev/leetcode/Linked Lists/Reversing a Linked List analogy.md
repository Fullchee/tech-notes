Rick and Morty
- Summer and Morty breaking Rick out of jail
- and reversing the portals behind them
- freezing time?

## Characters

sorted by age

- Rick (next)
	- just walks
- Summer (curr)
- Morty (prev)

Summer and Morty have portal guns

## Init values

- Rick = curr
- Summer = curr
	- Rick's cell
- Morty = `None`
	- the house

## Loop condition
While Summer is not `None`
- keep going until Summer enters the final `None` portal

## Loop
1. Rick moves to the next cell
	1. Rick = Rick.next
2. Reverse the portal
	1. Summer.next = Morty
3. Summer and Morty portal to the next cells
	1. Morty = Summer
	2. Summer = Rick

At the end of the loop, Rick.next = `None` (the house)