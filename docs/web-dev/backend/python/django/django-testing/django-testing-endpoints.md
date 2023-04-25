# Django Testing Endpoints

## [Writing a basic test](django-testing.md#writing-a-basic-test)

## Generating the URL with `reverse()`

`reverse()` uses the name in `urls.py`

```python title="urls.py"
from django.urls import path
from . import views

urlpatterns = (
	path("dashboard_query/<int:query_id>", views.run_dashboard_query, name="run_dashboard_query"),
```


### Adding query params to `reverse()`

kwargs: 

for a URL like `/dashboard/<int:dashboard_id>`, you could pass `*args` or `**kwargs` to set the `dashboard_id`

```python title="test_endpoint.py"
from django.urls import reverse
from django.test import TestCase
from django.utils.http import urlencode


class TestEndpoint(TestCase):
	def _make_api_call(self, kwargs=None, query_kwargs=None):
	""" args/kwargs: keys in the path """
		"GET /app/dashboard_query/<query_id>"
		url = reverse("run_dashboard_query", kwargs=kwargs)
		if query_kwargs:
		    url = f"{url}?{urlencode(kwargs)}"
		return self.client.get(url)
```

## Auth

```python
@classmethod
    def setUpTestData(cls):
        cls.user = UserFactory(is_superuser=True)
```

```python
self.client.force_login(self.user)
```

### HTTP Headers

[Client.get docs](https://docs.djangoproject.com/en/3.2/topics/testing/tools/#django.test.Client.get)

set HTTP headers with kwargs prefixed with `HTTP_`

```python
# HTTP header will have `secret=...`
response = self.client.get(reverse("endpoint"), HTTP_SECRET=settings.SECRET)
```

## Test endpoint with vanilla Django

```python title="test_endpoint.py"
from django.test import TestCase
from django.urls import reverse
from django.utils.http import urlencode
from rest_framework import status

class TestEndpoint(TestCase):
    def test_endpoint(self):
	    # Arrange
        user = UserFactory(is_superuser=False)

		# Act
	    self.client.force_login(user)
        response = self._make_api_call({'query_id': 1})

		# Assert
        self.assertEqual(response.status_code, status.HTTP_200_OK)
        data = response.json()
```

### [Django Rest Framework helpers](https://www.django-rest-framework.org/api-guide/testing/)

#### `status`

-   easier to read
-   so that you don't have to memorize HTTP status codes

```python
from rest_framework import status

self.assertEqual(response.status_code, status.HTTP_201_CREATED)
```

#### `APITestCase` and `APIClient`

##### vs vanilla Django

1. Nicer API to edit the header
    1. example: adding a `SECRET` to the HTTP header
2. the API is slightly nicer for JSON data

Vanilla Django

```python
self.client.post(
            reverse("create_or_get_dashboard"),
            json.dumps(new_dashboard_data),
            content_type="application/json",
        )
```

DRF

```python

self.client.post(
            reverse("create_or_get_dashboard"),
            new_dashboard_data,
            type="json",
        )
```

`APITestCase` overrides `self.client` with [`APIClient`](https://www.django-rest-framework.org/api-guide/testing/#apiclient)

###### `force_authenticate` vs `force_login`

TODO: ask a StackOverflow question

```diff title="test_endpoint.py"
- from django.test import TestCase
+ from rest_framework.test import APITestCase

- class TestEndpoint(TestCase):
+ class TestEndpoint(APITestCase):
    def test_endpoint(self):
	    # Arrange
        user = UserFactory(is_superuser=False)

		# Act
-	    self.client.force_login(user)
+       self.client.force_authenticate(user)
        response = self._make_api_call(kwargs={'query_id': 1}, query_kwargs={"year": 2022})

		# Assert
        self.assertEqual(response.status_code, 200)
        data = response.json() # or response.data
```

### [Request Factories](https://www.django-rest-framework.org/api-guide/testing/#apirequestfactory)

able to have a logged in user

-   unlike Django’s `RequestFactory`

Pros

-   You directly import & run your views
-   so in your code editor, you can click into the view
    -   instead of copying the url string name
    -   and searching for it in `urls.py`

Cons

-   a bit more boilerplate

-   you should still generate the correct the URL with `reverse()`
    -   (because the request that you pass to the view still needs to have a valid URL)
- 

```python title="test_with_api_request_factory.py"
from rest_framework.test import APITestCase, APIRequestFactory, force_authenticate
from .views import run_query_view

class TestEndpoint(APITestCase):
	def setupTests(self):
		self.factory = APIRequestFactory()
	def create_request(endpoint: str, user: User, query_params: Dict = None):
	    request = factory.get("/app_name/some_path")
	    # vanilla Django can only do request.user = user
	    force_authenticate(request, user)
	    response = run_query_view(request)
```

????

self.factory.get()