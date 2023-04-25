Prod JS code is minified
- fewer bytes to download
- obfuscation (hard to read the code)

TODO: how does sentry do this????

Downsides
- hard to debug

## Why are we debugging prod?

-   staging env not closely mimicking a prod env?
	-   local environments mimicking a prod env?
-   no strong front end error reporting we can trust to get us to the right part of the code which is throwing?
	- eg: Sentry?


## Workaround

- Source map points to the original code hosted on a private server
- that is only available via a VPN?

[[error-boundaries]]
