

```sh
function mp4slice() {
	ffmpeg -ss "$2" -i "$1" -t "$3" -vcodec copy -acodec copy splice.mp4
}
```