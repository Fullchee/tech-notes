>[!SUM(COALESCE(col1)) vs COALESCE(SUM(col1))]
>?

PyCharm complains about
SUM(COALESCE(col1))
- it converts it into a CASE statement