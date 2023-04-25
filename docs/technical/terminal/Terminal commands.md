[Julia Evans: A list of new(ish) command line tools](https://jvns.ca/blog/2022/04/12/a-list-of-new-ish--command-line-tools/)

## Clipboard

-   pbcopy & pbpaste

https://osxdaily.com/2007/03/05/manipulating-the-clipboard-from-the-command-line/

-   `pbcopy < file.txt`
-   `ps aux | pbcopy`

-   `pbpaste > pastetest.txt`
-   `pbpaste | grep rcp`

## `xargs`

-   Run a command using the input data as arguments:
-   `arguments_source | xargs command

## Secrets

```bash
read -s PGPASSWORD
secretly_type_your_password
export PGPASSWORD
```

### [direnv](https://github.com/direnv/direnv)

-   Checks for `.envrc` > `.env`
-   makes them environment variables

## Search

### ripgrep (rg)

-   better than `grep`
-   [ripgrepall](https://github.com/phiresky/ripgrep-all) also searches PDFs and other files - `brew install rga` - `brew install pandoc poppler tesseract ffmpeg`
    ????
    Example use cases

### Read logs

`lnav` has syntax highlighting for logs

### [Hyperfine](https://github.com/sharkdp/hyperfine) CLI Benchmarking Performance

## Typos

-   zsh auto recommends a command if you mistype
-   for subcommands, use [thefuck](https://github.com/nvbn/thefuck)
    -   video: https://user-images.githubusercontent.com/11246258/163878799-c9b01191-e253-4a9b-9818-429d1bc7a30e.mp4

## Python list to bash

```bash
space_separated_strings=$(python file.py | tr -d '[],')

# We need the eval because ????
eval "for query_content in $query_content_list; do
    echo \$query_content
    psql2 $COMMISSIONS_DB -c \$query_content;
done"
```

You should just do everything in Python
Run the shell psql2 from Python

???? What did Viktor do?

## `su` vs `sudo`

-   `su` switches users
-   `sudo` keeps the current user, runs as if they were sudo
-   `su -` creates a new environment with the super user's env var and switches to their home directory
-   `sudo su -`

### Open a man file in Preview (as a PDF)

`man -t apropos | open -fa Preview`


## Notify yourself after 10 mins

Doesn't work with do not disturb mode on 😞

```sh
# can't do sleep 10m on Mac
reminder() {
	sleep $((60*$1)) && osascript -e 'display notification "$2"'
}
```