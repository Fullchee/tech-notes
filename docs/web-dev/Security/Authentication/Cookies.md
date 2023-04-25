`set-cookie`

- [How Linus Tech Tips got hacked - YouTube](https://youtu.be/ASfMqrE0ISg)
	- session hijacking
	- malware browser extension
	- decrypts the cookie stored in SQLite
		- same process as Chrome
	- use a VPN to pretend that you're in Vancouver
	- refresh token and access token are stored as cookies
- [How Loom Leaked Session Cookies - YouTube](https://www.youtube.com/watch?v=iPXLk5Fk1-U)
	- send cookie to CDN (reverse proxy)
	- the CDN caches the set-cookie:x+1