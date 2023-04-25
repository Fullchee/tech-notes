## Mac

```sql
brew install postgres
```


## Windows

1. `choco install postgres`
	1. [Chocolatey Software | PostgreSQL](https://community.chocolatey.org/packages/postgresql)
2. Change the default password
	1. [Arctype Connect - Reset Password on Windows](https://arctype.com/postgres/setup/reset-password-windows)
	2. if you don't know the password
	3. change it to trust `pg_hba.conf`
	4. `ALTER USER postgres WITH PASSWORD 'new_password';`
3. Create a superuser
	1. with the same name as your Windows user
	2. `psql -U postgres`
	3. `CREATE USER fullchee SUPERUSER`
	4. then exit and run
	5. `createdb fullchee`