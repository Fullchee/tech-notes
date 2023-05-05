# Bash

## https://jvns.ca/blog/2022/04/12/a-list-of-new-ish--command-line-tools/

-   https://explainshell.com/
-   [`tldr`](https://tldr.sh/)



## General Tips

### Double Dash (`--`)

-   tells shell to treat any future dashes like strings and not flags
    -   `npm test -- -u -t="ColorPicker"`
    -   the `-u` is a flag for the command and not `npm`
-

```bash
grep "--hello" data.txt
grep: unrecognized option '--hello'
```

```bash
grep -- --hello data.txt
```

#### Why `git checkout -- file.txt`

-   the `--` is optional in this case
-   just a good habit, since branches usually have dashes

>[!${} vs $()]-
>`$()`: command substitution
>- first evaluate this, then evaluate the rest of the line
>- `echo $(pwd)/file.txt`
>
>`${}`: variable expansion
>- `MY_VAR=toto`
>- `echo ${MY_VAR}/file.txt`


## Loops

### Looping over array

```bash
for var in "$@"
do
    echo "$var"
done
```


### Looping over every file in the directory

```sh
for FILE in *; do
    ffmpeg -i "$(basename $FILE .mp4).mp4" -c copy "some_path/$(basename $FILE .mp4).aac";
done
```

Convert

```sh
for FILE in *; do
	ffmpeg -i "$(basename $FILE .aac).aac" -acodec libmp3lame "../bass-sectionals-mp3s/$(basename $FILE .aac).mp3";
done
```