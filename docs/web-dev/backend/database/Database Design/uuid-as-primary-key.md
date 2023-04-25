# UUID as primary key?

## Problems with an auto incrementing key

1. IDs are usually exposed
    - So if someone wants to know how many users you have, they just have to create a new user
2. If you're monkeying in the db, you can't accidentally delete a row in another table

## Why not a UUID

-   isn't this bad for cluster indexes?
-   you could use a UUID v1
    -   that would expose a date
