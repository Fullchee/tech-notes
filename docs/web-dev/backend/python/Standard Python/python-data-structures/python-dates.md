# Python Dates

```python
from datetime import datetime

>>> datetime.now()
datetime.datetime(2022, 8, 11, 19, 15, 16, 561797)
```


## Time intervals

We can do time delta in days

```python
from datetime import datetime, timedelta

t0 = datetime(year=2022, month=1, day=1)
t1 = datetime(year=2022, month=8, day=11)

diff = t1 - t0
>>> diff
datetime.timedelta(days=222)
>>> diff.total_seconds()
19180800.0
```

### Time delta in days instead of seconds

```python
days = diff / timedelta(days=1)

>>> days
222.0
```


### Subtract a month from a date

```python
from datetime import date
from dateutil.relativedelta import relativedelta


>>> date.today()
datetime.date(2022, 11, 9)

>>> date.today() - relativedelta(months=1)
datetime.date(2022, 10, 9)
```