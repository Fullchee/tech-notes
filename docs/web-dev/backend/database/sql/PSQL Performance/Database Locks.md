
## Types of locks

[Hussein Nasser: Locks in Postgres](https://fullchee-reminders.netlify.app/link/2224)

- Table lock
- row lock

### [Hussein Nasser: Exclusive row lock vs Shared row lock](https://fullchee-reminders.netlify.app/link/2208)

Exclusive lock
- others can't read

Shared lock
- others can't write


### [Advisory Locks](https://shiroyasha.io/advisory-locks-and-how-to-use-them.html)

lock with application defined meaning

- ideal candidate for concurrency control where the standard MVCC doesn't fit the bill
	- what is MVCC??? 
- example: restores: lock that commissions run ID
	- prevent another restore from restoring that same commissions run ID at the same time

#### Session advisory lock

- held until
	- session ends
	- lock is released manually
		- `SELECT pg_advisory_unlock(10);`
- avoid session locks????
	- A lock acquired in a transaction will hold even if the transaction rollbacks!!!
	- Transaction semantics are not honoured for session locks????

```sql
SELECT pg_try_advisory_lock(10);  -- 64-bit number
SELECT pg_try_advisory_lock(1, 2);  -- two 32-bit numbers
```

#### Transaction advisory lock


- transactional advisory lock acquired in a transaction will be released when the transaction ends

```sql
SELECT pg_try_advisory_xact_lock(:id1, :id2)
```

#### Listing advisory locks

```sql
SELECT mode, classid, objid FROM pg_locks WHERE locktype = 'advisory';
```


#### Example uses of advisory locks
- Restoring a commissions run
	- guarantee that there aren't two restores trying to restore the same commissions run
		- will mess with the calculations
-  coordinate access to some shared resource or a 3rd party services 
	- guarantee that only one node can access it at a time


## What causes a lock?

- DML statement
	- `INSERT INTO table (...) VALUES(...)`
	- `UPDATE table SET ... WHERE ...`
	- `DELETE FROM table WHERE ...`
- DDL statement
	- `CREATE TABLE ...`
	- `ALTER TABLE ...`
		- exclusive lock
	- will still allow writes
- (auto) [[PSQL Vacuum]]
- indexing????
- explicitly
	- `BEGIN: LOCK TABLE ... IN MODE`

## Identifying lock problems

- slow queries
- low resource usage
	- low I/O usage


### Debugging live

- `pg_locks`
- `pg_stat_activity`

```sql
SELECT *
FROM pg_stat_activity
WHERE wait_event_type = 'Lock'
```

[Hacks o’Clock: Blocked by rdsadmin](http://hacksoclock.blogspot.com/2016/01/blocked-by-rdsadmin.html)

### Debugging when gathering stats

- pgbadger
	- make sure you have some extra space
- if you're on RDS
	- make sure you're not maxed out on IOPS
	- logs and data are on the same device
- ![[image-20221129212634999.png]]
![[image-20221129212803067.png]]

What it doesn't do
- For each query, what other query is blocking it?
	- need to do some live debugging


## Common locking problems

### (auto)vaccum prevents running DDL

or DDL prevents autovacuum

#### How do you know you have this problem

????

#### autovaccum and DDL lock fix
- don't disable autovacuum 
	- [[PSQL Vacuum#Why autovacuum should always be on]]
- Give autovacuum more resources
	- so it finishes faster, more often
- split up large tables
	- partition or archive

#### Autovaccum freeze

- process name has: "to prevent xid wraparound"
- PSQL has 32 bit transaction IDs
	- easy to use them all
- autovacuum has to periodically recycle old IDs
- can't kill it
	- will get revived right away
	- super important for database

##### Autovaccum freeze fix
- vacuum tuning
- [Hacks o’Clock: Blocked by rdsadmin](http://hacksoclock.blogspot.com/2016/01/blocked-by-rdsadmin.html)


### `SELECT ... FOR UPDATE` overuse

- blocks writes to those rows
- when someone tries to implement a queue in psql
	- don't do that

### Idle in Transaction

```sql
SELECT *
FROM pg_stat_activity
WHERE state = 'idle in transaction'
```

1. someone starts a transaction with `BEGIN`
2. forgets to commit the transaction

Blocks autovacuum

#### Idle in Transaction fix

- find the app code and make sure it calls `COMMIT`
- `idle_in_transaction_session_timeout = 2min`

### Long DDL Locks

fixed in PostgreSQL 11

When you add/alter a column that's
- NOT NULL
- with a default

```sql
ALTER TABLE my_Table
ADD COLUMN my_col text NOT NULL DEFAULT 'blah';
```

Problem
- takes an AccessExclusiveLock
- rewrites the whole table

Fix (for pre PostgreSQL 11)
- see video [PostgreSQL Locking issues](https://youtu.be/OUHsBuXzdwk?t=1149)
