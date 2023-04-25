[Fullchee Values](https://fullchee-reminders.netlify.app/link/1740)

Single direction
- SOAP
- REST
	- send whatever data & JSON you want
	- scales, every request will have
	- just uses HTTP
- [[GraphQL]]
- tRPC

Bi-directional
- WebSockets



Raw TCP
- Databases invent their own protocol

## Client libraries

[Fullchee Values](https://fullchee-reminders.netlify.app/link/1740)

The server sends data in a specific format

The client library knows how to read that specific format

the browser has a client library to read HTTP requests
- establish connection
- negotiates, TLS
- checks that the server supports HTTP/2
	- otherwise falls back to HTTP/1
- does the headers, streams
Hard to maintain and patch client libraries
- curl: built in 1996 and still adding new support for different protocols, features
- [[gRPC]] standardized the client library

