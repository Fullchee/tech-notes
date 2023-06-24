## Cropping audio

### ffmpeg
```sh
function mp3slice() {
    if [ -z "$1" ] ; then
        echo 'Usage: mp3slice input.mp3 HH:MM:SS.mmm HH:MM:SS:mmm output.mp3'
        return
    fi
    ffmpeg -i "$1" -ss "$2" -to "$3" -c copy "$4"
}
```


```sh
function concatmp3() {
	if [ -z "$3" ] ; then
		echo 'Usage: concatmp3 file1.mp3 file2.mp3 output.mp3'
		return
	fi
	ffmpeg -i "concat:$1|$2" -acodec copy "$3"
}
```

## Audacity
silence parts


eqMac
- remove bass when listening to music (Spotify) 