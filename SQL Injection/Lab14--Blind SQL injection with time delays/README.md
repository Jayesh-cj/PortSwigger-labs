# Lab-14: [Blind SQL injection with time delays](https://portswigger.net/web-security/sql-injection/blind/lab-time-delays)

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie. 

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information. 

**Aim :-** To solve the lab, exploit the SQL injection vulnerability to cause a 10 second delay. 



## Solution
- Capture the request in **burp suite** and add ``` '||pg_sleep(10)-- ``` in the end of the **TrackingId cookie**, send the request and observe that the server takes 10 seconds delay to respond

**Explanation**
- Here the original query may look like the following
    ```  SELECT * FROM tracking WHERE id = '<tracking-cookie>' ```

- While adding the payload the query will change to the following
    ```  SELECT * FROM tracking WHERE id = '<tracking-cookie>'||pg_sleep(10)-- ' ```
    - The ``` || `` is used for string concatenation so it forces to evaluate the expression on the right.
    
    - ``` pg_sleep(10) ``` Tells to **wait for 10 second** to execute the query

    - ``` -- ``` Tells to ignore the rest of the query 
