# Database Security
- security important bc they store massive amounts of sensitive data
- security varies depending on type of database (nosql, sql)

## Relational DB Access Control
- SQL commands:
- `GRANT`
    - syntax:
    - ex: `GRANT SELECT ON ANY TABLE TO Alice`
```sql
GRANT {privileges | role}
[ON table]
TO {user | role | public}
[IDENTIFIED BY password]
[WITH GRANT OPTION]
```

- `REVOKE`
    - syntax:
    - ex: `REVOKE SELECT ON ANY TABLE FROM Alice`
```sql
REVOKE {privileges | role}
[ON table]
FROM { user | role | PUBLIC}
```
- cascading authorizations - if root user that gave authorization gets permissions revoked, then users who are given access by the root user should also get their permissions revoked

## SQL Injections
- malicious SQL commands sent to database
- in a webapp environment, script takes user input and builds a SQL query
    - can be used to craft SQL injection
- example:

```sql
Var Shipcity;
Shipcity = Request.form (“Shipcity”);
Var sql = “ select *
from OrdersTable
where Shipcity = ‘” + Shipcity + “‘
”;
```
- user can enter `Redmond’ ; DROP table OrdersTable;`
    - then entire orders table is dropped!

### SQL Injection Defenses
- sanitize inputs!
- used prepared statements

## Inference Attacks on DBs
- suppose student can run average score query on database
    - attacker wants exact score of certain student
    - a student takes exam late
        - simply can check average score before vs after, and score can easily be found
### Defense Against Inference Attacks
- don't allow aggregate query results when returned result is too small 
- transform data by removing identifying info