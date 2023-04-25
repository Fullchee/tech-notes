# Django HTTP

## JsonResponse

At Forma, we had a custom `JsonResponse`

[`JsonResponse` docs](https://docs.djangoproject.com/en/4.1/ref/request-response/#jsonresponse-objects)

```python
response = JsonResponse({'foo': 'bar'}, status=200)
```

Returning an array

-   security vulnerability before ES5
-   you should return an object anyway
    -   easier to add/remove stuff in the future

```python
response = JsonResponse([1, 2, 3], safe=False)
```
