1. have to send username & pass for every request
2. can't log out unless you close the browser
	1. (no way to invalidate the session from the server side)
	2. unless you change their password?


Why do you have to base64 encode the username and password

to escape special characters



Cons

- no way to invalidate sessions
- except to change their password on them
- or implement black lists
	- which is basically implementing sessions