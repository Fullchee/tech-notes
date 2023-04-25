## Shortcuts that aren't engrained

- Ctrl + XX
	- move between start of command line and current cursor position (and back again)
- Alt + T
	- swap current word with previous
- Alt + U
	- uppercase from cursor to end of word
- Alt + L
	- lowercase from cursor to end of word
- Alt + .
	- use the last word of the previous command**



## `fzf` shortcuts

- `Ctrl-R`
	- better searching through history with `fzf`
-   `CTRL-T`
	- list of **files** and folders in the current directory
	- pastes the selected path to the command line
-   `ALT-C`
	- lists subdirectories in the current directory
	- `cd` into the selected directory


## Bang (!) Commands

- `!!`
	- run last command
	- `sudo !!`
- `!blah`
	- run the most recent command that starts with ‘blah’
	- `!ls`
- `!$`
	- the last word of the previous command
	- same as `Alt + .`
	- `!$:p`
		- print out the word that `!$` would substitute
		- instead of running it
- `!*`
	- the previous command except for the last word
	- `find some_file.txt /`
	- `!*` would give you `find some_file.txt`
	- `!*:p`
		- print out what `!*` would substitute
		- instead of running it