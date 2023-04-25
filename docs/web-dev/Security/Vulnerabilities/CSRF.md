cross site request forgery


## Example

blog (or embedded element): click a link to

bank.com/transfer?to=124&amount=1000

already logged in to bank.com => it'll work


## Avoiding a CSRF attack

1. Same site cookie
	1. (Default is lax??)
2. CSRF token
	1. hidden input in form
	2. Nonce
3. HTTP only cookies
4. Backend can check origin referrer header
5. Captcha
