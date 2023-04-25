## What

Query language

a way to get data from your database/server to the frontend

## Problems that it solves

1. Frontend can get the exact data it needs in 1 API call
	1. use case: Facebook mobile app
	2. no long chain of API calls
	3. no under/over fetching
2. typing
	1. know the types of the data you need
3. Federation
	1. Syntax.FM

If you have siloed frontend & backend teams
* they can work independently
* frontend can mock the GraphQL server and just get the data they need
* the backend can implement the GraphQL server independently

## Metaphor

Subway: make it your way! (with limits)

In & Out: pick from options (REST)

## Downsides

- setting up a GraphQL server is more complex
	- write your own reducers
	- or use a service
- making a request to a GraphQL server is more complex
	- need a library to generate the queries
	- or you have complex query params
- less likely to get cache
- need to address the [[N + 1 Problem]]
	- [dataloader](https://github.com/graphql/dataloader)
- 