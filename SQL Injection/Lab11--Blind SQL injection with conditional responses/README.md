# Lab-11: [Blind SQL injection with conditional responses](https://portswigger.net/web-security/sql-injection/blind/lab-conditional-responses)

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and no error messages are displayed. But the application includes a Welcome back message in the page if the query returns any rows. 

The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user. 

**Aim :-** To solve the lab, log in as the administrator user. 

**Hint :-** You can assume that the password only contains lowercase, alphanumeric characters. 



## Solution
- Alter the cookie and confirm SQLi
    - Capture the request in burp suit and use the following payloads on the **TrackingId** cookie and observe the response
    - ``` ' AND '1'='1 ```
        1=1 means the condition is true and returns **Welcome Back** message in the response
    - ``` ' AND '1'='2 ```
        1=2 means the condition is false and doesn't returns a **Welcome Back** message in the response
    It confirms the execution of the SQL payload


- Confirm the **users** table and **administrator** user in the table
    - Use the following payload to confirm the **users table**
        ``` ' AND (SELECT 'a' FROM users LIMIT 1)='a ```
        The query forces the database to select a fixed value ```('a')``` from the users table, by puting ```LIMIT 1``` ensure that only a single row is returned. This prevents errors caused by multiple rows being returned from the subquery. If the users table exists and the query executes successfully, the condition evaluates to TRUE, and the application responds normally and return the **Welcome Back** message, confirming the presence of the **users** table in the database.
    
    - Use the following payload to confirm the **administrator table**
        ``` ' AND (SELECT 'a' FROM users WHERE username='administrator')='a` ```
        The query retrieves value from the users table only if there is a user with the username ``` administrator ``` is present. If the request responds with a **Welcome Back** message that confirms the presence of the ``` administrator ``` user.


- Find the number of characters in the **password** for the **administrator**
    - Use the payload ``` ' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>1)='a ```
        - The query checks whether the ``` administrator ``` user has a password length greater than 1 character. If the condition is true, the subquery returns the fixed value ``` 'a' ```, making the comparison **TRUE**, and return with a **Welcome Back** message.
    
    - Change the value **1** untill get a response without **Welcome Back** message.

    - ``` ' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>20)='a ``` The payload with value **20** returns the response without a **Welcome Back** message. There is **20 character in the password**


- Retrieve the Password
    ``` ' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='a ```
    - The payload retrieves a single character from the administrator password and compare with the character ``` 'a ```, if both matches then condition becomes True and returns with the **Welcome Back** message otherwise without the message.

    - Send the request to **Intruder** and select the **Cluster bombing attack**
    
    - Select index position 1 from ``` (password,1,1) ``` and click the **Add §** for select position 1, select the character ``` a ``` and click **Add §** for select position 2. The payload will look like the following
    ``` ' AND (SELECT SUBSTRING(password,§1§,1) FROM users WHERE username='administrator')='§a§ ```

    - Configure the payload **position 1** to **1-20** and payload **position 2** to **0-1** also **a-z**, Start the attack

    - Check for the responses with **Welcome Back** message and retrive the characters that replaced in the payload **position 2** in the order of 1 - 20 from the payload position 1, combine all the characters will give the password of ``` administrator ```  
