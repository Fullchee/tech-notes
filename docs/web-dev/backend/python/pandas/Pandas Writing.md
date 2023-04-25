
## Write to a SQL database

[pandas.DataFrame.to_sql](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_sql.html)

### Connect to the db

```python
import sqlalchemy as sql

engine = sql.create_engine("DATABASE_URL")
connection = engine.connect()
```

### Save to the db

```python
result = []
df = pd.DataFrame(result)
df.to_sql(name="table_name",
		  con=connection,
		  index=False,
		  if_exists='replace',  # or append
)
```
