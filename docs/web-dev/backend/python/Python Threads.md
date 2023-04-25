ll[ThreadPoolExecutor in Python: The Complete Guide](https://superfastpython.com/threadpoolexecutor-in-python/)

`.submit()` creates a future object


```python
with ThreadPoolExecutor() as pool:
	# run each function in a separate thread, doesn't block
	for future in [
		pool.submit(my_func, arg1, arg2),
		pool.submit(my_func, arg1),
	]:
		result = future.result()
		# can also timeout future.result(timeout=5)
```

