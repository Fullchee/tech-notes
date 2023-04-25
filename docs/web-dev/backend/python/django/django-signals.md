# Django Signals

## Use cases

Permissions: `post_save` --> assign to "Superuser" role


```python title="models.py"
from django.db.models.signals import pre_save
from django.dispatch import receiver


@receiver(pre_save, sender=Comment)
def do_something_on_save(sender, instance, **kwargs):
	
	# previous value
	print(sender.objects.get(id=instance.id))
	# new value
	print(instance)
```