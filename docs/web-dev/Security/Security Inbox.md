**TryHackMe: OWASP Juicebox**

[5 developer tools for detecting and fixing security vulnerabilities](https://dev.to/opinionatedpie/5-developer-tools-for-detecting-and-fixing-security-vulnerabilities-h1j?utm_source=pocket_mylist)

https://web.dev/security-headers/

SRI: Sub-resource Integrity

```html
<script
  src="//cdnjs....."
  integrity="sha256-..." 
  crossorigin="anonymous">
```

if the CDN gets hacked, then the script won't run