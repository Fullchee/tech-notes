## SQL Injection

aka SQLi

![[image-20221201103417882.png]]



end users can run arbitrary SQL on your database

### Types

- Boolean based
	- `/employees?name=xyz'; OR 1=1--`
	- gets all the employees
- time based
	- `/employees?name=xyz'; SELECT pg_sleep(5)--`
	- will return a 500 error after 5 seconds
	- if you do this a ton of times --> connection exhaustion
	- dangerous because it's silent
-  data tampering
	- `/employees?name=xyz'; UPDATE employees_employee SET `

CVE
- common vulnerabilities and exploits

[CVE - PostgreSQL](https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=postgres)



Use ORMs


```diff
Employee.objects.raw(f"""
  SELECT name FROM employee WHERE
-  name='{name}'"""
+  name=%s""", name
)
```