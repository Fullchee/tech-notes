
[Video: Django: Where to put business logic ](https://fullchee-reminders.netlify.app/link/2168)

<iframe width="727" height="360" src="https://www.youtube.com/embed/yG3ZdxBb1oo" title="Radoslav Georgiev - Django structure for scale and longevity" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## TLDR

Cherry-pick whatever makes sense to you, based on your specific context.

**Separation of concerns**

- [[#Models]]
	- define data models
	- relationships between models
	- model properties
		- for trivial DB fetches
	- `clean()` validation
		- called with `model_instance.full_clean()`
- [[#Services]]
	- writes to DB
	- Selectors
		- a kind of service that just fetches from DB
		- trivial DB fetches: use model properties
		- can handle permissions, filtering
- [[#Views & APIs]]
	- [YouTube: Django structure#APIs](https://youtu.be/yG3ZdxBb1oo?t=1677)
	- [[#Serializers]]: nested inside the API
		- Python/ORM objects <--> JSON

### TLDR example

```python
class CourseListApi(AuthMixin, APIView):
	class OutputSerializer(serializers.ModelSerializer):
		class Meta:
			model = Course
			fields = ('id', 'name', 'start_date', 'end_date')

	def get(self, request):
		courses = get_courses()  # service or selector
		
		data = self.OutputSerializer(courses, many=True)
		
		return Response(data)
```

???? Would this even work for our use case of nested serialization

> [! Serializer vs ModelSerializer]
> Output serializer: `ModelSerializer` is nice for returning lists
> 
> create/update: only use plain `Serializer`, explicitly state all the fields
> ModelSerializer would handle the creating

```python
class CourseCreateApi(AuthMixin, APIView):
	class InputSerializer(serializers.Serializer):
		name = serializers.CharField()
		start_date = serializers.DateField()
		end_date = serializers.DateField()

	def post(self, request):
		serializer = self.InputSerializer(data=request.data)
		serializer.is_valid(raise_exception=True)

		create_course(**serializer.validated_data)

	return Response(status=status.HTTP_201_CREATED)
```

```python
class CourseUpdateApi(AuthMixin, APIView):
	class InputSerializer(serializers.Serializer):
		name = serializers.CharField(required=False)
		start_date = serializers.DateField(required=False)
		end_date = serializers.DateField(required=False)

	def post(self, request):
		serializer = self.InputSerializer(data=request.data)
		serializer.is_valid(raise_exception=True)

		update_course(course_id=course_id, **serializer.validated_data)

	return Response(status=status.HTTP_201_CREATED)
```

> [!Why inline serializer]-
> changing a base serializer -> could break 5 APIs
> break all the tests

## Notes on abstraction

- If you're putting something the database, use as little abstraction as possible
	- no DRF modelviewsets
	- ?????????
- getting something out of database
	- use as much abstraction as needed

Boxes that Django gives us

- Models
- Views/APIs
- Templates
- Forms / Serializers
- Tasks

## Models

- small @property
	- has_started
	- has_finished
- validation logic with `clean`
	- [[Django Models#[Validating objects](https://docs.djangoproject.com/en/4.1/ref/models/instances/ validating-objects)]]


### Why business logic doesn't belong in Models

- fat models aren't maintainable
	- God object
- models only for data model & relations
- clean() for additional validation
- don't modify `save()` for additional logic

### Testing Models

- custom validations or properties
- tests don't hit db -> fast tests 🏃


## Custom Model Managers and QuerySets

[Django Style guide](https://github.com/HackSoftware/Django-Styleguide#overview): business logic should not live in custom managers or query sets

### When to use custom model managers and querysets?

- like model properties
- use this for simple stuff
	- there might be more complex logic like 3rd party API calls
	- where you should move the logic to services.py

### Custom Model Manager example

[Custom Model Manager & Model QuerySet](https://fullchee-reminders.netlify.app/link/2167)

```python
class PostManager(models.Manager):
	def sorted(self):
		return self.get_queryset().sorted()
```

```python
Post.objects.sorted()
```

`get_queryset` is like `Post.objects.all()`

### QuerySet Manager example

Implement your own `get_queryset`

```python
class PostQuerySet(models.QuerySet):
	def sorted(self):
		return self.order_by('-created_at')
```

so that you can 

```python
Post.objects.all().sorted()
```

## Views & APIs

Django Rest Framework (DRF)

need to put it in the serializer

model view set???

## Serializers

- Python/ORM objects <--> JSON

### Why serializers shouldn't create objects and do business logic

- misleading and confusing when you have to do stuff that the serializer doesn't immediately support
	- update some deep abstraction

separation of concerns

### Why nested Serializers in the view API?

We don't want to reuse serializers, especially for InputSerializers

- output serializer is okay sometimes

Editing a base serializer will break a ton of APIs
- need to reuse serializers with great care

Adding 1 property --> breaking 5 other APIs because they all use the serializer

## Services

### What is a service

- simple function (w/ type hints)
- speaks the domain language
- handles
	- permissions
	- cross-cutting concerns
	- calls other services/tasks
	- works mainly with models


```python
def user_create(
    *,  # keyword only
    email: str,
    name: str
) -> User:
    user = User(email=email)
    user.full_clean()
    user.save()

	# calls other services
    profile_create(user=user, name=name)
    confirmation_email_send(user=user)

    return user
```

### When to use a service
- every non-trivial operation that touches the database should be a service
- no ORM code in your AP

### selectors.py

- business logic around fetching
- not always necessary
handle permissions, filtering, ...


#### Rule of thumb

- if you get the N + 1 problem
	- If your model property starts doing queries on the model's relations
	- which can't be solved with `select_related` or `prefetch_related`
- it should be a selector

example

```python
class Lecture(models.Model):
	@property
	def not_present_students(self):
		present_ids = self.present_students.values_list('id', flat=True)
		
		return self.course.students.exclude(id__in=present_ids)
```

### Testing services
- where the business logic is
- hit the db
- mocking
