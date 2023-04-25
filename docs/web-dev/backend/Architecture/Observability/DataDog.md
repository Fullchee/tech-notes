## Why DataDog

[Datadog: Introducing Datadog in 45 Seconds](https://fullchee-reminders.netlify.app/link/2230)

see everything in one place
- infrastructure
- end-to-end request traces
- prod request profiling
- centralizes all logs

### Alternative to DataDog

DataDog is pricy 🤑

- New Relic
- Sentry?
- Honeycomb
	- Jessica Kerr's company


## Which queries are slow?

1. APM
	1. ![[image-20230405155727127.png]]
2. postgres
3. Traces tab
4. Search `env:env-name` `service:postgres` `operation_name:postgres.query`
5. Update the duration

