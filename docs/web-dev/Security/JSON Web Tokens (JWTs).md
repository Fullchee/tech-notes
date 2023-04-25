
server to server Authorization
- you're the same user that logged in before

API authentication
- right username and pass

[Intro to JWT](https://fullchee-reminders.netlify.app/link/2173)

[Don't use JWTs for Auth](https://fullchee-reminders.netlify.app/link/2172)


## Why

- Server doesn't need to store sessions
- no Redis 


## When to use

- SSO
	- logging into bank server
	- logging into retirement/investment server
	- where both servers have the same shared secret
	- although you could just have the same shared Redis instance with all the sessions
- server-to-server authorization
- API authorization
	- when you register to use an API, they give you a secret JWT

## Cons

- can't invalidate sessions
	- if someone's session is hijacked


## How to store a JWT

- HTTP only cookie