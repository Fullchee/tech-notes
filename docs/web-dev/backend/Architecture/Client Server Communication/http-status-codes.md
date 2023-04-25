# HTTP status codes

[List of HTTP status codes - Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

|                                                                                |                                                                       |
| ------------------------------------------------------------------------------ | --------------------------------------------------------------------- |
| [201 Created](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/201)    |                                                                       |
| [202 Accepted](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/202)   | Request has been accepted for processing, example: export as XLSX/CSV |
|                                                                                |                                                                       |
| [204 No Content](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/204) | Save/update and continue, response for a `PUT`                        |

301
- permanent redirect
- only good for SEO

|                                                                                        |                                                                                             |
| -------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| [400: Bad Request](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/400)       |                                                                                             |
| [401: Unauthorized](https://developer.mozilla.org/en-US/docs/Web/HTTP/401)             | Not logged in                                                                               |
| [402: Payment Required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402)  | **Non Standard!** Paywall, Garmin: uses this when it should use a 403                       |
| [403: Forbidden](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/403)         | Need to be logged in or you don't have the permissions                                      |
| [409: Conflict](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/409)          | example: version control conflict (uploading file that's older than the file on the server) |
| [429: Too many requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/429) |                                                                                             |


- 502
	- bad gateway
	- proxy got a bad response from the other server
	- storybook.formaai.com: when Jenkins is out of memory

## Python

### Django

### [Requests](https://pypi.org/project/requests/)

https://stackoverflow.com/a/61463451

`response.raise_for_status()` throws an error on any 400+ status code

`response.ok` is a boolean of whether the status code is less than 400

```python
response = requests.get(url)
response.raise_for_status()
```
