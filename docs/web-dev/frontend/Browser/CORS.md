Cross Origin Resource Sharing

[Hasty Treat - JSON, JSONP and CORS — Syntax Podcast 063](https://syntax.fm/show/063/hasty-treat-json-jsonp-and-cors)

## Why CORS

Access resources (other than JS) from other domains

Examples

- JSON from any other server
- images from Cloudinary
- fonts from Google Fonts


## [Preflight request](https://developer.mozilla.org/en-US/docs/Glossary/Preflight_request)

### What

HTTP `OPTIONS` request to check whether the server understands CORS

Browser will not send the cross origin request if the server doesn't understand CORS

### Why

Prevent new ways to CSRF to an old pre-CORS server

- no preflight request for old kinds of requests
	- like POST request to get some JS
	- POST request to get JSON will send a preflight

#### Why preflight for every request

URLs could be handled by different servers

- `bank.com/login`
- `bank.com/account`

so it has to be for every request



## JSONP

Since you could request cross origin JS

you wrap JSON in some JS