[anthonywritescode: when should I pin deps: never and always! (intermediate) anthony explains #514 - Reminders](https://fullchee-reminders.netlify.app/link/2265)

## Libraries

`cfgv>=2.0.0`

Lower bound for your libraries

### Why not `cfgv>=2.0.0,<3.0`

Common use cases of library likely will likely still work

the `<3.0` would cause conflicts for people that need the functionality?????


`cfgv>=2.0.0,!3.0.0`

if there's a bug that will likely get fixed

### 
python_requires = >=3.7,<3.11

- won't be installable in Python 3.11
- when it probably still works

Application
- we need to freeze
- use pip tools