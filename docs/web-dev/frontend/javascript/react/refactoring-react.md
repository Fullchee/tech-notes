# Refactoring React

### State that depends first on `props` and then on `useEffect` 💩

GET `/dashboard/<ID>` will get a JSON response

```json
{
    "dashboard": {
        "id": 9,
        "name": "Dashboard name",
        ...
}
```

GET `/dashboard` will get the same JSON response

```jsx
const DashboardRenderer = ({ urlId }) => {
// init
const [backendId, setBackendId] = useState(urlid);
const dashboard = useSelector({dashboards} => dashboards[backendId]);

const dispatch = useDispatch();
useEffect(() => {
		loadDashboard(dispatch, backendId).then(({ data }) => {
			setBackendId(data.id);
		});
	});
}, [dispatch, backendId]);
```

1. First render: `urlId` is `null`
2. `useEffect` is called
    1. It sets the `backendId` state which triggers a re-render
3. Second re-render: runs the `useEffect` again
    1. makes another API call

How to only make one API call?

### Solution: only use the `prop` in the `useEffect`

```diff
const DashboardRenderer = ({ urlId }) => {
// init
const [backendId, setBackendId] = useState(urlId);
const dashboard = useSelector({dashboards} => dashboards[backendId]);

const dispatch = useDispatch();
useEffect(() => {
- 		loadDashboard(dispatch, backendId).then(({ data }) => {
+ 		loadDashboard(dispatch, urlId).then(({ data }) => {
			setBackendId(data.id);
		});
	});
- }, [dispatch, backendId]);
+ }, [dispatch, urlId]);
```

## `UnknownObject` as a dependency in `useEffect`

It makes an API call every time 😞

-   when a new object is created
-   it has a new pointer

```jsx
const Component = ({queryParams}) => {

  useEffect(() => {
    fetch("example.com?" + new URLSearchParams(...queryParams));
  }, [queryParams]);
  ...
};
```

### Solution

1. Store the serialized (`JSON.stringify`) object’s previous value
2. If the current serialized value is different than before
	1. make an API call

```jsx
const Component = ({ queryParams }) => {
    const previousValue = usePrevious(JSON.stringify(queryParams));
    useEffect(() => {
        if (JSON.stringify(queryParams) !== previousValue) {
            fetch("example.com?" + new URLSearchParams(...queryParams));
        }
    }, [queryParams]);
};
```


```jsx
<button onClick={handleClick || undefined}
```


Don't need the undefined


## Returning undefined

```jsx
function MyComp() {
	const canView = useFeatureToggle('feature');
	return canView && <div>Hi</div>
}
```

Components can't return undefined

It was a way to catch errors
- since you likely didn't mean to return undefined
- likely forgot a return statement
- or forgot to return something
- if you don't want to render anything, you can return `null`

```diff
function MyComp() {
	const canView = useFeatureToggle('feature');
-   return canView && <div>Hi</div>
+	return canView ? <div>Hi</div> : null
}
```

[components rendering undefined](https://github.com/reactwg/react-18/discussions/75)