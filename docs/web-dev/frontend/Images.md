## Image resources

#### Get an image from Unsplash

-   https://source.unsplash.com/random/300×300


### Bookmarklet to lint images 
- https://ausi.github.io/respimagelint/

## Cloudinary

Can transform images on the go by updating the URL

I personally don't use it to the fullest on my portfolio site

### [Cloudinary and Next.JS](https://spacejelly.dev/posts/how-to-use-cloudinary-images-in-next-js-with-blurred-placeholders/)


## Image formats

[[SVG]]

[Using Modern Image Formats: AVIF And WebP — Smashing Magazine](https://www.smashingmagazine.com/2021/09/modern-image-formats-avif-webp/)

### AVIF
- go-to image format
- replaces JPEG, PNG, GIF
	- animation
	- alpha transparency
	- lossy or lossless
- Good support since 2022
- better compression for photograph pictures than WebP

### WebP
- more support than AVIF
- faster encode/decoding than AVIF

### Progressive enhancement

```html
<picture>
 <source srcset="img/photo.avif" type="image/avif">
 <source srcset="img/photo.webp" type="image/webp">
 <img src="img/photo.jpg" alt="Description" width="360" height="240">
</picture>
```
### Can't use AVIF nor WebP

- MozJPEG (optimize JPEG images)
- OxiPNG (non-photographic images)
- JPEG 2000 (lossy or lossless photographic images)


![AVIF vs WebP](https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3e168f7-0c9a-46dc-be3d-bd379be6ad7b/modern-image-formats-3.png)

## Display different images depending on light/dark mode

probably the `picture` element