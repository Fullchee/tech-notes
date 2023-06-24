Loom
- screen recording with a nicer UI & cropping tool than the default screen recorder


## Cropping

### Preview

- can trim the front or end of the video

### Lossless cut

Good for cutting middle sections of the video

### ffmpeg

```sh
function mp4slice() {
	ffmpeg -ss "$2" -i "$1" -t "$3" -vcodec copy -acodec copy splice.mp4
}
```


## HandBrake
- to compress the images


iMovie
- 



