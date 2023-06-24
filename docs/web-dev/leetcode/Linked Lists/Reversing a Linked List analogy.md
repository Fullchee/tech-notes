Rick and Morty
- Summer and Morty breaking Rick out of jail
- and reversing the portals behind them

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

The loop ends when Summer = `None`

and Morty is at the first node
- return Morty