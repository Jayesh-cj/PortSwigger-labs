# Lab-9: [SQL injection UNION attack, retrieving data from other tables](https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-data-from-other-tables)

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. 

The database contains a different table called users, with columns called username and password. 

**Aim :-** To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user. 


## Solution
- Use the following payload to retrieve the contents of the users table:
    ``` ' UNION SELECT username,password FROM users-- ```
    - ``` UNION ``` will combine the select query with filter search query
    - ``` SELECT username,password FROM users ``` Will return all the usernames and passwords from the users table
    - ``` -- ``` tells SQL to ignore everything after it  
