
[Comparison with SQL](https://pandas.pydata.org/docs/getting_started/comparison/comparison_with_sql.html)

[10 minutes to pandas](https://pandas.pydata.org/docs/user_guide/10min.html)

[Pandas equivalent of 10 useful SQL queries](https://towardsdatascience.com/pandas-equivalent-of-10-useful-sql-queries-f79428e60bd9)

## Using Pandas

### Read a CSV

```python
import pandas as pd
df = pd.read_csv("penguins.csv")
```

### Viewing data

```python
display(df.head())
# display(df.tail(2))
```

|     | species | island    | bill_len_mm | bill_depth_mm | flipper_len_mm | body_mass_g | sex |
| --- | ------- | --------- | ----------- | ------------- | -------------- | ----------- | --- |
| 0   | Adelie  | Torgersen | 39.1        | 18.7          | 181.0          | 3750.0      | M   |
| 1   | Adelie  | Torgersen | 39.5        | 17.4          | 186.0          | 3800.0      | F   |
| 2   | Adelie  | Torgersen | 40.3        | 18.0          | 195.0          | 3250.0      | F   |

```python
display(df.describe())
```

|       | bill_mm    | bill_depth_mm | flipper_mm | mass_g      |
| ----- | ---------- | ------------- | ---------- | ----------- |
| count | 342.000000 | 342.000000    | 342.000000 | 342.000000  |
| mean  | 43.921930  | 17.151170     | 200.915205 | 4201.754386 |
| std   | 5.459584   | 1.974793      | 14.061714  | 801.954536  |
| min   | 32.100000  | 13.100000     | 172.000000 | 2700.000000 |
| 25%   | 39.225000  | 15.600000     | 190.000000 | 3550.000000 |
| 50%   | 44.450000  | 17.300000     | 197.000000 | 4050.000000 |
| 75%   | 48.500000  | 18.700000     | 213.000000 | 4750.000000 |
| max   | 59.600000  | 21.500000     | 231.000000 | 6300.000000 |

### Getting stats on data

```python
# get a single column
# df.bill_length_mm
bill_length = df["bill_length_mm"]

# Series
type(bill_length)

bill_length.mean()
```

    43.9219298245614

### Get a single value: at

```python
# `at` can only get one value, can't return a series
assert df.iat[0, 2] == df.at[0, "bill_length_mm"]
```

### Selecting rows

```python
### ROWS

# df["key1", "key2"]
# in this case, the keys are the row numbers

# loc and at are optimized
# df[0:3]

print("\n")

# like
# assert df.iloc[2] == df.loc[2]

# Rows are also series
row_2 = df.iloc[2]
display(row_2)

# multiple rows is a data fraame
display(df.iloc[2:5])
```

```sql
SELECT DISTINCT species, island
FROM penguins;
```

```python
df[["species", "island"]].drop_duplicates()

# same thing, all rows, 2 columns
# df.loc[:, ["species", "island"]].drop_duplicates()
```

|     | species | island |
| --- | --- | --- |
| 0   | Adelie | Torgersen |
| 20  | Adelie | Biscoe |
| 30  | Adelie | Dream |
| 152 | Chinstrap | Dream |
| 220 | Gentoo | Biscoe |

## New column

```sql
SELECT *, bill_length_mm + bill_depth_mm AS beak_to_eye
FROM penguins;
```

this returns a new data frame, doesn't mutate the existing df

```python
df.assign(beak_to_eye=df.bill_length_mm + df.bill_depth_mm).head()
```

| | species | island | bill\_length\_mm | bill\_depth\_mm | flipper\_length\_mm | body\_mass\_g | sex | beak\_to\_eye |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0   | Adelie | Torgersen | 39.1 | 18.7 | 181.0 | 3750.0 | MALE | 57.8 |
| 1   | Adelie | Torgersen | 39.5 | 17.4 | 186.0 | 3800.0 | FEMALE | 56.9 |
| 2   | Adelie | Torgersen | 40.3 | 18.0 | 195.0 | 3250.0 | FEMALE | 58.3 |
| 3   | Adelie | Torgersen | NaN | NaN | NaN | NaN | NaN | NaN |
| 4   | Adelie | Torgersen | 36.7 | 19.3 | 193.0 | 3450.0 | FEMALE | 56.0 |

## WHERE (filtering)

boolean indexing

```sql
SELECT species, body_mass_g
FROM penguins
WHERE body_mass_g > 6000
  AND species = 'Gentoo'
  AND bill_length_mm IS NOT NULL;
```

```python
# Boolean series
is_chonky = df.body_mass_g > 6000
is_gentoo = df["species"] == "Gentoo"
are_looong = df.bill_length_mm.notna()

all_columns = df[is_chonky & is_gentoo & are_looong]

display(all_columns)
```
| | species | island | bill\_length\_mm | bill\_depth\_mm | flipper\_length\_mm | body\_mass\_g | sex |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 237 | Gentoo | Biscoe | 49.2 | 15.2 | 221.0 | 6300.0 | MALE |
| 253 | Gentoo | Biscoe | 59.6 | 17.0 | 230.0 | 6050.0 | MALE |

```python
# loc: 1st param: filter on rows
# 2nd param: column filter
df.loc[is_chonky & is_gentoo & has_length, ["species", "body_mass_g"]]
```
| species | body\_mass\_g |
| --- | --- | --- |
| 237 | Gentoo | 6300.0 |
| 253 | Gentoo | 6050.0 |

### Get the row with the max

```python
longest_bill_index = df.bill_length_mm.idxmax()

df.iloc[longest_bill_index]
```

```
    species              Gentoo
    island               Biscoe
    bill_length_mm         59.6
    bill_depth_mm          17.0
    flipper_length_mm     230.0
    body_mass_g          6050.0
    sex                    MALE
    Name: 253, dtype: object
```

## Group by

```sql
SELECT AVG(bill_length_mm), COUNT(*)
FROM penguins
GROUP BY species
```

```python
# DataFrameGroupBy
species = df.groupby("species")

# a data frame for each species
# species.apply(display)

# SeriesGroupBy
groupby_column = species["bill_length_mm"]
# groupby_column.apply(display)

# mean() on the SeriesGroupBy only does it that series
display(groupby_column.mean())

# mean() on the DataFrameGroupBy applies it to every column
display(species.mean())
```

    species
    Adelie       38.791391
    Chinstrap    48.833824
    Gentoo       47.504878
    Name: bill_length_mm, dtype: float64


| species   | bill\_length\_mm | bill\_depth\_mm | flipper\_length\_mm | body\_mass\_g |
|-----------|------------------|-----------------|---------------------|---------------|
| Adelie    | 38.791391        | 18.346358       | 189.953642          | 3700.662252   |
| Chinstrap | 48.833824        | 18.420588       | 195.823529          | 3733.088235   |
| Gentoo    | 47.504878        | 14.982114       | 217.186992          | 5076.016260   |

```sql
SELECT COUNT(*)
FROM penguins
GROUP BY species
```

```python
species = df.groupby("species")
# size(): special function that only returns the count of every species
display(species.size())
display(species.count())  # redundant information for every column
```

    species
    Adelie       152
    Chinstrap     68
    Gentoo       124
    dtype: int64
	
	
| species | island | bill\_length\_mm | bill\_depth\_mm | flipper\_length\_mm | body\_mass\_g | sex |
| --- | --- | --- | --- | --- | --- | --- |
| Adelie | 152 | 151 | 151 | 151 | 151 | 146 |
| Chinstrap | 68  | 68  | 68  | 68  | 68  | 68  |
| Gentoo | 124 | 123 | 123 | 123 | 123 | 119 |

```sql
SELECT species, COUNT(*) AS 'count', AVG(bill_length_mm) AS avg_bill_length
FROM penguins
GROUP BY species
ORDER BY avg_bill_length DESC
```

```python
species = df.groupby("species")

# DataFrame, key is the species name
aggregated = species.agg({"bill_length_mm": np.mean, "species": np.size})

renamed = aggregated.rename(columns={"bill_length_mm":"avg_bill_length", "species" : "count"})

renamed.sort_values("avg_bill_length", ascending=False)
```


|     | avg\_bill\_length | count |
| --- | --- | --- |
| species |     |     |
| --- | --- | --- |
| Chinstrap | 48.833824 | 68  |
| Gentoo | 47.504878 | 124 |
| Adelie | 38.791391 | 152 |

### Group by multiple

```sql
SELECT species, COUNT(*) AS 'count', AVG(bill_length_mm) AS avg_bill_length
FROM penguins
GROUP BY species, island
```

```python
species_island = df.groupby(["species", "island"])

# DataFrameGroupBy
# data frame for every unique combo of (species, island)
# aggregated = species_island.apply(display)

# DataFrame with multi-level columns
species_island_bill_length = species_island.agg({"bill_length_mm": [np.size, np.mean]})

display(species_island_bill_length)

# to access the individual columns, you have to get the top name first
display(species_island_bill_length["bill_length_mm"]["mean"])

# or iloc, all rows, the mean column
# species_island_bill_length.iloc[:, 1]
```

    species    island
    Adelie     Biscoe       38.975000
               Dream        38.501786
               Torgersen    38.950980
    Chinstrap  Dream        48.833824
    Gentoo     Biscoe       47.504878
    Name: mean, dtype: float64

### Stack

![image](https://www.w3resource.com/w3r_images/pandas-dataframe-stack-2.png)

Move the multi-column into the index

```python
display(species_island_bill_length)
species_island_bill_length.stack()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th colspan="2" halign="left">bill_length_mm</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>size</th>
      <th>mean</th>
    </tr>
    <tr>
      <th>species</th>
      <th>island</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">Adelie</th>
      <th>Biscoe</th>
      <td>44</td>
      <td>38.975000</td>
    </tr>
    <tr>
      <th>Dream</th>
      <td>56</td>
      <td>38.501786</td>
    </tr>
    <tr>
      <th>Torgersen</th>
      <td>52</td>
      <td>38.950980</td>
    </tr>
    <tr>
      <th>Chinstrap</th>
      <th>Dream</th>
      <td>68</td>
      <td>48.833824</td>
    </tr>
    <tr>
      <th>Gentoo</th>
      <th>Biscoe</th>
      <td>124</td>
      <td>47.504878</td>
    </tr>
  </tbody>
</table>
</div>

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th>bill_length_mm</th>
    </tr>
    <tr>
      <th>species</th>
      <th>island</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="6" valign="top">Adelie</th>
      <th rowspan="2" valign="top">Biscoe</th>
      <th>size</th>
      <td>44.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>38.975000</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Dream</th>
      <th>size</th>
      <td>56.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>38.501786</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Torgersen</th>
      <th>size</th>
      <td>52.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>38.950980</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Chinstrap</th>
      <th rowspan="2" valign="top">Dream</th>
      <th>size</th>
      <td>68.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>48.833824</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Gentoo</th>
      <th rowspan="2" valign="top">Biscoe</th>
      <th>size</th>
      <td>124.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>47.504878</td>
    </tr>
  </tbody>
</table>
</div>

## HAVING

```sql
SELECT island
FROM penguins
GROUP BY island
HAVING COUNT(species) > 1
```

```python
islands = df.groupby(["island"])
islands = islands.filter(lambda x: x["species"].drop_duplicates().count() > 1)

islands
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>species</th>
      <th>island</th>
      <th>bill_length_mm</th>
      <th>bill_depth_mm</th>
      <th>flipper_length_mm</th>
      <th>body_mass_g</th>
      <th>sex</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20</th>
      <td>Adelie</td>
      <td>Biscoe</td>
      <td>37.8</td>
      <td>18.3</td>
      <td>174.0</td>
      <td>3400.0</td>
      <td>FEMALE</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Adelie</td>
      <td>Biscoe</td>
      <td>37.7</td>
      <td>18.7</td>
      <td>180.0</td>
      <td>3600.0</td>
      <td>MALE</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Adelie</td>
      <td>Biscoe</td>
      <td>35.9</td>
      <td>19.2</td>
      <td>189.0</td>
      <td>3800.0</td>
      <td>FEMALE</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Adelie</td>
      <td>Biscoe</td>
      <td>38.2</td>
      <td>18.1</td>
      <td>185.0</td>
      <td>3950.0</td>
      <td>MALE</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Adelie</td>
      <td>Biscoe</td>
      <td>38.8</td>
      <td>17.2</td>
      <td>180.0</td>
      <td>3800.0</td>
      <td>MALE</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>339</th>
      <td>Gentoo</td>
      <td>Biscoe</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>340</th>
      <td>Gentoo</td>
      <td>Biscoe</td>
      <td>46.8</td>
      <td>14.3</td>
      <td>215.0</td>
      <td>4850.0</td>
      <td>FEMALE</td>
    </tr>
    <tr>
      <th>341</th>
      <td>Gentoo</td>
      <td>Biscoe</td>
      <td>50.4</td>
      <td>15.7</td>
      <td>222.0</td>
      <td>5750.0</td>
      <td>MALE</td>
    </tr>
    <tr>
      <th>342</th>
      <td>Gentoo</td>
      <td>Biscoe</td>
      <td>45.2</td>
      <td>14.8</td>
      <td>212.0</td>
      <td>5200.0</td>
      <td>FEMALE</td>
    </tr>
    <tr>
      <th>343</th>
      <td>Gentoo</td>
      <td>Biscoe</td>
      <td>49.9</td>
      <td>16.1</td>
      <td>213.0</td>
      <td>5400.0</td>
      <td>MALE</td>
    </tr>
  </tbody>
</table>
<p>292 rows × 7 columns</p>
</div>

## SQL in Pandas

```python
import sqlite3
conn = sqlite3.connect("penguins.db")
peaks = pd.read_sql("""
    SELECT MIN(body_mass_g)
    FROM penguins
    WHERE species = 'Gentoo'""",
conn)

peaks
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MIN(body_mass_g)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3950</td>
    </tr>
  </tbody>
</table>
</div>

```python
import pandas as pd
import sqlalchemy as sql

engine = sql.create_engine(os.environ["DATABASE_URL"])

df = pd.read_sql_query(
        sql.text(
            """
        SELECT *
        FROM penguins
        """
        ),
        engine,
    )
```
