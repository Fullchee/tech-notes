## Date to string

```javascript
> date.toLocaleDateString();
'2022-09-08'
```

## Handle month offset

Example

-   Fiscal year starts in April (month offset = 3)

Useful for getting the quarter

```javascript
date = new Date("Jan 17, 1995"); // Jan is actually Q4
offset = 3;
date.setMonth(date.getMonth() - offset) > date;
1994 - 10 - 17;
```

### [Temporal API](https://blog.webdevsimplified.com/2022-02/temporal-date-api/)
