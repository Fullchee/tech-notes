Performance for free

1. multiplexing
	1. one TCP connection to get all assets
	2. each request has a stream ID
	3. ![[image-20221023191307452.png]]
	4. no need for HTTP/1 hacks
		1. image sprites
		2. bundling your JS into 1 file
2. Compressed (binary)
	1. HTTP/1 is in plain text
3. server push
	1. can send resources before HTML is fully parsed

You can also cancel requests!

