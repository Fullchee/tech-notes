# React Query

https://fullchee-reminders.netlify.app/link/2090

[React Query: a Server State Manager](https://tkdodo.eu/blog/react-query-as-a-state-manager)

## What problem does it solve?

1. Fancy fetch
	1. caching, retrying and a bunch of this logic
2. server data sync
	1. smartly refreshes your data
		- refetchOnMount
			- can set a custom `staleTime` if you don't like the default behaviour
		- refetchOnWindowFocus
		- refetchOnReconnect

## Setup

```js
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      // ✅ globally default to 20 seconds
      staleTime: 1000 * 20,
    },
  },
})

// 🚀 everything todo-related will have a 1 minute staleTime
queryClient.setQueryDefaults(todoKeys.all, { staleTime: 1000 * 60 })

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <ComponentOne />
      <ComponentTwo />
    </QueryClientProvider>
  )
}
```


## Usage

```js
export const useTodos = () =>  // custom hook!
  useQuery({ queryKey: ['todos'], queryFn: fetchTodos })

function ComponentOne() {
  const { isLoading, error, data, isFetching } = useTodos()
  return (
	  <React.Suspense fallback={}
  )
}
```

instead of doing it yourself with `useEffect`

has browser dev-tools

React Query probably uses an Abort Controller

```diff title="useFetch.jsx"

export function useFetch(url) {
	const [loading, setLoading] = useState(true)
	const [data, setData] = useState()
	const [error, setError] = useState()

	useEffect(() => {
+		const controller = new AbortController()
	    setLoading(true)
- 	    fetch(url)
+       fetch(url, { signal: controller.signal })
	        .then(setData)
	        .catch(setError)
	        .finally(() => setLoading(false))
+       return () => {
+           controller.abort()
+       }
+   }, [url])
	return { loading, data, error }
}

```

When would you need to use xState?

- super complex user state logic